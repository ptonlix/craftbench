---
title: Prompt Context Harness Engineering
category: concepts
tags: [ai-agent, prompt, context, harness]
aliases: [Prompt Engineering, Context Engineering, Harness Engineering]
relationships:
  - target: "[[concepts/agent-loop-engineering]]"
    type: related_to
  - target: "[[synthesis/ai-agent-production-loop]]"
    type: related_to
  - target: "[[concepts/human-in-the-loop]]"
    type: uses
sources:
  - workbench/articles/published/2026-06-20-prompt-context-harness/index.md
  - workbench/articles/published/2026-06-12-agent-loop-engineering/index.md
  - /Users/atlas/WorkStation/craftbench/workbench/articles/published/2026-08-03-social-short-post-codex-context-compaction.md
summary: Prompt、Context、Harness 分别决定任务表达、信息质量和可靠执行；长任务还需依据主线完整性与验收信号选择压缩或 Handoff。
provenance:
  extracted: 0.8
  inferred: 0.2
  ambiguous: 0.0
base_confidence: 0.61
lifecycle: draft
lifecycle_changed: 2026-07-08
tier: core
created: 2026-07-08T08:33:23Z
updated: 2026-08-09T12:27:06+08:00
---

# Prompt Context Harness Engineering

Prompt、Context、Harness 是构建 Agent 应用的三层工程结构。Prompt 决定模型这次要做什么，Context 决定模型此刻知道什么，Harness 决定模型如何可靠地做并持续变好。

## Prompt Engineering

Prompt 是指令层，负责角色、目标、流程、约束、输出格式和自检方式。它解决单次调用的表达质量问题，让模型更容易听懂任务边界。

## Context Engineering

Context 是信息层，负责检索、筛选、压缩、排序和去噪。它不是把资料塞满窗口，而是把“刚好需要的情报”放到模型面前，减少幻觉和错误判断。

## Harness Engineering

Harness 是系统层，包含 Agent Loop、工具调用、权限控制、日志追踪、错误恢复、Guardrails、测试、评估、版本管理、成本控制、部署和监控。它决定 Agent 是 demo 还是生产系统。

## Common Failure Mode

很多 Agent 不稳定并不是模型不够强，而是三层中缺了一层：只有 prompt 没有 context，模型会猜；只有 prompt 和 context 没有 harness，行为不可验证、不可追踪、不可恢复。

## Long-Context Operations

- 上下文窗口占用高不是自动切换 Session 的充分条件；只要任务主线、当前状态和最新目标仍清楚，压缩后通常可以继续执行。
- `/compact` 应在信息确实需要收敛时使用，过于频繁的压缩可能损失任务细节，也会降低缓存复用价值。
- Handoff 适合任务关系较弱、需要更干净上下文，或跨 Agent 接力的场景。
- Harness 应让 Agent 能依据目标、边界和验收方法判断是否完成，而不是把上下文百分比当作唯一控制信号。

## Related

- [[concepts/agent-loop-engineering]] — Loop 把三层结构组织成持续运行节奏。
- [[concepts/human-in-the-loop]] — Harness 中的关键控制点。
- [[synthesis/ai-agent-production-loop]] — 三层结构在生产系统中的综合落点。
- [[references/published-social-posts-2026-08-03-to-06]] — Codex 上下文压缩、Handoff 与验收标准的实践来源。

## Open Questions

- Context 与 Harness 的边界在真实产品中常会重叠，例如评估系统既影响检索策略，也影响执行闭环。 ^[inferred]

## Sources

- [[references/published-article-batch-2026-06]] — Prompt/Context/Harness 全景文章和 Loop Engineering 文章。
