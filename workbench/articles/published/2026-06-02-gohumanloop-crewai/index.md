---
url: https://zhuanlan.zhihu.com/p/1928959362552014309
title: "使用GoHumanLoop增强你的Agent人机协同 - CrewAI 中的实践"
description: "GoHumanLoop 介绍GitHub地址： GoHumanLoop GoHumanLoop：是一个Python库，使AI Agent能够在关键阶段动态请求人类输入（批准/反馈/对话）。 CrewAI介绍官网：www.crewai.com/Github：https://github.com/crewAIInc…"
author: "关于作者赛博东哥CyberFD  专注AI Agent流程管理｜个人知识管理与创造 回答13文章15关注者1,062​关注他​发私信"
coverImage: "assets/2026-06-02-gohumanloop-crewai-cover.jpg"
language: "zh"
captured_at: "2026-06-02T07:30:52.706Z"
source_channel: "zhihu"
imported_at: "2026-07-02"
---

# 使用GoHumanLoop增强你的Agent人机协同 - CrewAI 中的实践

-   GitHub地址：

![](assets/2026-06-02-gohumanloop-crewai-fig1.jpg)

`GoHumanLoop`：是一个Python库，使AI Agent能够在关键阶段动态请求人类输入（批准/反馈/对话）。

## CrewAI介绍

-   官网：

-   Github：

目前最流行的 Mutil-Agent 框架之一

![](assets/2026-06-02-gohumanloop-crewai-fig2.jpg)

CrewAI 官网

## 一. 高效构建Human-in-the-Loop流程

今天我们就一起来使用 GoHumanLoop 在 CrewAI 框架上构建一个通过邮件来发送审批请求的例子

-   **需求背景：**

1.  构建一个Agent，其中存在一个关键步骤需要特定管理人员进行审批，审批通过后方可继续执行。
2.  审批人通过邮件来获取审批信息，并通过回复邮件完成审批

好，我们就根据以上背景，先构建一个**CrewAI Agent**

```
import os
from crewai import Agent, Crew, Task
from crewai.tools import tool

PROMPT = """multiply 2 and 5, then add 32 to the result"""

@tool
def add(a: int, b: int) -> int:
    """Add two numbers together."""
    return a + b

@tool
def multiply(a: int, b: int, approval_result=None) -> int:
    """multiply two numbers"""
    print(f"approval_result: {approval_result}")
    return a * b

general_agent = Agent(
    role="Math Professor",
    goal="""Provide the solution to the students that are asking
    mathematical questions and give them the answer.""",
    backstory="""You are an excellent math professor that likes to solve math questions
    in a way that everyone can understand your solution""",
    allow_delegation=False,
    tools=[add, multiply],
    verbose=True,
)

task = Task(
    description=PROMPT,
    agent=general_agent,
    expected_output="A numerical answer.",
)

crew = Crew(agents=[general_agent], tasks=[task], verbose=True)

if __name__ == "__main__":
    result = crew.kickoff()
    print("\n\n---------- RESULT ----------\n\n")
    print(result)
```

上述代码就是一个简单的示例，假定 `multiply` 操作就是我们定义的关键步骤，需要管理人员审批。 目前 CrewAI 框架中，支持两种方式

