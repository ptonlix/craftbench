---
url: https://zhuanlan.zhihu.com/p/1929835908267480384
title: "使用GoHumanLoop将你的AI Agent在企业微信建立人机协同（一）"
description: "一. 前言 之前已经发过两篇文章，介绍GoHumanLoop在LangGraph和CrewAI这两个 AI Agent 框架中的实践应用。 使用GoHumanLoop增强你的Agent人机协同 - LangGraph 中的实践使用GoHumanLoop增强你的Agent人机协同 - Cr…"
author: "关于作者赛博东哥CyberFD  专注AI Agent流程管理｜个人知识管理与创造 回答13文章15关注者1,062​关注他​发私信"
coverImage: "assets/2026-06-02-gohumanloop-wework-cover.jpg"
language: "zh"
captured_at: "2026-06-02T07:55:36.286Z"
source_channel: "zhihu"
imported_at: "2026-07-02"
---

# 使用GoHumanLoop将你的AI Agent在企业微信建立人机协同（一）

![](assets/2026-06-02-gohumanloop-wework-fig1.jpg)

GoHumanLoop WeWork 介绍

## 一. 前言

之前已经发过两篇文章，介绍`GoHumanLoop`在`LangGraph`和`CrewAI`这两个 AI Agent 框架中的实践应用。

`GoHumanLoop`：是一个Python库，使AI Agent能够在关键阶段动态请求人类输入（批准/反馈/对话）。

-   GitHub地址：

