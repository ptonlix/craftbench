---
title: LangGraph Human Loop Integration
category: skills
tags: [langgraph, ai-agent, human-in-the-loop, python]
aliases: [LangGraph HITL Integration, GoHumanLoop LangGraph]
relationships:
  - target: "[[entities/gohumanloop]]"
    type: uses
  - target: "[[concepts/human-in-the-loop]]"
    type: implements
  - target: "[[entities/gohumanloop-wework]]"
    type: related_to
sources:
  - workbench/articles/published/2026-06-01-gohumanloop-langgraph/index.md
  - workbench/articles/published/2026-06-05-gohumanloop-wework-langgraph/index.md
summary: 在 LangGraph 中，可用 GoHumanLoop adapter 将审批、信息获取和反馈收集包装为节点或装饰器。
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

# LangGraph Human Loop Integration

LangGraph 与 GoHumanLoop 的集成方式，是把人工审批、补充信息和反馈收集显式放进图节点或敏感操作装饰器中，让 workflow 能在关键位置暂停并等待人类决策。

## Pattern

1. 定义 LangGraph state，例如 `messages` 和 `next`。
2. 创建 `DefaultHumanLoopManager`，并配置终端 provider 或 API provider。
3. 创建 LangGraph adapter。
4. 在需要人工补充输入的节点上使用信息请求装饰器。
5. 在敏感操作函数上使用审批装饰器，并把审批结果传入真实执行函数。
6. 根据 `HumanLoopStatus.APPROVED`、`REJECTED` 等状态决定图的下一步。

## Example Scenarios

- 金融建议和交易：Agent 先生成建议，人类审核后才进入转账或投资操作。
- 企业微信审批：LangGraph 节点通过 GoHumanLoop API provider 发起审批，企业微信审批完成后回到 workflow。
- 反馈闭环：流程结束前请求用户反馈，并把反馈写回 state。

## Practical Notes

- 把“审批”放在执行动作之前，而不是动作之后补日志。
- 把审批结果作为结构化参数传给工具函数，避免 Agent 把自然语言回复误读为授权。
- 对接企业微信时，前置条件是 GoHumanLoop WeWork 服务和企业微信模板已经部署完成。

## Related

- [[entities/gohumanloop]] — 集成所依赖的库。
- [[entities/gohumanloop-wework]] — API provider 的企业微信实现。
- [[concepts/human-in-the-loop]] — 该集成实现的控制机制。
- [[synthesis/ai-agent-production-loop]] — LangGraph human loop 是生产 loop 的具体形态之一。

## Open Questions

- 多节点、多审批人的 LangGraph 路由策略在文章中没有展开，需要进一步设计状态机。 ^[inferred]

## Sources

- [[references/published-article-batch-2026-06]] — LangGraph 与企业微信实践文章。