-   终端输入
-   [webhook](https://link.zhihu.com/?target=https%3A//docs.crewai.com/learn/human-in-the-loop%23human-in-the-loop-hitl-workflows)

这两种方式都不够灵活，并且支持有限，不能满足我们审批需求。 为此 `GoHumanLoop` 就发挥威力了，通过`GoHumanLoop`的简单封装，即可实现
让我们来看看使用 GoHumanLoop 后的代码 ➡️

让我们来看看上述代码

-   `EmailProvider` 是`GoHumanLoop`提供的对外审批、请求等的服务，专门用于邮件场景
-   `DefaultHumanLoopManager` 是 `GoHumanLoop` 默认的管理器，负责管理 `Provider`等
-   `[HumanloopAdapter](https://zhida.zhihu.com/search?content_id=260444684&content_type=Article&match_order=1&q=HumanloopAdapter&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3ODA1NTgyMzgsInEiOiJIdW1hbmxvb3BBZGFwdGVyIiwiemhpZGFfc291cmNlIjoiZW50aXR5IiwiY29udGVudF9pZCI6MjYwNDQ0Njg0LCJjb250ZW50X3R5cGUiOiJBcnRpY2xlIiwibWF0Y2hfb3JkZXIiOjEsInpkX3Rva2VuIjpudWxsfQ.4NW9cFlC81glKpy81Ajg0rxcEstf7RZY6BSMwXSF6wU&zhida_source=entity)` 是`GoHumanLoop`对外提供的通用适配器，可以适配不同的 Agent 框架, 如 LangGraph、CrewAI 等，负责对外输出`GoHumanLoop`的各项能力。
-   `[require_approval](https://zhida.zhihu.com/search?content_id=260444684&content_type=Article&match_order=1&q=require_approval&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3ODA1NTgyMzgsInEiOiJyZXF1aXJlX2FwcHJvdmFsIiwiemhpZGFfc291cmNlIjoiZW50aXR5IiwiY29udGVudF9pZCI6MjYwNDQ0Njg0LCJjb250ZW50X3R5cGUiOiJBcnRpY2xlIiwibWF0Y2hfb3JkZXIiOjEsInpkX3Rva2VuIjpudWxsfQ.5Qh4gT_04JTV_hWk6l63nKYMvuoSVPXWskZ9OE53a90&zhida_source=entity)` 是`GoHumanLoop`的核心能力之一，提供审批功能。 `metadata`参数中设定好用于 `EmailProvider`接收人的邮箱

###
运行示例代码

1.  创建一个 .env 文件

```
cp .env.example .env
# Modify the .env file with your API key and other configuration
# 参考如下：

# DeepSeek API (https://platform.deepseek.com/api_keys)
MODEL="deepseek-chat"
OPENAI_API_KEY='sk-xxxx'
OPENAI_API_BASE="https://api.deepseek.com/v1"

# EmailProvider 配置示例
# 邮箱服务器设置
SMTP_SERVER="smtp.163.com"
SMTP_PORT="587"
IMAP_SERVER="imap.163.com"
IMAP_PORT="993"

# 邮箱凭证
GOHUMANLOOP_EMAIL_USERNAME="xxx@163.com"
GOHUMANLOOP_EMAIL_PASSWORD="xxxx"

# 测试收件人
TEST_RECIPIENT_EMAIL="xxx@qq.com"

```

2\. 运行代码

```
uv run main.py
```

3\. 检查邮箱是否收到审批邮件

![](assets/2026-06-02-gohumanloop-crewai-fig3.jpg)

检查邮箱

4\. 回复邮件（同意或拒绝）

根据指导内容，以提供的格式回复同意或拒绝的信息

```
===== PLEASE KEEP THIS LINE AS CONTENT START MARKER =====
Decision: approve
Reason: [Your reason]
===== PLEASE KEEP THIS LINE AS CONTENT END MARKER =====
```

![](assets/2026-06-02-gohumanloop-crewai-fig4.jpg)

Crew 运行界面

审批同意，完成任务任务啦～

## 二. 更多示例

更多示例，可以访问以下示例仓库

目前还在建设中，欢迎大家使用`GoHumanLoop`后，分享投稿给我噢～

## 三. 最后

`GoHumanLoop`采用MIT协议开源，欢迎大家贡献力量，一起共建`GoHumanLoop`
您可以做

-   报告错误
-   建议改进
-   文档贡献
-   代码贡献
    ...

如果你对本项目感兴趣，欢迎评论区交流和联系我～

-   GitHub地址：

如果感觉对你有帮助，欢迎支持 Star 一下