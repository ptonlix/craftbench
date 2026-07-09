---
title: Human-in-the-Loop
category: concepts
tags: [ai-agent, governance, safety, workflow]
aliases: [HITL, Human Loop, 人类在环]
relationships:
  - target: "[[concepts/agent-loop-engineering]]"
    type: uses
  - target: "[[entities/gohumanloop]]"
    type: related_to
  - target: "[[synthesis/ai-agent-production-loop]]"
    type: related_to
sources:
  - workbench/articles/published/2026-06-01-gohumanloop-langgraph/index.md
  - workbench/articles/published/2026-06-02-gohumanloop-crewai/index.md
  - workbench/articles/published/2026-06-02-gohumanloop-wework/index.md
  - workbench/articles/published/2026-06-05-gohumanloop-wework-langgraph/index.md
  - workbench/articles/published/2026-06-12-agent-loop-engineering/index.md
summary: Human-in-the-loop 是在 Agent 关键动作前引入人工输入、审批、反馈或接管的控制机制，用来保留判断权与可追溯性。
provenance:
  extracted: 0.78
  inferred: 0.22
  ambiguous: 0.0
base_confidence: 0.78
lifecycle: draft
lifecycle_changed: 2026-07-08
tier: core
created: 2026-07-08T08:33:23Z
updated: 2026-07-08T08:33:23Z
---

# Human-in-the-Loop

Human-in-the-loop 是让 AI Agent 在关键阶段暂停并请求人类输入、审批、反馈或对话的流程控制机制。它不是反自动化，而是把人类判断放在高风险、低置信度或需要责任归属的节点上。

## Key Ideas

- 在金融交易、生产变更、数据删除、Offer 审批、关键配置修改等场景中，Agent 可以参与分析和准备，但最终动作前应设置审批点。
- 人类在环可以表现为三类动作：审批或拒绝、补充缺失信息、对结果提供反馈。
- HITL 的工程价值在于让 Agent 的行为可中断、可解释、可追踪，并把责任边界显式化。
- 可靠的 Agent Loop 不应追求无条件无人驾驶；更好的形态是自动执行低风险重复劳动，在关键节点交还判断权。
- HITL 需要和工具权限、日志、状态机、失败恢复、回调渠道一起设计，单靠一句 prompt 无法保证安全。 ^[inferred]

## Implementation Patterns

- 本地演示可使用终端 provider，让 LangGraph 或 CrewAI 流程在节点中等待输入。
- 异步流程可使用邮件、API provider 或企业微信审批，把人类决策从 Agent 运行环境外部带回工作流。
- 对审批结果应使用结构化状态，例如 approved、rejected、timeout、cancelled，而不是只依赖自然语言文本。
- 审批数据应作为工具调用或工作流节点的显式参数传入，避免 Agent 自行猜测审批结论。

## Related

- [[entities/gohumanloop]] — 提供 HITL 管理器、provider 和框架适配器。
- [[entities/gohumanloop-wework]] — 将 GoHumanLoop 请求接入企业微信审批。
- [[skills/langgraph-human-loop-integration]] — LangGraph 节点和装饰器集成方式。
- [[skills/crewai-human-loop-integration]] — CrewAI 工具调用审批方式。
- [[synthesis/ai-agent-production-loop]] — HITL 是生产级 Agent Loop 的刹车系统。

## Open Questions

- 审批粒度如何设置最合适：过粗会留下风险，过细会拖慢流程并让人产生审批疲劳。 ^[inferred]

## Sources

- [[references/published-article-batch-2026-06]] — 2026 年 6 月已发布文章批次。
