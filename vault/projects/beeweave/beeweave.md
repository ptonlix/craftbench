---
title: BeeWeave
category: project
tags: [beeweave, knowledge-workbench, agent, markdown]
aliases: [BeeWeave Project]
relationships:
  - target: "[[projects/beeweave/concepts/workbench-vault-architecture]]"
    type: implements
  - target: "[[projects/beeweave/concepts/agent-skill-install-model]]"
    type: implements
  - target: "[[concepts/agent-loop-engineering]]"
    type: extends
sources: [../beeweave, workbench/articles/published/2026-07-08-article-beeweave-creation-workbench.md]
source_path: ../beeweave
summary: BeeWeave 是面向 Agent 的知识工作台，把 workbench 原始材料、vault 稳定知识和 agent skills 连接成创作与知识复用飞轮。
provenance:
  extracted: 0.8
  inferred: 0.2
  ambiguous: 0.0
base_confidence: 0.76
lifecycle: draft
lifecycle_changed: 2026-07-08
tier: supporting
created: 2026-07-08T08:13:32Z
updated: 2026-07-08T09:38:20Z
---

# BeeWeave

BeeWeave 是一个 agent-native creation workbench，用于围绕创作过程建立数据飞轮：收集材料、用 Agent 创作、把高信号输出沉淀为持久知识，再把这些知识作为下一轮收集和创作的上下文。

## Key Concepts

- [[projects/beeweave/concepts/workbench-vault-architecture]] — 区分源码仓库、运行时 `workbench/` 和稳定知识 `vault/` 的边界。
- [[projects/beeweave/concepts/agent-skill-install-model]] — 解释默认全局技能、可选高级技能和项目本地完整技能集的安装策略。
- [[concepts/agent-loop-engineering]] — BeeWeave 把一次性对话扩展为可持续的收集、创作、沉淀、复用循环。
- [[concepts/prompt-context-harness-engineering]] — BeeWeave 的 skill、bootstrap 和 CLI 共同构成 Agent 可操作的上下文与执行系统。

## Source Layout

- `beeweave/` 提供 Python CLI 和本地 helper，包括 setup、profile、cache、batch、graph 和 AST 提取命令。
- `.skills/` 存放 Agent skill 源文件，分为 wiki 维护类和 workbench 创作类。
- `bootstrap/` 存放安装到用户项目的 Agent context、规则和工作流模板。
- `docs/` 和 `mkdocs.yml` 维护中英文 MkDocs 文档站点；`site/` 是构建产物，不作为源码维护。
- `extensions/brain-capture/` 提供浏览器捕获扩展，把网页内容保存到 `workbench/inbox/web/`。
- `openspec/` 记录行为和工作流变更的 proposal、design、tasks 与 spec。
- `tests/` 覆盖 CLI、setup 布局、缓存、批处理、图分析、AST 提取和文档约束。

## Operating Loop

BeeWeave 的运行时工作区由 `bwe setup` 创建：`workbench/` 用于 inbox、captures、web clippings、drafts、published articles 和 source library；`vault/` 用于概念、实体、技能、参考、综合和项目页。这个边界让原始输入保持可追溯，同时让稳定知识以 Obsidian markdown 和 wikilinks 形式复用。

文章发布工作流把这个边界延伸成创作飞轮：素材进入 workbench，写作 skill 生成草稿，发布稿进入 `workbench/articles/published/`，再由 ingest 把高信号观点沉淀回 vault。下一轮创作可通过 query、digest 或 context pack 重新取回稳定上下文，而不是让不同 Agent 每次重新理解项目背景。

## Related

- [[projects/beeweave/skills/beeweave-cli-operations]] — `bwe` CLI 的核心命令和辅助命令。
- [[projects/beeweave/skills/beeweave-development-workflow]] — 修改 BeeWeave 本身时的验证和 OpenSpec 工作流。
- [[projects/beeweave/entities/beeweave-brain-capture-extension]] — 浏览器捕获入口。
- [[projects/beeweave/references/beeweave-source-repository]] — 本次同步的源码仓库参考页。
- [[projects/beeweave/references/beeweave-creation-workbench-article]] — 用写作场景解释 BeeWeave 创作飞轮的已发布文章。

## Open Questions

- 哪些 BeeWeave skills 应继续保持全局默认，哪些应该只作为项目本地能力安装，仍需要随着真实使用数据迭代。 ^[inferred]

## Sources

- [[projects/beeweave/references/beeweave-source-repository]] — BeeWeave 源码仓库、README、docs、OpenSpec 和 AST 结构抽取。
- [[projects/beeweave/references/beeweave-creation-workbench-article]] — 已发布文章对创作飞轮、上下文复用和多 Agent 使用边界的叙述。
