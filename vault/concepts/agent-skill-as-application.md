---
title: Agent Skill As Application
category: concepts
tags: [agent-skill, software, automation, product]
aliases: [Skill as App, Agent-native Application]
relationships:
  - target: "[[concepts/agent-loop-engineering]]"
    type: related_to
  - target: "[[concepts/prompt-context-harness-engineering]]"
    type: uses
  - target: "[[projects/beeweave/concepts/agent-skill-install-model]]"
    type: related_to
sources:
  - workbench/articles/published/2026-06-02-agent-cleaner-skill/index.md
summary: Agent skill 可以把明确、规则可定义的工具软件能力封装成轻量应用，让 Agent 直接执行分析、报告和受控操作。
provenance:
  extracted: 0.62
  inferred: 0.38
  ambiguous: 0.0
base_confidence: 0.44
lifecycle: draft
lifecycle_changed: 2026-07-08
tier: supporting
created: 2026-07-08T08:33:23Z
updated: 2026-07-08T08:33:23Z
---

# Agent Skill As Application

Agent skill 可以把传统工具软件中规则明确、边界清晰的能力变成轻量应用。文章中的 Mac/Windows 存储清理 skill 展示了这种模式：Agent 先只读扫描，再生成可交互报告，最后由用户确认后执行清理动作。

## Key Ideas

- 很多工具型软件本质是 UI 加一组系统扫描、规则判断和文件操作；Agent skill 可以直接理解环境并生成定制化方案。 ^[inferred]
- 存储清理 skill 的关键不是“让 Agent 随便删文件”，而是只读扫描、透明解释、风险分级和用户二次确认。
- 报告按绿灯、黄灯、红灯分级：绿灯可自动清理，黄灯需要用户查看，红灯应跳过。
- 交互式 HTML 报告让用户看到路径、大小、类型、说明、影响和清理命令，而不是只看到一个抽象垃圾大小。
- Agent skill 相比固定规则软件的优势，是能根据用户环境和自然语言需求定制分析。

## Design Requirements

- 扫描阶段必须只读。
- 删除动作必须由用户显式点击并二次确认。
- 高风险路径应默认不提供直接删除按钮。
- 每个建议都应解释“是什么、为什么可清、删了有什么影响”。
- 可逆操作优先，例如移动到废纸篓而不是立即删除。

## Related

- [[concepts/prompt-context-harness-engineering]] — 该 skill 同时需要 prompt、系统上下文和执行 harness。
- [[concepts/agent-loop-engineering]] — skill 可以成为个人工作 loop 中可复用的工具单元。
- [[projects/beeweave/concepts/agent-skill-install-model]] — BeeWeave 的 skill 安装策略与该理念一致。

## Open Questions

- Agent skill 是否会替代一部分单功能工具软件，取决于安全、权限、确认体验和用户信任，而不只是模型能力。 ^[inferred]

## Sources

- [[references/published-article-batch-2026-06]] — Agent 清理软件 skill 文章。
