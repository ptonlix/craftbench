---
title: BeeWeave Development Workflow
category: skills
tags: [beeweave, development, openspec, testing]
aliases: [BeeWeave Dev Workflow]
relationships:
  - target: "[[projects/beeweave/beeweave]]"
    type: related_to
  - target: "[[projects/beeweave/skills/beeweave-cli-operations]]"
    type: uses
  - target: "[[projects/beeweave/concepts/agent-skill-install-model]]"
    type: related_to
sources: [../beeweave]
summary: 修改 BeeWeave 本身时，应遵循 OpenSpec、集中 UI helper、非交互兼容、focused checks 和完整测试的工作流。
provenance:
  extracted: 0.74
  inferred: 0.26
  ambiguous: 0.0
base_confidence: 0.63
lifecycle: draft
lifecycle_changed: 2026-07-08
tier: supporting
created: 2026-07-08T08:13:32Z
updated: 2026-07-08T08:13:32Z
---

# BeeWeave Development Workflow

BeeWeave 源码开发围绕 Python CLI、skills、bootstrap、docs、OpenSpec 和测试展开。变更应保持作用域清晰，优先沿用现有 CLI/setup/skill 模式。

## Key Practices

- 行为或工作流变更先进入 `openspec/changes/<change>/`，包含 proposal、design、tasks 和 capability spec。
- 修改 CLI 交互时，共享展示逻辑应放在 `beeweave/ui.py`，避免在命令 handler 中直接添加分散的 ANSI、prompt、banner 或 summary rendering。
- InquirerPy 必须保持可选；非交互和缺少 InquirerPy 的 fallback 要 deterministic、scriptable、prompt-free。
- 不给 `graph-query`、`graph-analyse`、`batch-plan`、`cache-*`、`ast-extract`、`list` 等机器可读命令添加 banner 或 panel。
- 根目录 `AGENTS.md` 是仓库开发上下文，`bootstrap/AGENTS.md` 是用户项目执行上下文；两者职责不能混淆。
- 运行时 `vault/` 与 `workbench/` 是用户数据，由 setup 生成，不应作为源码 mirror 提交。

## Verification

- 常规验证：`uv run pytest`、`uv run bwe setup --help`、`uv run bwe info`。
- OpenSpec 变更验证：`openspec validate <change-name> --strict`。
- 文档站点变更验证：`uv run --group docs mkdocs build --strict`。

## Related

- [[projects/beeweave/skills/beeweave-cli-operations]] — CLI 命令的行为面。
- [[projects/beeweave/concepts/agent-skill-install-model]] — skill 和 bootstrap 修改的安装语义。
- [[projects/beeweave/references/beeweave-source-repository]] — 本工作流的源码依据。

## Open Questions

- 对技能内容变更，是否需要更细粒度的自动 lint 或 schema 验证仍是后续改进空间。 ^[inferred]

## Sources

- [[projects/beeweave/references/beeweave-source-repository]] — `AGENTS.md`、`docs/development.md`、OpenSpec tasks 和项目记忆。
