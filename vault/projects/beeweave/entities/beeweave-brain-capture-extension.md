---
title: BeeWeave Brain Capture Extension
category: entities
tags: [beeweave, browser-extension, capture, workbench]
aliases: [Brain Capture, BeeWeave Capture Extension]
relationships:
  - target: "[[projects/beeweave/concepts/workbench-vault-architecture]]"
    type: uses
  - target: "[[projects/beeweave/beeweave]]"
    type: related_to
  - target: "[[projects/beeweave/skills/beeweave-cli-operations]]"
    type: related_to
sources: [../beeweave]
summary: BeeWeave Brain Capture 是零构建 Chrome 扩展，可把当前网页 URL、可读文本或选中文本保存到 workbench inbox。
provenance:
  extracted: 0.9
  inferred: 0.1
  ambiguous: 0.0
base_confidence: 0.63
lifecycle: draft
lifecycle_changed: 2026-07-08
tier: supporting
created: 2026-07-08T08:13:32Z
updated: 2026-07-08T08:13:32Z
---

# BeeWeave Brain Capture Extension

BeeWeave Brain Capture 是 `extensions/brain-capture/` 下的零构建 Chrome 扩展，用于把当前页面 URL、标题、可读文本、用户备注或选中文本保存为 markdown capture。

## Key Ideas

- 扩展安装方式是 Chrome Developer mode 的 “Load unpacked”，目标目录为 `extensions/brain-capture`。
- 浏览器不能直接读取本地 BeeWeave config，因此用户需要在 popup 中选择一次 `workbench/inbox/web/` 作为写入目录。
- 捕获文件命名类似 `2026-06-17-page-title.md`，包含 YAML frontmatter、标题、URL、创建时间、capture metadata 和页面文本。
- 捕获内容上限为 140,000 字符，以保持后续 ingest 可处理。
- 捕获进入 inbox 后，应通过 `beeweave-ingest workbench/inbox` 提升为 vault 中的稳定知识页。

## Related

- [[projects/beeweave/concepts/workbench-vault-architecture]] — 扩展写入 workbench inbox，而不是直接写 vault。
- [[projects/beeweave/beeweave]] — 扩展是 BeeWeave 收集材料阶段的入口之一。
- [[concepts/agent-loop-engineering]] — 浏览器捕获服务于后续创作和知识沉淀循环。

## Open Questions

- 扩展当前依赖用户手动授权目标目录；未来是否需要本地 helper bridge 来减少配置摩擦仍未确定。 ^[inferred]

## Sources

- [[projects/beeweave/references/beeweave-source-repository]] — `extensions/brain-capture/README.md` 和 README 可选功能说明。
