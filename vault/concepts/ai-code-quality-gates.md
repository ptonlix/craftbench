---
title: AI Code Quality Gates
category: concepts
tags: [ai, software-engineering, code-quality, testing]
aliases: [AI 代码质量门禁, 从逐行审查到质量关卡]
relationships:
  - target: "[[concepts/agent-loop-engineering]]"
    type: implements
  - target: "[[synthesis/ai-agent-production-loop]]"
    type: uses
  - target: "[[concepts/agent-goal-boundary-security]]"
    type: related_to
sources:
  - /Users/atlas/WorkStation/craftbench/workbench/articles/published/2026-07-24-social-short-post-ai-code-review.md
summary: AI 生成代码的审查重点从逐行阅读上移到测试、变异测试、架构指标和分工明确的 Agent 流水线。
provenance:
  extracted: 0.78
  inferred: 0.22
  ambiguous: 0.0
base_confidence: 0.32
lifecycle: draft
lifecycle_changed: 2026-07-24
tier: supporting
created: 2026-07-24T23:20:12+08:00
updated: 2026-07-24T23:20:12+08:00
---

# AI Code Quality Gates

AI 生成代码的速度可能远高于人工阅读速度。若仍把逐行审查作为主要质量手段，生成阶段节省的时间会被检查阶段重新消耗。审查对象因此从每一行实现，上移到可自动执行的质量门槛。

## Quality Gates

- 单元测试与 Gherkin 验收测试。
- QA、覆盖率和代码质量指标。
- 变异测试：主动注入错误，验证测试是否真的能发现问题。
- 依赖结构、圈复杂度和模块大小等架构指标。
- 需求规格化、编码、重构、架构审查由不同 Agent 或阶段负责。

## Review Shift

- 人负责定义什么样的代码才准通过，而不是试图读完所有生成代码。
- 验证应独立于生成者，避免同一个 Agent 同时出题、答题和判卷。 ^[inferred]
- 质量纪律没有消失，而是从编码动作迁移到测试、边界、指标和交付门禁。

## Related

- [[concepts/agent-loop-engineering]] — 质量门禁把独立验证落实为可执行 Loop。
- [[synthesis/ai-agent-production-loop]] — Verification 应与代码生成阶段分离。
- [[concepts/agent-goal-boundary-security]] — 两者都通过系统边界约束强能力 Agent。

## Open Questions

- 哪些架构指标最适合成为自动阻断条件，哪些只能作为人工审查信号？
- 当测试本身也由 AI 生成时，如何避免同源盲区？

## Sources

- 《AI 时代，代码审查的对象变了》（2026-07-24）。
