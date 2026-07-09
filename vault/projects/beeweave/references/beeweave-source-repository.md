---
title: BeeWeave Source Repository
category: references
tags: [beeweave, source-repository, documentation, openspec]
aliases: [BeeWeave Repo]
relationships:
  - target: "[[projects/beeweave/beeweave]]"
    type: related_to
  - target: "[[projects/beeweave/concepts/workbench-vault-architecture]]"
    type: related_to
  - target: "[[projects/beeweave/skills/beeweave-development-workflow]]"
    type: related_to
sources: [../beeweave]
summary: 本页记录 BeeWeave 源码仓库作为本次 ingest 来源的范围：README、docs、bootstrap、skills、OpenSpec、CLI、测试和扩展。
provenance:
  extracted: 0.84
  inferred: 0.16
  ambiguous: 0.0
base_confidence: 0.63
lifecycle: draft
lifecycle_changed: 2026-07-08
tier: supporting
created: 2026-07-08T08:13:32Z
updated: 2026-07-08T08:13:32Z
---

# BeeWeave Source Repository

本次同步来源是 BeeWeave 源码仓库 `../beeweave`。它包含 Python CLI、Agent skills、bootstrap 模板、文档站点、浏览器扩展、测试和 OpenSpec 变更记录。

## Source Scope

- 阅读的高信号文档包括 `README.md`、`docs/architecture.md`、`docs/cli.md`、`docs/skills.md`、`docs/flywheel.md`、`docs/agents.md`、`docs/development.md`、`docs/quickstart.md` 和 `extensions/brain-capture/README.md`。
- 结构抽取使用 `bwe ast-extract`，覆盖 shell、Python 和 JavaScript 文件，识别 CLI、UI、profile、uninstall、graph、cache、batch 和 extension 相关代码结构。
- `bwe batch-plan` 显示仓库内还有 `site/` 构建产物、`tmp/` 临时数据和图片资产；本次项目知识同步不把这些生成/临时内容作为独立知识页。
- OpenSpec 记录了文档站点、CLI 交互体验、workbench/vault 布局、项目重命名和 agent context/bootstrap 拆分等已完成或活跃变更。

## Distilled Pages

- [[projects/beeweave/beeweave]]
- [[projects/beeweave/concepts/workbench-vault-architecture]]
- [[projects/beeweave/concepts/agent-skill-install-model]]
- [[projects/beeweave/skills/beeweave-cli-operations]]
- [[projects/beeweave/skills/beeweave-development-workflow]]
- [[projects/beeweave/entities/beeweave-brain-capture-extension]]

## Notes

本次同步以项目级知识为目标，而不是完整源码逐文件文档化；函数级事实主要留给 AST 和源码本身。 ^[inferred]

## Sources

- `../beeweave` — BeeWeave 源码仓库。
