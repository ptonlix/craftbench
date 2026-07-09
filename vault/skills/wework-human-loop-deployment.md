---
title: WeWork Human Loop Deployment
category: skills
tags: [wework, deployment, approval, ai-agent]
aliases: [企业微信 HumanLoop 部署, GoHumanLoop WeWork Deployment]
relationships:
  - target: "[[entities/gohumanloop-wework]]"
    type: uses
  - target: "[[entities/gohumanloop]]"
    type: uses
  - target: "[[concepts/human-in-the-loop]]"
    type: implements
sources:
  - workbench/articles/published/2026-06-02-gohumanloop-wework/index.md
  - workbench/articles/published/2026-06-05-gohumanloop-wework-langgraph/index.md
summary: 部署 GoHumanLoop WeWork 需要配置企业微信应用、审批模板、信息模板、API Key、服务端回调和 Agent 侧 APIProvider。
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

# WeWork Human Loop Deployment

GoHumanLoop WeWork 部署的目标，是让 Agent 的 human loop 请求进入企业微信审批体系，并把审批结果返回给 Agent workflow。

## Deployment Steps

1. 在企业微信中创建应用 `GoHumanLoop`，获取企业 ID、应用 ID、应用 Secret。
2. 配置 Token 和 EncodingAESKey，用于企业微信回调和消息安全。
3. 创建审批模板和信息模板，记录模板 ID。
4. 配置创建人 ID、审批人 ID，必要时通过 GoHumanLoop metadata 动态指定审批人。
5. 部署 GoHumanLoop WeWork 服务，可手动部署或 Docker 部署。
6. 为服务配置数据库、API Key 获取接口和 HumanLoop 接口。
7. 在 Agent 侧使用 GoHumanLoop `APIProvider` 指向该服务。
8. 在 LangGraph 或其他 workflow 中使用审批节点和信息获取节点。

## Operational Boundaries

- 企业微信负责触达和审批 UI。
- GoHumanLoop WeWork 负责把 human loop 请求转换为企业微信审批流程。
- Agent workflow 负责根据审批状态继续、拒绝或请求补充信息。
- 生产环境需要关注公网回调、密钥保护、审批模板字段兼容和请求审计。 ^[inferred]

## Related

- [[entities/gohumanloop-wework]] — 被部署的示例服务。
- [[skills/langgraph-human-loop-integration]] — Agent 侧消费审批结果的示例。
- [[synthesis/ai-agent-production-loop]] — 企业微信审批是 Loop 中的人类接管点。

## Open Questions

- 文章没有完整展开失败重试、回调幂等、多审批人和审批撤回的处理策略。 ^[ambiguous]

## Sources

- [[references/published-article-batch-2026-06]] — 企业微信部署与 LangGraph 对接文章。
