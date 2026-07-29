---
title: Vibe Coding
category: concepts
tags:
  - vibe-coding
  - ai-programming
  - learning
  - llm
  - workflow
sources:
  - "published social post: 2026-07-10-social-zhihu-vibe-coding-free-resources.md"
  - /Users/atlas/WorkStation/craftbench/workbench/articles/published/2026-07-12-social-short-post-vibe-coding-research-first.md
  - /Users/atlas/WorkStation/craftbench/workbench/articles/published/2026-07-28-social-short-post-vibe-coding-ownership.md
base_confidence: 0.74
lifecycle: draft
lifecycle_changed: "2026-07-10"
tier: supporting
summary: >
  Vibe Coding 降低软件首版生产成本，但稳定产出和长期拥有仍需要研究、架构、测试、迁移、监控与明确责任。
provenance:
  extracted: 0.76
  inferred: 0.19
  ambiguous: 0.05
updated: 2026-07-29T17:20:11+08:00
---

## 是什么

Vibe Coding 不是在学编程，是学「用 AI 把想法变成产品」。和传统编程不同，它的重心不在于手写代码，而在于如何描述需求、给 AI 提供完整上下文、调试和迭代 AI 生成的半成品代码，直到得到一个可用的产品。^[inferred]

一句话总结，**会用 AI 编程，跟会编程，是两回事**。

## 四项核心能力

1. 把需求拆清楚
2. 给 AI 完整的工程上下文
3. 调试 AI 生成的代码
4. 把半成品一步步迭代成成品

## 与传统编程的关系

Vibe Coding 不排斥传统编程知识。有编程基础的人在调试阶段会更快，但零基础也能从 AI 小游戏和 Web 原型项目起步，边做边建立手感。^[inferred]

## 学习路线

见 [[skills/vibe-coding-self-learning-path]]。三个免费的开源仓库（[[entities/easy-vibe]]、[[entities/vibe-coding-cn]]、[[entities/awesome-vibe-coding]]）组成的自学路线可以在一到三个月内跑通从 AI 小游戏到多 Agent 协同的完整流程。

## 与 Agent 开发的关系

Vibe Coding 和 [[concepts/agent-loop-engineering]] 有重叠——都涉及将 AI 从单次对话扩展为持续工作系统。Vibe Coding 更侧重个人用 AI 做产品，Agent Loop 更侧重生产级自动化系统的设计。^[inferred]

## 先研究再开工

[[concepts/research-first-vibe-coding]] 把 Vibe Coding 从“描述需求后立即生成”扩展为研究、方案确认和实施三个阶段。先比较同类开源项目的功能、架构、技术栈与取舍，可以降低 Agent 过早固化第一个可运行方案的风险。

## 创造成本与拥有成本

Vibe Coding 显著降低的是软件第一版的生产成本：一个人可以在几小时内生成页面、接口和数据库。但软件生命周期远长于首次开发，后续仍要承担权限、数据迁移、通知、依赖升级、监控、备份、安全和故障恢复等责任。

AI 擅长局部修改，却不天然掌握整个系统的责任边界。没有明确代码所有者时，连续的局部修补会增加系统理解和维护成本。因此，自研与购买的判断标准不应只是“能否快速做出来”，而应是团队能否控制复杂度，并愿意长期承担维护责任。

一次性脚本、数据迁移、Glue Code 和边界清晰的团队专属工具适合用 AI 加速；复制 Jira、Notion、Slack 这类复杂生态产品则需要谨慎。更稳健的边界是：竞争优势自己做，通用能力尽量买。
