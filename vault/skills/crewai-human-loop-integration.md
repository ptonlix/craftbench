---
title: CrewAI Human Loop Integration
category: skills
tags: [crewai, ai-agent, human-in-the-loop, python]
aliases: [CrewAI HITL Integration, GoHumanLoop CrewAI]
relationships:
  - target: "[[entities/gohumanloop]]"
    type: uses
  - target: "[[concepts/human-in-the-loop]]"
    type: implements
sources:
  - workbench/articles/published/2026-06-02-gohumanloop-crewai/index.md
summary: 在 CrewAI 中，可用 GoHumanLoop provider 和 manager 将关键工具调用包装为邮件审批点。
provenance:
  extracted: 0.82
  inferred: 0.18
  ambiguous: 0.0
base_confidence: 0.44
lifecycle: draft
lifecycle_changed: 2026-07-08
tier: supporting
created: 2026-07-08T08:33:23Z
updated: 2026-07-08T08:33:23Z
---

# CrewAI Human Loop Integration

CrewAI 与 GoHumanLoop 的集成思路，是在 Agent 工具调用前插入人工审批。文章示例使用邮件 provider，把审批请求发送给人类，再根据审批结果决定是否执行工具。

## Pattern

1. 配置 LLM、CrewAI agent、task 和 tool。
2. 创建 `EmailProvider`，配置 SMTP、发件人、授权信息和审批接收人。
3. 创建 `DefaultHumanLoopManager` 管理 provider。
4. 在敏感工具调用前发起审批请求。
5. 如果审批通过，继续执行工具；如果拒绝或超时，则取消操作。

## Why It Matters

CrewAI 原生流程更关注角色、任务和工具协作，但企业审批常常需要外部人类确认。GoHumanLoop 将审批通道抽象为 provider，使审批逻辑不必散落在每个 CrewAI tool 中。 ^[inferred]

## Related

- [[entities/gohumanloop]] — 提供邮件 provider 和 human loop 管理。
- [[concepts/human-in-the-loop]] — CrewAI 中的审批控制模式。
- [[skills/langgraph-human-loop-integration]] — 另一个 Agent 框架中的相同理念。

## Open Questions

- 邮件审批的时延、重复点击、审批链接安全性和审计留痕需要在生产使用中补充设计。 ^[inferred]

## Sources

- [[references/published-article-batch-2026-06]] — CrewAI 实践文章。
