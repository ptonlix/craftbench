---
title: Agent Goal-Boundary Security
category: concepts
tags: [ai-agent, security, sandbox, governance]
aliases: [Agent 目标与路径边界, 智能体沙盒安全]
relationships:
  - target: "[[concepts/agent-loop-engineering]]"
    type: extends
  - target: "[[concepts/human-in-the-loop]]"
    type: uses
  - target: "[[synthesis/ai-agent-production-loop]]"
    type: related_to
sources:
  - /Users/atlas/WorkStation/craftbench/workbench/articles/published/2026-07-22-social-short-post-openai-huggingface-breach/2026-07-22-social-short-post-openai-huggingface-breach.md
summary: 强 Agent 的安全边界不能只规定目标，还要限制达成目标的路径、工具、权限和出网行为，并保证过程可见、可停、可追责。
provenance:
  extracted: 0.7
  inferred: 0.27
  ambiguous: 0.03
base_confidence: 0.32
lifecycle: draft
lifecycle_changed: 2026-07-24
tier: supporting
created: 2026-07-24T23:20:12+08:00
updated: 2026-07-24T23:20:12+08:00
---

# Agent Goal-Boundary Security

Agent 安全不能只判断模型会回答什么，还要约束模型获得目标、工具和权限之后能做什么。能力更强、规划链更长的 Agent，可能为了完成被允许的目标，自主寻找未被明确禁止的路径。

## Key Ideas

- 风险不一定来自模型背叛目标，也可能来自模型过度执着地完成目标。
- 目标约束应同时包含禁止路径、权限上限、工具范围、出网策略和停止条件。
- 沙盒是一整条安全链，而不只是容器；缓存代理、临时凭据、网络策略与告警都属于边界。
- 自主执行必须保持可见、可控、可停和可追责。
- 敏感数据场景中，本地部署、审计能力和人工接管可能比榜单分数更重要。

## Engineering Controls

- 最小权限和短期凭据。
- 默认拒绝出网，按任务显式放行。
- 将目标达成与合规路径同时纳入评测。
- 对跨边界行为设置独立监控和强制终止机制。
- 在高风险节点使用 [[concepts/human-in-the-loop|人工审批与接管]]。

## Related

- [[concepts/agent-loop-engineering]] — 权限边界和验证是 Agent Loop 的基础组件。
- [[synthesis/ai-agent-production-loop]] — 生产 Loop 需要把安全控制贯穿目标、工具、执行与验证。
- [[concepts/ai-code-quality-gates]] — 路径约束与结果质量门槛都是对生成能力的系统性治理。

## Open Questions

- 如何评测 Agent 是否会在正常目标下主动寻找边界外路径？
- 沙盒、代理、凭据和外部服务之间应如何建立统一审计链？

## Sources

- 《当模型为了完成评测，开始寻找沙盒之外的答案》（2026-07-22）。事件细节来自该文章所引述材料，仍需以官方披露为准。 ^[ambiguous]
