---
title: GoHumanLoop WeWork
category: entities
tags: [ai-agent, wework, approval, go]
aliases: [gohumanloop-wework, GoHumanLoop-WeWork, 企业微信 HumanLoop 服务]
relationships:
  - target: "[[entities/gohumanloop]]"
    type: extends
  - target: "[[concepts/human-in-the-loop]]"
    type: implements
  - target: "[[skills/wework-human-loop-deployment]]"
    type: related_to
sources:
  - workbench/articles/published/2026-06-02-gohumanloop-wework/index.md
  - workbench/articles/published/2026-06-05-gohumanloop-wework-langgraph/index.md
summary: GoHumanLoop WeWork 是把 GoHumanLoop 审批和信息获取请求接入企业微信审批体系的示例服务。
provenance:
  extracted: 0.84
  inferred: 0.16
  ambiguous: 0.0
base_confidence: 0.61
lifecycle: draft
lifecycle_changed: 2026-07-08
tier: supporting
created: 2026-07-08T08:33:23Z
updated: 2026-07-08T08:33:23Z
---

# GoHumanLoop WeWork

GoHumanLoop WeWork 是针对企业微信场景的 API Service，用于把 GoHumanLoop 的审批、获取信息等请求连接到企业微信应用和审批流程。

## Key Ideas

- 服务面向企业内部协同：Agent 触发 human loop 请求，API provider 将请求发送到企业微信审批或信息模板。
- 它提供两类接口：对接 GoHumanLoop API Provider 的 HumanLoop 接口，以及用于安全认证的 API Key 获取接口。
- 企业微信侧需要创建应用，配置企业 ID、应用 ID、应用 Secret、Token、EncodingAESKey、审批模板 ID、信息模板 ID、创建人和审批人。
- GoHumanLoop 与 WeWork 服务配合后，Agent 可以在 LangGraph 中通过 API provider 发起企业微信审批，并根据返回状态继续或终止流程。

## Deployment Shape

- 企业微信应用提供外部审批和消息入口。
- GoHumanLoop WeWork 服务接收 HumanLoop 请求，转换为企业微信审批流程。
- Agent 侧通过 GoHumanLoop `APIProvider` 调用该服务，并在 workflow 中读取审批结果。
- 反向代理、可访问回调 URL、数据库和 API Key 管理是部署中的关键工程点。 ^[inferred]

## Related

- [[entities/gohumanloop]] — WeWork 服务扩展的基础库。
- [[skills/wework-human-loop-deployment]] — 企业微信应用、模板和服务部署步骤。
- [[skills/langgraph-human-loop-integration]] — 与 LangGraph workflow 组合的示例。
- [[concepts/human-in-the-loop]] — 服务要实现的控制模式。

## Open Questions

- 文章把 GoHumanLoop WeWork 定位为示例服务；生产部署时的多租户、审计、权限和密钥轮换策略还需要补充。 ^[inferred]

## Sources

- [[references/published-article-batch-2026-06]] — 企业微信系列两篇文章。
