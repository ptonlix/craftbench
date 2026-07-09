---
url: https://zhuanlan.zhihu.com/p/1927682387803891043
title: "使用GoHumanLoop增强你的Agent人机协同 - LangGraph 中的实践"
description: "GoHumanLoop 介绍GitHub地址：https://github.com/ptonlix/gohumanloop GoHumanLoop：是一个Python库，使AI Agent能够在关键阶段动态请求人类输入（批准/反馈/对话）。 核心功能：人类在环控制：让AI代理系统暂停…"
author: "关于作者赛博东哥CyberFD  专注AI Agent流程管理｜个人知识管理与创造 回答13文章15关注者1,062​关注他​发私信"
coverImage: "assets/2026-06-01-gohumanloop-langgraph-cover.jpg"
language: "zh"
captured_at: "2026-06-01T15:08:00.434Z"
source_channel: "zhihu"
imported_at: "2026-07-02"
---

# 使用GoHumanLoop增强你的Agent人机协同 - LangGraph 中的实践

​

目录

-   GitHub地址：

![](assets/2026-06-01-gohumanloop-langgraph-fig1.jpg)

GoHumanLoop 介绍

`GoHumanLoop`：是一个Python库，使AI Agent能够在关键阶段动态请求人类输入（批准/反馈/对话）。
**核心功能：**

-   人类在环控制：让AI代理系统暂停并升级决策，增强安全性和信任。
-   多渠道集成：支持终端、电子邮件、API控制和支持多个LangGraph/CrewAI等框架（即将推出）。
-   灵活的工作流程：结合自动推理和人工监督，确保人工智能操作的可靠性。

通过连接自主代理和人类判断，确保负责任的AI部署。
今天我们来介绍使用`GoHumanLoop` 如何在`LangGraph`中的增加Agent控制

---

## 一. 场景介绍

在介绍如何使用前，还是先选定一个需求场景，方便大家更好理解

-   我需要 Agent 帮我给出一个投资建议，并询问我们的意见
-   Agent 根据这份投资建议，实际操作转账投资，在转账前需要我们批准
-   操作完成后，询问我对整个流程的反馈

