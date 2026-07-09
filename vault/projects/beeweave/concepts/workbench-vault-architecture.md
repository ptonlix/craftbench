---
title: Workbench Vault Architecture
category: concepts
tags: [beeweave, architecture, workbench, vault]
aliases: [BeeWeave Runtime Layout, Workbench/Vault Boundary]
relationships:
  - target: "[[projects/beeweave/beeweave]]"
    type: related_to
  - target: "[[concepts/agent-loop-engineering]]"
    type: extends
  - target: "[[synthesis/ai-agent-production-loop]]"
    type: related_to
sources: [../beeweave, workbench/articles/published/2026-07-08-article-beeweave-creation-workbench.md]
summary: BeeWeave 用 workbench 保存原始输入、草稿和发布稿，用 vault 保存稳定知识页，并以发布后 ingest 形成创作复用循环。
provenance:
  extracted: 0.84
  inferred: 0.16
  ambiguous: 0.0
base_confidence: 0.76
lifecycle: draft
lifecycle_changed: 2026-07-08
tier: supporting
created: 2026-07-08T08:13:32Z
updated: 2026-07-08T09:38:20Z
---

# Workbench Vault Architecture

BeeWeave 的核心边界是“原始工作区”和“编译后知识库”：`workbench/` 承接粗糙输入、捕获、资料库和文章草稿，`vault/` 承接可搜索、可链接、可复用的稳定 markdown 知识页。

## Key Ideas

- `workbench/inbox/captures/` 保存 Agent 快速捕获和会话发现，`workbench/inbox/web/` 保存浏览器剪藏。
- 已处理的 inbox 输入移动到 `workbench/inbox/archived/`，被拒绝或需人工调整的候选内容进入 `workbench/inbox/rejected/`。
- `workbench/articles/drafts/` 和 `workbench/articles/published/` 支撑从草稿到已发布输出再到 vault ingest 的创作路径。
- `vault/` 保存 concepts、entities、skills、references、synthesis 和 projects 等稳定页面，并维护 `.manifest.json`、`index.md`、`log.md` 与 `hot.md`。
- BeeWeave 源码仓库不应提交运行时 `vault/` 或 `workbench/` 实例目录；这些目录由用户在实际工作区通过 `bwe setup` 创建。
- 文章级工作流允许 workbench 保持粗糙和开放，同时要求进入 vault 的内容是经过发布或确认后的稳定判断。

## Why It Matters

这个边界让 BeeWeave 更接近“知识编译器”：原始输入保留在 workbench，稳定判断进入 vault，Agent 查询时优先读已编译页面而不是反复重读原始材料。它也减少了源码仓库和用户数据之间的混淆。

在写作场景里，这个分层避免一次创作结束后链接、讨论、确认观点和错误方向全部蒸发；发布稿被 ingest 后，下一次相关选题可以直接查询 vault 中的稳定上下文。

## Related

- [[projects/beeweave/beeweave]] — BeeWeave 项目概览。
- [[projects/beeweave/skills/beeweave-cli-operations]] — `bwe setup` 创建运行时目录。
- [[projects/beeweave/references/beeweave-creation-workbench-article]] — 用写作场景解释 workbench 到 vault 的发布回流。
- [[concepts/agent-loop-engineering]] — workbench/vault 边界服务于持续循环，而不是一次性归档。

## Open Questions

- 对大型 vault，哪些页面应该被自动提升为 core tier，仍需要更成熟的 graph metrics 和人工确认。 ^[inferred]

## Sources

- [[projects/beeweave/references/beeweave-source-repository]] — `README.md`、`docs/architecture.md`、`docs/flywheel.md` 和相关 OpenSpec 变更。
- [[projects/beeweave/references/beeweave-creation-workbench-article]] — 已发布文章对粗糙输入、稳定知识和创作飞轮的解释。
