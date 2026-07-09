---
title: BeeWeave CLI Operations
category: skills
tags: [beeweave, cli, setup, operations]
aliases: [bwe CLI Operations]
relationships:
  - target: "[[projects/beeweave/beeweave]]"
    type: related_to
  - target: "[[projects/beeweave/concepts/workbench-vault-architecture]]"
    type: uses
  - target: "[[projects/beeweave/concepts/agent-skill-install-model]]"
    type: uses
sources: [../beeweave]
summary: BeeWeave 的 `bwe` CLI 负责 setup、profile、uninstall、info、技能列表、graph/cache/batch/AST 等本地辅助操作。
provenance:
  extracted: 0.88
  inferred: 0.12
  ambiguous: 0.0
base_confidence: 0.63
lifecycle: draft
lifecycle_changed: 2026-07-08
tier: supporting
created: 2026-07-08T08:13:32Z
updated: 2026-07-08T08:13:32Z
---

# BeeWeave CLI Operations

BeeWeave 暴露 `bwe` 命令，用于安装 Agent skills、初始化运行时目录、管理 profile、查看安装信息，以及给 ingest/query 提供本地 helper。

## Core Commands

- `bwe setup` 在当前 workspace 创建 `vault/` 和 `workbench/`，写入 BeeWeave config，并为选定 Agent 安装 skills 和 bootstrap。
- `bwe profile` 管理命名 profile；`bwe profile set-default <name>` 会显式把命名配置复制为默认配置，并备份旧默认配置。
- `bwe uninstall` 移除 BeeWeave 管理的 skills、bootstrap 文件和配置，但保留用户的 `vault/` 与 `workbench/` 内容。
- `bwe list` 列出随包分发的 skill。
- `bwe info` 展示版本、配置和安装路径。

## Knowledge Helpers

- `bwe graph-query` 和 `bwe graph-analyse` 查询或分析 vault wikilink 图。
- `bwe batch-plan` 为大目录 ingest 规划批次。
- `bwe cache-check`、`cache-update` 和 `cache-hash` 维护 `.manifest.json` 的增量同步基础。
- `bwe ast-extract` 从代码中抽取文件、函数、类、导入和调用关系，减少 LLM 对源码文件的直接读取。

## Operational Notes

- `bwe setup --profile NAME` 创建或更新命名配置，但不会激活该 profile；单次 Agent 请求可用 `@name` 路由。
- 非交互和缺少 InquirerPy 的环境必须保持确定性、可脚本化和无提示阻塞。
- 面向人类的 setup/info/uninstall 输出走共享 UI helper；机器可读命令保持 JSON 或纯文本输出。

## Related

- [[projects/beeweave/concepts/workbench-vault-architecture]] — setup 创建的运行时边界。
- [[projects/beeweave/concepts/agent-skill-install-model]] — setup 安装策略。
- [[projects/beeweave/skills/beeweave-development-workflow]] — 修改 CLI 时的验证流程。

## Open Questions

- 随着 graph/cache/helper 命令增多，哪些输出应保持机器可读、哪些可使用 summary panel，需要继续在 CLI 约束中明确。 ^[inferred]

## Sources

- [[projects/beeweave/references/beeweave-source-repository]] — `docs/cli.md`、`README.md`、`beeweave/cli.py` AST 结构和项目记忆。
