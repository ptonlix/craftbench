---
title: "BeeWeave 自进化写作工作流"
type: social
format: short-post
status: draft
created: 2026-07-14T15:48:00+08:00
updated: 2026-07-14T16:17:00+08:00
tags:
  - writing
  - beeweave
---

用 AI 写作最烦的，不是初稿不够好，而是你明明改过很多次，下一篇它还是照样犯错。

开头太宏大，删掉。语气像报告，重写。结尾全是套话，再改。你花时间调教出的偏好，只活在当前对话里。换个会话，一切重新开始。

我最近给 BeeWeave 加了一套自进化写作工作流，就是想解决这个问题。

writer 记录写稿和改稿过程。learner 从终稿、修改和反馈里提炼候选规则。evolver 负责审阅、验证和激活。下次动笔，writer 会自动读取已经生效的风格、反模式和示例。

你改掉的坏习惯，不会反复出现。你强调过的表达偏好，也不用每次重写 Prompt。

规则不会偷偷生效。它们先进入待审区，经过验证或人工确认后才会启用，还能拒绝和回滚。

BeeWeave 不是让 AI 多写一篇，而是让每一次改稿，都成为下一篇的起点。

🐝 BeeWeave is an agent-native creation workbench that turns collected material, AI-assisted drafts, and durable markdown knowledge into a reusable creative data flywheel.

项目地址
https://github.com/ptonlix/beeweave

自进化写作工作流
https://ptonlix.github.io/beeweave/zh/self-evolving-writing/

## 质检报告

**L1 硬性规则** ✅
- 正文禁用词与禁用标点零命中
- 正文无列表、无空泛工具名
- 正文加项目说明与链接后仍在长推上限内
- 无表演式情绪和陈词滥调

**L2 风格一致性** ✅
- 从反复改稿却无法积累的具体痛点切入
- 短段落逐层推进，信息密度高
- BeeWeave、writer、learner、evolver 均为具体名称

**L3 活人感** ✅
- 有明确产品判断，没有品牌宣传腔
- 功能、边界和用户收益完整

**总评**：3 层全部通过
