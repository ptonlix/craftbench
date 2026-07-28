---
title: Agent Loop Engineering
category: concepts
tags: [ai-agent, engineering, workflow, automation]
aliases: [Loop Engineering, Agentic Loop]
relationships:
  - target: "[[concepts/prompt-context-harness-engineering]]"
    type: extends
  - target: "[[concepts/human-in-the-loop]]"
    type: uses
  - target: "[[synthesis/ai-agent-production-loop]]"
    type: related_to
sources:
  - workbench/articles/published/2026-06-12-agent-loop-engineering/index.md
  - workbench/articles/published/2026-06-20-prompt-context-harness/index.md
  - /Users/atlas/WorkStation/craftbench/workbench/articles/published/2026-07-22-social-short-post-openai-huggingface-breach/2026-07-22-social-short-post-openai-huggingface-breach.md
  - /Users/atlas/WorkStation/craftbench/workbench/articles/published/2026-07-24-social-short-post-ai-code-review.md
summary: Agent Loop Engineering 让 AI 持续工作，并用路径边界、独立质量门禁、记忆和人工接管约束强自主能力。
provenance:
  extracted: 0.72
  inferred: 0.28
  ambiguous: 0.0
base_confidence: 0.82
lifecycle: draft
lifecycle_changed: 2026-07-08
tier: core
created: 2026-07-08T08:33:23Z
updated: 2026-07-24T23:20:12+08:00
---

# Agent Loop Engineering

Agent Loop Engineering 是把 AI 协作从“会提问”推进到“会运转”的系统设计能力。它关注任务入口、执行环境、上下文、工具、权限、验证、记忆和人类接管点，而不只是单次 prompt 的表达。

## Key Ideas

- Prompt 仍然重要，但它只是一次行动的意图表达；Loop 让多次行动有节奏、有状态、有反馈。
- 一个可靠 loop 应有任务入口，例如 GitHub Issue、CI 失败、监控告警、Markdown task 或业务请求。
- 每个任务最好有隔离执行环境，例如独立 branch、worktree、sandbox 或明确的权限边界。
- Agent 启动时应读取项目规范、业务规则、最近变更、相关测试和历史坑位。
- 验证应独立于生成环节：测试、静态扫描、代码审查、人工审批最好作为不同环节存在。
- Loop 越顺，人越不能认知投降；绿灯不等于理解，自动化不能替代最终判断。
- 目标约束还应规定 Agent 永远不能走的路径，而不只是告诉它终点。
- 当生成速度超过人工阅读速度，验证应上移为测试、变异测试、架构指标和分阶段质量门禁。

## Loop Components

- 入口：任务从哪里来。
- 上下文：Agent 启动时知道什么。
- 工具：Agent 能调用什么外部系统。
- 权限边界：哪些动作允许自动执行，哪些必须审批。
- 验证：结果如何被独立检查。
- 记忆：经验如何沉淀进 AGENTS、skills、wiki 或 memory。
- 接管点：人类在哪里保留判断权。

## Related

- [[concepts/prompt-context-harness-engineering]] — Prompt、Context、Harness 是 Loop 内部的基础零件。
- [[concepts/human-in-the-loop]] — Loop 的刹车和责任边界。
- [[synthesis/ai-agent-production-loop]] — 生产级 Agent Loop 的综合模型。
- [[projects/beeweave/beeweave]] — BeeWeave 把外部记忆和工作流沉淀为可复用 loop。
- [[concepts/agent-goal-boundary-security]] — 把禁止路径、权限、出网和停止条件纳入 Loop。
- [[concepts/ai-code-quality-gates]] — 用独立、可执行的质量关卡替代不可扩展的逐行审查。

## Open Questions

- Loop 的成熟度应如何度量：任务吞吐、失败恢复、人工介入率、验证可靠性或知识复用率都可能是指标。 ^[inferred]

## Sources

- [[references/published-article-batch-2026-06]] — Loop Engineering 与 Prompt/Context/Harness 文章。