以上面这个假定的金融投资场景为例，来介绍一下 GoHumanLoop 如何来在`LangGraph`中的增强[Human-in-the-loop](https://zhida.zhihu.com/search?content_id=260279606&content_type=Article&match_order=1&q=Human-in-the-loop&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3ODA0OTkyNzEsInEiOiJIdW1hbi1pbi10aGUtbG9vcCIsInpoaWRhX3NvdXJjZSI6ImVudGl0eSIsImNvbnRlbnRfaWQiOjI2MDI3OTYwNiwiY29udGVudF90eXBlIjoiQXJ0aWNsZSIsIm1hdGNoX29yZGVyIjoxLCJ6ZF90b2tlbiI6bnVsbH0.l1u36FxaMaho-4kIaveibxuN1mOOhie3zSinWQopnv0&zhida_source=entity) 控制

---

## 二. 需求实现

我们先用 `LangGraph` 来实现一个基础的 Workflow

```
from typing import Dict, Any, List, Annotated, TypedDict
import operator
import os
from dotenv import load_dotenv
from langchain_core.messages import HumanMessage, AIMessage, SystemMessage
from langchain_openai import ChatOpenAI
from langgraph.graph import StateGraph, END
from langgraph.prebuilt import ToolNode

from gohumanloop.adapters.langgraph_adapter import HumanloopAdapter
from gohumanloop.core.manager import DefaultHumanLoopManager
from gohumanloop.providers.terminal_provider import TerminalProvider
from gohumanloop.core.interface import HumanLoopStatus
import logging
from typing_extensions import TypedDict

# 设置日志配置
logging.basicConfig(
    level=logging.INFO, format="%(asctime)s - %(name)s - %(levelname)s - %(message)s"
)
logger = logging.getLogger("langgraph_adapter")

# 加载环境变量
load_dotenv()

# 定义状态类型
class AgentState(TypedDict):
    messages: List[Any]
    next: str

# 从环境变量获取API密钥和基础URL
api_key = os.getenv("OPENAI_API_KEY")
api_base = os.getenv("OPENAI_API_BASE")

# 创建 LLM
llm = ChatOpenAI(model="deepseek-chat", base_url=api_base)

def execute_financial_transaction(
    amount: float, account_id: str, approval_result=None
) -> Dict[str, Any]:
    """执行一个需要人工审批的金融交易

    Args:
        amount: 交易金额
        account_id: 账户ID
        approval_result: 审批结果信息

    Returns:
        Dict: 交易结果
    """
    logger.info(f"审批信息: {approval_result}")

    # 根据审批结果处理交易
    if approval_result and approval_result.get("status") == HumanLoopStatus.APPROVED:
        return {
            "status": "success",
            "message": f"成功执行金额为 {amount} 的交易到账户 {account_id}",
            "transaction_id": "tx_123456789",
        }
    else:
        return {
            "status": "cancelled",
            "message": f"交易已被拒绝并取消: 金额 {amount}, 账户 {account_id}",
            "transaction_id": None,
        }

# LangGraph 工作流节点
def agent(state: AgentState) -> AgentState:
    """AI 代理处理节点"""
    messages = state["messages"]

    # 添加系统提示，定义LLM的角色和任务
    if not any(msg.type == "system" for msg in messages):
        system_message = SystemMessage(
            content="""
你是一位专业的金融顾问助手，负责帮助用户处理金融交易请求。
你的职责包括：
1. 理解用户的金融交易需求
2. 提供专业的金融建议
3. 协助用户完成交易流程
4. 确保交易安全和合规

请根据用户的请求，提供清晰的交易建议和操作方案。你的回复将由人工审核后再执行。
"""
        )
        messages = [system_message] + messages

    # 为用户消息添加更明确的指令
    last_message = messages[-1]
    if isinstance(last_message, HumanMessage):
        # 保留原始用户消息
        user_content = last_message.content

        # 构建更详细的提示
        enhanced_prompt = f"""
用户请求: {user_content}

请分析这个金融交易请求并提供以下内容:
1. 交易类型和金额确认
2. 交易风险评估
3. 执行建议和注意事项
4. 是否建议执行此交易(是/否)及理由

请以专业金融顾问的身份回复，你的建议将被用于决定是否执行此交易。
"""
        # 替换最后一条消息
        messages = messages[:-1] + [HumanMessage(content=enhanced_prompt)]

    # 调用LLM获取响应
    response = llm.invoke(messages)

    # 恢复原始用户消息以保持对话连贯性
    if isinstance(last_message, HumanMessage):
        # 使用列表切片替换最后一个元素，避免直接赋值可能导致的问题
        messages = messages[:-1] + [last_message]

    return {"messages": messages + [response], "next": "human_review"}

def human_review(state: AgentState) -> AgentState:
    """人工审核节点"""
    messages = state["messages"]
    last_message = messages[-1].content if messages else "无消息"

    approval_data = input("请输入审批结果")
    logger.info(f"人工审核结果: {approval_data}")

    ...

def process_transaction(state: AgentState) -> AgentState:
    """处理交易节点"""
    messages = state["messages"]

    # 模拟交易处理
    transaction_result = execute_financial_transaction(
        amount=100.0, account_id="user_12345"
    )

    result_message = HumanMessage(content=f"交易结果: {transaction_result['message']}")
    return {"messages": messages + [result_message], "next": "collect_feedback"}

@adapter.require_info(ret_key="feedback_data")
def collect_feedback(state: AgentState, feedback_data={}) -> AgentState:
    """收集用户反馈节点"""
    messages = state["messages"]

    logger.info(f"获取的反馈信息: {feedback_data}")

    feedback_message = HumanMessage(
        content=f"收到用户反馈: {feedback_data.get('response', '无反馈')}"
    )
    return {"messages": messages + [feedback_message], "next": END}

def router(state: AgentState) -> str:
    """路由节点，决定下一步执行哪个节点"""
    return state["next"]

def main():
    # 创建工作流图
    workflow = StateGraph(AgentState)

    # 添加节点
    workflow.add_node("agent", agent)
    workflow.add_node("human_review", human_review)
    workflow.add_node("process_transaction", process_transaction)
    workflow.add_node("collect_feedback", collect_feedback)

    # 设置边和路由
    workflow.set_entry_point("agent")
    workflow.add_edge("agent", "human_review")
    workflow.add_conditional_edges("human_review", router)
    workflow.add_conditional_edges("process_transaction", router)
    workflow.add_conditional_edges("collect_feedback", router)

    # 编译工作流
    app = workflow.compile()

    # 运行工作流
    try:
        # 创建一个更符合金融投资场景的初始状态
        initial_state = {
            "messages": [
                HumanMessage(
                    content="我想投资5万元购买一些低风险的基金产品，主要用于退休储蓄，期限大约10年。请给我一些建议？"
                )
            ],
            "next": "agent",
        }

        for state in app.stream(initial_state, stream_mode="values"):
            messages = state.get("messages", {})
            if messages:
                logger.info(f"当前状态: {state['next']}")
                logger.info(f"最新消息: {messages[-1].content}")

        logger.info("工作流执行完成!")
    except Exception as e:
        logger.exception(f"工作流执行错误: {str(e)}")

if __name__ == "__main__":
    main()

```

上面这个例子中，定义了几个节点，workflow 流程如下：

![](assets/2026-06-01-gohumanloop-langgraph-fig2.jpg)

-   `agent`： 通过 LLM 生成投资方案
-   `human_review`：人工审核投资方案
-   `process_transaction`： 执行转账投资等高风险操作
-   `collect_feedback`： 收集整个流程的意见反馈

根据这上面几个简单的节点，串联起了整个工作流
正常使用 `LangGraph` 一般只能通过 `interrupt` 来中断流程，**等待用户信息输入（需要额外编写各种交互流程）**，然后继续流程。
而使用 `GoHumanLoop` 通过简单的封装就能与外部审批系统做交互，高效完成需要人类介入的工作
让我们来一起看一下在 这个例子中如何使用 `GoHumanLoop`

---

## ⛓️ 三. 使用GoHumanLoop改造LangGraph

首先，先定义`HumanLoopManager`和`HumanloopAdapter`实例，`HumanloopAdapter`用来适配各种 Agent 框架，`HumanLoopManager`是用来管理各种审批方式提供者，比如这里例子中，为了方便演示，我们使用了`TerminalProvider`

-   `TerminalProvider`： 通过终端交互提供审批的信息

```
# 创建 HumanLoopManager 实例
manager = DefaultHumanLoopManager(
    initial_providers=TerminalProvider(name="TerminalProvider")
)

# 创建 hAdapter 实例
adapter = HumanloopAdapter(manager, default_timeout=60)

```

然后，使用装饰器封装`LangGraph`的节点

```
@adapter.require_approval(ret_key="approval_data", execute_on_reject=True)
def human_review(state: AgentState, approval_data=None) -> AgentState:
    """人工审核节点"""
    messages = state["messages"]
    last_message = messages[-1].content if messages else "无消息"

    logger.info(f"人工审核结果: {approval_data}")

    # 添加审核结果到消息
    if approval_data and approval_data.get("status") == HumanLoopStatus.APPROVED:
        review_message = HumanMessage(content=f"[已审核] {last_message}")
        return {"messages": messages + [review_message], "next": "process_transaction"}
    else:
        review_message = HumanMessage(content=f"[审核拒绝] 请重新生成回复")
        return {"messages": messages + [review_message], "next": "agent"}

# 使用审批装饰器的敏感操作
@adapter.require_approval(execute_on_reject=True)
def execute_financial_transaction(
    amount: float, account_id: str, approval_result=None
) -> Dict[str, Any]:
    """执行一个需要人工审批的金融交易

    Args:
        amount: 交易金额
        account_id: 账户ID
        approval_result: 审批结果信息

    Returns:
        Dict: 交易结果
    """
    logger.info(f"审批信息: {approval_result}")

    # 根据审批结果处理交易
    if approval_result and approval_result.get("status") == HumanLoopStatus.APPROVED:
        return {
            "status": "success",
            "message": f"成功执行金额为 {amount} 的交易到账户 {account_id}",
            "transaction_id": "tx_123456789",
        }
    else:
        return {
            "status": "cancelled",
            "message": f"交易已被拒绝并取消: 金额 {amount}, 账户 {account_id}",
            "transaction_id": None,
        }

```

`require_approval` 是专门用于审批的装饰器， `execute_on_reject`是即使拒绝了还能继续执行，方便让 Agent 继续执行拒绝操作的流程，否则直接抛出异常，停止整个工作流 `execute_financial_transaction`节点中，我们还定义了一个参数`approval_result`，用于接收审批的详细信息，比如审批的状态和审批反馈。该参数，还可以通过`ret_key`来指定。

###
1\. 完整代码：

```
# /// script
# requires-python = ">=3.10"
# dependencies = [
# "gohumanloop>=0.0.9",
# "langgraph>=0.4.7",
# "langchain-openai>=0.3.12"]
# ///

from typing import Dict, Any, List, Annotated, TypedDict
import operator
import os
from dotenv import load_dotenv
from langchain_core.messages import HumanMessage, AIMessage, SystemMessage
from langchain_openai import ChatOpenAI
from langgraph.graph import StateGraph, END
from langgraph.prebuilt import ToolNode

from gohumanloop.adapters.langgraph_adapter import HumanloopAdapter
from gohumanloop.core.manager import DefaultHumanLoopManager
from gohumanloop.providers.terminal_provider import TerminalProvider
from gohumanloop.core.interface import HumanLoopStatus
import logging
from typing_extensions import TypedDict

# 设置日志配置
logging.basicConfig(
    level=logging.INFO, format="%(asctime)s - %(name)s - %(levelname)s - %(message)s"
)
logger = logging.getLogger("langgraph_adapter")

# 加载环境变量
load_dotenv()

# 定义状态类型
class AgentState(TypedDict):
    messages: List[Any]
    next: str

# 从环境变量获取API密钥和基础URL
api_key = os.getenv("OPENAI_API_KEY")
api_base = os.getenv("OPENAI_API_BASE")

# 创建 LLM
llm = ChatOpenAI(model="deepseek-chat", base_url=api_base)

# 创建 HumanLoopManager 实例
manager = DefaultHumanLoopManager(
    initial_providers=TerminalProvider(name="TerminalProvider")
)

# 创建 LangGraphAdapter 实例
adapter = HumanloopAdapter(manager, default_timeout=60)

# 使用审批装饰器的敏感操作
@adapter.require_approval(execute_on_reject=True)
def execute_financial_transaction(
    amount: float, account_id: str, approval_result=None
) -> Dict[str, Any]:
    """执行一个需要人工审批的金融交易

    Args:
        amount: 交易金额
        account_id: 账户ID
        approval_result: 审批结果信息

    Returns:
        Dict: 交易结果
    """
    logger.info(f"审批信息: {approval_result}")

    # 根据审批结果处理交易
    if approval_result and approval_result.get("status") == HumanLoopStatus.APPROVED:
        return {
            "status": "success",
            "message": f"成功执行金额为 {amount} 的交易到账户 {account_id}",
            "transaction_id": "tx_123456789",
        }
    else:
        return {
            "status": "cancelled",
            "message": f"交易已被拒绝并取消: 金额 {amount}, 账户 {account_id}",
            "transaction_id": None,
        }

# LangGraph 工作流节点
def agent(state: AgentState) -> AgentState:
    """AI 代理处理节点"""
    messages = state["messages"]

    # 添加系统提示，定义LLM的角色和任务
    if not any(msg.type == "system" for msg in messages):
        system_message = SystemMessage(
            content="""
你是一位专业的金融顾问助手，负责帮助用户处理金融交易请求。
你的职责包括：
1. 理解用户的金融交易需求
2. 提供专业的金融建议
3. 协助用户完成交易流程
4. 确保交易安全和合规

请根据用户的请求，提供清晰的交易建议和操作方案。你的回复将由人工审核后再执行。
"""
        )
        messages = [system_message] + messages

    # 为用户消息添加更明确的指令
    last_message = messages[-1]
    if isinstance(last_message, HumanMessage):
        # 保留原始用户消息
        user_content = last_message.content

        # 构建更详细的提示
        enhanced_prompt = f"""
用户请求: {user_content}

请分析这个金融交易请求并提供以下内容:
1. 交易类型和金额确认
2. 交易风险评估
3. 执行建议和注意事项
4. 是否建议执行此交易(是/否)及理由

请以专业金融顾问的身份回复，你的建议将被用于决定是否执行此交易。
"""
        # 替换最后一条消息
        messages = messages[:-1] + [HumanMessage(content=enhanced_prompt)]

    # 调用LLM获取响应
    response = llm.invoke(messages)

    # 恢复原始用户消息以保持对话连贯性
    if isinstance(last_message, HumanMessage):
        # 使用列表切片替换最后一个元素，避免直接赋值可能导致的问题
        messages = messages[:-1] + [last_message]

    return {"messages": messages + [response], "next": "human_review"}

@adapter.require_approval(ret_key="approval_data", execute_on_reject=True)
def human_review(state: AgentState, approval_data=None) -> AgentState:
    """人工审核节点"""
    messages = state["messages"]
    last_message = messages[-1].content if messages else "无消息"

    logger.info(f"人工审核结果: {approval_data}")

    # 添加审核结果到消息
    if approval_data and approval_data.get("status") == HumanLoopStatus.APPROVED:
        review_message = HumanMessage(content=f"[已审核] {last_message}")
        return {"messages": messages + [review_message], "next": "process_transaction"}
    else:
        review_message = HumanMessage(content=f"[审核拒绝] 请重新生成回复")
        return {"messages": messages + [review_message], "next": "agent"}

def process_transaction(state: AgentState) -> AgentState:
    """处理交易节点"""
    messages = state["messages"]

    # 模拟交易处理
    transaction_result = execute_financial_transaction(
        amount=100.0, account_id="user_12345"
    )

    result_message = HumanMessage(content=f"交易结果: {transaction_result['message']}")
    return {"messages": messages + [result_message], "next": "collect_feedback"}

@adapter.require_info(ret_key="feedback_data")
def collect_feedback(state: AgentState, feedback_data={}) -> AgentState:
    """收集用户反馈节点"""
    messages = state["messages"]

    logger.info(f"获取的反馈信息: {feedback_data}")

    feedback_message = HumanMessage(
        content=f"收到用户反馈: {feedback_data.get('response', '无反馈')}"
    )
    return {"messages": messages + [feedback_message], "next": END}

def router(state: AgentState) -> str:
    """路由节点，决定下一步执行哪个节点"""
    return state["next"]

def main():
    # 创建工作流图
    workflow = StateGraph(AgentState)

    # 添加节点
    workflow.add_node("agent", agent)
    workflow.add_node("human_review", human_review)
    workflow.add_node("process_transaction", process_transaction)
    workflow.add_node("collect_feedback", collect_feedback)

    # 设置边和路由
    workflow.set_entry_point("agent")
    workflow.add_edge("agent", "human_review")
    workflow.add_conditional_edges("human_review", router)
    workflow.add_conditional_edges("process_transaction", router)
    workflow.add_conditional_edges("collect_feedback", router)

    # 编译工作流
    app = workflow.compile()

    # 运行工作流
    try:
        # 创建一个更符合金融投资场景的初始状态
        initial_state = {
            "messages": [
                HumanMessage(
                    content="我想投资5万元购买一些低风险的基金产品，主要用于退休储蓄，期限大约10年。请给我一些建议？"
                )
            ],
            "next": "agent",
        }

        for state in app.stream(initial_state, stream_mode="values"):
            messages = state.get("messages", {})
            if messages:
                logger.info(f"当前状态: {state['next']}")
                logger.info(f"最新消息: {messages[-1].content}")

        logger.info("工作流执行完成!")
    except Exception as e:
        logger.exception(f"工作流执行错误: {str(e)}")

if __name__ == "__main__":
    main()

```

### 2\. 运行该代码

1.  先安装 UV 工具 （最新的Python包和环境管理工具）

可以前往对应仓库，学习下载：

复制上述代码到 `langgraph_adapter_example.py`

2\. 执行上述代码

```
## Create a `.env` file with your API key:

# DeepSeek API (https://platform.deepseek.com/api_keys)
OPENAI_API_KEY='sk-xxxx'
OPENAI_API_BASE="https://api.deepseek.com/v1"

# 配置环境变量，这里使用的是 DeepSeek。可以自行修改合适的模型
vim .env

```

3\. 使用uv运行该代码

```
uv run langgraph_adapter_example.py
```

4\. 运行过程

![](assets/2026-06-01-gohumanloop-langgraph-fig3.jpg)

交互过程一

生成投资建议，获取人类反馈。根据指引输入`approve`

![](assets/2026-06-01-gohumanloop-langgraph-fig4.jpg)

交互过程二

执行转账投资操作，获取审批。根据指引输入`approve`

![](assets/2026-06-01-gohumanloop-langgraph-fig5.jpg)

交互过程三

输入反馈建议并提交，完成整个工作流

好了，以上就是本期在LangGraph 中的实践，欢迎大家实操体验

---

## 四. 更多示例

更多示例，可以访问以下仓库

目前还在建设中，欢迎大家使用`GoHumanLoop`后，分享投稿给我噢～

---

## 五. 最后

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
