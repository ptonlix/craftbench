---
title: Research-First Vibe Coding
category: concepts
tags: [vibe-coding, research, architecture, workflow]
aliases: [先研究再开工, Research Before Coding]
relationships:
  - target: "[[concepts/vibe-coding]]"
    type: extends
  - target: "[[concepts/prompt-context-harness-engineering]]"
    type: uses
  - target: "[[concepts/agent-loop-engineering]]"
    type: implements
sources: [/Users/atlas/WorkStation/craftbench/workbench/articles/published/2026-07-12-social-short-post-vibe-coding-research-first.md]
summary: 在让 Agent 写代码前，先研究同类开源项目并比较功能、架构和取舍，再由人确认方案后实施。
provenance:
  extracted: 0.80
  inferred: 0.20
  ambiguous: 0.0
base_confidence: 0.37
lifecycle: draft
lifecycle_changed: 2026-07-17
tier: supporting
created: 2026-07-17T07:06:00Z
updated: 2026-07-17T07:06:00Z
---

# Research-First Vibe Coding

Research-first Vibe Coding 把 Agent 的角色顺序从“立即编码”改成“先做研究，再提出方案，确认后实施”。它针对的主要风险不是生成速度不足，而是 Agent 太快固化第一个可运行方案。

## Workflow

1. 明确项目目标，并要求暂不写代码。
2. 搜索若干相似开源项目。
3. 比较功能、架构、技术栈、优点与缺点。
4. 基于已有工程经验提出实现方案。
5. 由人确认方案后再进入编码。

## Why It Works

- 同类项目把已经发生过的工程取舍和踩坑经验带进当前上下文。
- 方案评审在代码大量生成前发生，改变方向的成本更低。
- 研究、确认和实施形成一个带检查点的 [[concepts/agent-loop-engineering|Agent Loop]]。
- 它扩展了 [[concepts/vibe-coding]]：关键能力不仅是清楚描述需求，也包括先构造高质量工程上下文。

## Open Questions

- 如何判断参考项目的架构适合当前规模，而不是盲目复制？
- 研究阶段应在什么条件下停止，避免分析替代交付？

## Sources

- Vibe Coding 先研究再开工（2026-07-12 已发布短文）。
