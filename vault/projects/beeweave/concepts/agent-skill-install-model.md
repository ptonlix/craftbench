---
title: Agent Skill Install Model
category: concepts
tags: [beeweave, skills, agents, bootstrap]
aliases: [BeeWeave Skill Install Policy]
relationships:
  - target: "[[projects/beeweave/beeweave]]"
    type: related_to
  - target: "[[concepts/agent-skill-as-application]]"
    type: extends
  - target: "[[projects/beeweave/skills/beeweave-cli-operations]]"
    type: related_to
sources: [../beeweave, workbench/articles/published/2026-07-08-article-beeweave-creation-workbench.md]
summary: BeeWeave 将少量便携技能全局安装，把完整技能集和 bootstrap 模板安装到选定项目，避免污染无关工作区。
provenance:
  extracted: 0.78
  inferred: 0.22
  ambiguous: 0.0
base_confidence: 0.76
lifecycle: draft
lifecycle_changed: 2026-07-08
tier: supporting
created: 2026-07-08T08:13:32Z
updated: 2026-07-08T09:38:20Z
---

# Agent Skill Install Model

BeeWeave 的 skill 安装策略分为默认全局、可选高级全局和项目本地完整安装三层。默认全局集合保持小而便携，项目本地安装则提供完整 BeeWeave 工作台能力。

## Key Ideas

- 默认全局技能包括 `beeweave-update`、`beeweave-query` 和 `beeweave-ingest`，用于跨项目同步、查询和资料 ingest。
- 可选高级全局技能包括 capture、context pack、digest、status、memory bridge 等，需要用户显式选择。
- 项目本地安装为选定 Agent 写入完整 skill 集和 bootstrap 文件，适合 BeeWeave 工作区或需要完整工作流的项目。
- `bwe setup` 支持 Claude、Codex、Cursor、Gemini、Kiro、Hermes、OpenClaw、Pi、Copilot CLI、Trae 等多个 Agent target。
- 用户项目 context 模板来自 `bootstrap/AGENTS.md`，并生成 `AGENTS.md`、`CLAUDE.md`、`GEMINI.md`、`HERMES.md` 等入口；BeeWeave 仓库根目录的 `AGENTS.md` 只服务源码开发。
- 这个安装模型服务多 Agent 共享上下文：不同 Agent 可以通过克制的默认技能进入同一个知识循环，而完整能力只安装到明确选择的工作区。

## Design Rationale

这种分层避免把完整 BeeWeave 工作流强加到每个项目，同时保留跨项目查询和同步的低摩擦入口。它把 skill 当作可移植应用能力，而不是单个聊天会话里的临时提示词。 ^[inferred]

发布文章进一步强调了这个边界的产品理由：Agent skill 不应变成到处污染项目的全局插件，完整能力应该留给真正的 BeeWeave 工作区或用户明确选择的项目。

## Related

- [[concepts/agent-skill-as-application]] — skill 可以像轻量应用一样封装规则、输入和操作流程。
- [[projects/beeweave/skills/beeweave-cli-operations]] — `bwe setup --agents` 和 `--global-extra` 实现安装策略。
- [[projects/beeweave/references/beeweave-creation-workbench-article]] — 从多 Agent 使用体验解释默认技能克制的必要性。
- [[projects/beeweave/skills/beeweave-development-workflow]] — 修改 skill 或 bootstrap 时应配套测试和文档扫描。

## Open Questions

- 高级全局技能的默认推荐集合可能需要根据用户常用 Agent 和 vault 规模继续调整。 ^[inferred]

## Sources

- [[projects/beeweave/references/beeweave-source-repository]] — `README.md`、`docs/skills.md`、`docs/agents.md` 和 `bootstrap/`。
- [[projects/beeweave/references/beeweave-creation-workbench-article]] — 已发布文章对默认全局技能、可选高级技能和多 Agent 上下文共享的解释。