之前的应用主要通过本地终端来获取人类的输入-审批、反馈等。在`GoHumanLoop`也支持通过[API Provider](https://zhida.zhihu.com/search?content_id=260551364&content_type=Article&match_order=1&q=API+Provider&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3ODA1NTk3MjksInEiOiJBUEkgUHJvdmlkZXIiLCJ6aGlkYV9zb3VyY2UiOiJlbnRpdHkiLCJjb250ZW50X2lkIjoyNjA1NTEzNjQsImNvbnRlbnRfdHlwZSI6IkFydGljbGUiLCJtYXRjaF9vcmRlciI6MSwiemRfdG9rZW4iOm51bGx9.16kP4_OmrtdRdcGjnZhwG726jbQfYfUOfmKbN_4x3eU&zhida_source=entity) 来对接外部的审批系统。
最近我开发了一个对接到企业微信的 API Service，能将GoHumanLoop 的审批、获取信息等请求与用户的企业微信系统进行链接，帮助用户完成AI Agent 连接到企业微信，实现更强大的`[Human-in-the-Loop](https://zhida.zhihu.com/search?content_id=260551364&content_type=Article&match_order=1&q=Human-in-the-Loop&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3ODA1NTk3MjksInEiOiJIdW1hbi1pbi10aGUtTG9vcCIsInpoaWRhX3NvdXJjZSI6ImVudGl0eSIsImNvbnRlbnRfaWQiOjI2MDU1MTM2NCwiY29udGVudF90eXBlIjoiQXJ0aWNsZSIsIm1hdGNoX29yZGVyIjoxLCJ6ZF90b2tlbiI6bnVsbH0.kFEiBsNm3FdhleKRjUvOgHHNIhVUoKnNtnJqE5R2n0c&zhida_source=entity)`。
今天我们来一起看一下这个 API Service - `GoHumanLoop-WeWork`

## 二. 项目介绍

**GoHumanLoop WeWork** 是针对`GoHumanLoop`在企业微信场景下进行审批、获取信息操作的示例服务。方便用户在使用`GohumanLoop`时，对接到自己的企业微信环境中。

✈️✈️✈️ **GitHub项目地址：**

![](assets/2026-06-02-gohumanloop-wework-fig2.jpg)

GoHumanLoop与Gohumanloop-Wework架构关系

从上图看出

-   `GoHumanLoop`提供了一套统一的 API 接口，通过`API Provider`对外提供。
-   `gohumanloop-wework`实现了`API Consumer`的功能，通过`API Provider`来获取审批相关的信息，并且通过企业微信 WeWork API 实现了与用户的企业微信应用进行交互，发送审批请求和获取审批事件回调等。

`gohumanloop-wework`采用[Beego](https://link.zhihu.com/?target=https%3A//link.juejin.cn/%3Ftarget%3Dhttps%253A%252F%252Fgithub.com%252Fbeego%252Fbeego)作为 Web 框架。`sqlite`作为简单的数据存储。[go-workwx](https://link.zhihu.com/?target=https%3A//link.juejin.cn/%3Ftarget%3Dhttps%253A%252F%252Fgithub.com%252Fxen0n%252Fgo-workwx)作为企业微信 API 实现。提供一个可拓展的 GoHumanLoop 企业微信审批示例服务。

-   访问 Swagger 文档:

![](assets/2026-06-02-gohumanloop-wework-fig3.jpg)

`gohumanloop-wework`提供两大类接口，一个对接`GoHumanLoop`的 API Provider 的`HumanLoop`接口。另一个是获取 API Key 的接口，方便安全认证。

## 三. 项目部署

> 需要用户提前准备好企业微信和企业微信应用 详情见：[work.weixin.qq.com/](https://link.zhihu.com/?target=https%3A//link.juejin.cn/%3Ftarget%3Dhttps%253A%252F%252Fwork.weixin.qq.com%252F)
>
> 用户需要获取企业微信`企业ID`
> 用户需要在企业微信中创建应用`GoHumanLoop`，获取`应用ID`和`应用Secret`
> 用户需要在应用中,开启 API 接收消息。获取`Token`和`EncodingAESKey` 用于接收审批消息事件。审批应用中设置可调用接口的应用，关联新创建的应用。
> 用户需要将`企业ID`、`应用ID`、`应用Secret`、`Token`、`EncodingAESKey`配置到 GoHumanLoop 中
> 用户需要在企业微信中创建审批模板，获取`审批模板ID`和`信息模板ID`
> 用户需要将`审批模板ID`、`信息模板ID`、`创建人ID`、`审批人ID`配置到 GoHumanLoop 中

### 1\. 配置文件

-   项目配置样例文件在`conf/app.conf.example`中

```
appname = gohumanloop-wework
httpport = 8080 # HTTP 端口按需配置

# wework
agentid = 1000003 # 企业微信应用ID
corpsecret = XXXXX # 应用Secret
corpid = XXXXX # 企业ID
ptoken = XXXXX # Token
pkey = XXXXX # EncodingAESKey

# template
approve_template_id = 8TmoaR5xEaZsuzKyRT4Zt82FLYCYXVN5EVk6R # 审批模板ID
info_template_id = 3WN63LowuwFRsDXft1GbiQi4NrYyLApeejYCBs3S # 信息模板ID
creator_userid = ChenFuDong # 创建人ID，详情参考企业微信文档
approver_userid = ChenFuDong # 审批人ID (默认审批人，实际可通过 GoHumanLoop Metadata数据指定)

# database
datapath = ./data/gohumanloop.db # 数据库路径
```

-   修改配置文件

```
mv conf/app.conf.example conf/app.conf
```

### 2\. 企业微信审批模板

目前这个版本中，支持审批和信息获取。分别使用两个模板，模板格式固定，需要参考以下配置：

![](assets/2026-06-02-gohumanloop-wework-fig4.jpg)

审批模板

-   参考图片内的字段，都是文本控件和多行文本控件。包括以下字段

1.  任务 ID
2.  对话 ID
3.  请求 ID
4.  HumanLoop 类型
5.  申请内容
6.  申请问题
7.  申请说明

以上字段由 GoHumanLoop 库来传输并自动填充并自动发起审批流程

![](assets/2026-06-02-gohumanloop-wework-fig5.jpg)

审批模板

-   审批流程可以参考上图设置，审批人设置为自选

![](assets/2026-06-02-gohumanloop-wework-fig6.jpg)

信息获取模板

-   参考图片内的字段，都是文本控件和多行文本控件。详情同审批流程模板和说明

![](assets/2026-06-02-gohumanloop-wework-fig7.jpg)

信息获取模板

-   信息获取流程不需要具体审批，只需要获取具体信息。没有设置审批人，只设置了办理人，专用于获取信息。

### 3\. 部署方式

GoHumanLoop Wework 支持两种部署方式手动部署和 [Docker 部署](https://zhida.zhihu.com/search?content_id=260551364&content_type=Article&match_order=1&q=Docker+%E9%83%A8%E7%BD%B2&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3ODA1NTk3MjksInEiOiJEb2NrZXIg6YOo572yIiwiemhpZGFfc291cmNlIjoiZW50aXR5IiwiY29udGVudF9pZCI6MjYwNTUxMzY0LCJjb250ZW50X3R5cGUiOiJBcnRpY2xlIiwibWF0Y2hfb3JkZXIiOjEsInpkX3Rva2VuIjpudWxsfQ.bTkjFzxtPzuKXurc60AOAF1FdAjYHs3NPpZA7IMvMW0&zhida_source=entity)。

> 这两种方式均需要有企业微信同一注册主体下的服务器。服务器和域名需要已备案，开启 API 接收消息时也需要域名验证是否是同一注册主体下

1.  手动部署

Go 版本要求：1.23.0

-   下载代码

```
git clone https://github.com/ptonlix/gohumanloop-wework.git
```

-   编译

```
make build
```

-   运行

```
./gohumanloop-wework
```

2\. Docker 部署

-   提前安装好 Docker 服务
-   拉取镜像

```
docker pull ptonlix/gohumanloop-wework:latest
```

-   运行容器

```
解释

docker run -d \
  --name gohumanloop-wework \
  -v /path/to/local/conf:/app/conf \
  -v /path/to/local/data:/app/data \
  -p 9800:9800 \
  ptonlix/gohumanloop-wework:latest
```

3\. 配置反向代理

以 Nginx 为例，可以参考在 Nginx 配置文件中添加以下路由配置

```
location ^~ /humanloop/ {
        proxy_pass http://127.0.0.1:9800/gohumanloop/callback;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Real-Port $remote_port;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
}

location ^~ /api/v1/humanloop/ {
        proxy_pass http://127.0.0.1:9800;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Real-Port $remote_port;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
}

location ^~ /api/v1/apikey/ {
        proxy_pass http://127.0.0.1:9800;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Real-Port $remote_port;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
}
```

## 四. 实践案例

以我自己创建的企业微信为例，我用同一个企业主体下备案过的腾讯云服务器

-   企业微信创建好应用

![](assets/2026-06-02-gohumanloop-wework-fig8.jpg)

-   配置腾讯云Docker加速地址

```
vim /etc/docker/daemon.json

{
  "registry-mirrors": [
    "https://mirror.ccs.tencentyun.com"
]
}
```

-   拉取镜像

```
docker pull ptonlix/gohumanloop-wework:latest
```

-   运行容器

```
docker run -d \
  --name gohumanloop-wework \
  -v /path/to/local/conf:/app/conf \
  -v /path/to/local/data:/app/data \
  -p 9800:9800 \
  ptonlix/gohumanloop-wework:latest
```

![](assets/2026-06-02-gohumanloop-wework-fig9.jpg)

测试运行容器

-   企业微信配置好API接收消息

![](assets/2026-06-02-gohumanloop-wework-fig10.jpg)

配置API接收消息

## 五. 总结

好了，以上就是我们的`GoHumanLoop-WeWork`链接企业微信进行人机协同`Human-in-the-Loop`的准备工作，下一步让我们看看怎么利用`GoHumanLoop`结合到我们的AI Agent中。
✈️✈️✈️ **GitHub项目地址：**

如果觉得对你有帮助的话，欢迎Star
如果感兴趣的话，可以联系我进一步交流
谢谢～