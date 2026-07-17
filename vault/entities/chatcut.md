---
title: ChatCut
category: entities
tags: [chatcut, video-editing, ai-agent, pricing]
aliases: [ChatCut Plugin]
relationships:
  - target: "[[concepts/agent-skill-as-application]]"
    type: implements
  - target: "[[concepts/prompt-context-harness-engineering]]"
    type: related_to
sources: [/Users/atlas/WorkStation/craftbench/workbench/articles/published/2026-07-13-social-short-post-chatcut-pricing.md]
summary: ChatCut 是 Agent 驱动的视频编辑插件；基础编辑使用既有 Agent 额度，生成视频、音乐、图片或旁白可能另耗 credits。
provenance:
  extracted: 0.65
  inferred: 0.05
  ambiguous: 0.30
base_confidence: 0.37
lifecycle: draft
lifecycle_changed: 2026-07-17
tier: supporting
created: 2026-07-17T07:06:00Z
updated: 2026-07-17T07:06:00Z
---

# ChatCut

ChatCut 被描述为可由 Codex 等 Agent 操作的视频编辑插件。其成本需要区分“基础编辑消耗既有 Agent 额度”和“生成新素材消耗 ChatCut credits”。

## Pricing Model

- 剪辑、加字幕和调整时间线等基础编辑不单独收取插件费，但仍消耗 Codex 或其他 Agent 原有的订阅额度。
- 生成视频、音乐、图片和旁白会使用 ChatCut 自有 credits。
- 来源称官方计划从每月 25 美元起；价格与额度具有时效性，应以官方最新说明为准。 ^[ambiguous]

## Low-Risk Trial

- 先用一条 3–5 分钟短视频验证真实额度消耗。
- 安装插件后新建 Task 测试，避免直接影响已有工程。

## Related

- [[concepts/agent-skill-as-application]] — 把视频编辑能力封装为 Agent 可执行的应用工作流。
- [[concepts/prompt-context-harness-engineering]] — 额度、项目隔离和验证步骤属于执行 harness 的边界。 ^[inferred]

## Sources

- ChatCut 到底收不收费（2026-07-13 已发布短文）。
