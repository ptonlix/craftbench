---
title: MCP Stateless Protocol
category: concepts
tags: [mcp, ai-agent, protocol, infrastructure]
aliases: [MCP 无状态协议]
relationships:
  - target: "[[concepts/agent-loop-engineering]]"
    type: uses
sources: [/Users/atlas/WorkStation/craftbench/workbench/articles/published/2026-07-30-social-short-post-mcp-2026-protocol/2026-07-30-social-short-post-mcp-2026-protocol.md]
summary: MCP 通过自包含请求、显式状态句柄和标准 HTTP 运维能力，从会话绑定的工具协议走向可横向扩展的 Agent 基础设施。
provenance: {extracted: 0.90, inferred: 0.08, ambiguous: 0.02}
base_confidence: 0.37
lifecycle: draft
lifecycle_changed: 2026-08-12
tier: supporting
created: 2026-08-12T11:04:00+08:00
updated: 2026-08-12T11:04:00+08:00
---

# MCP Stateless Protocol

MCP 2026-07-28 候选版本删除协议级会话绑定，使每次请求携带处理所需上下文，并让任意服务实例接手。应用状态仍可存在，但通过工具返回的显式句柄传递。

## Key Ideas

- 无状态请求减少 sticky session 和共享会话存储依赖，便于普通负载均衡和横向扩容。
- `Mcp-Method`、`Mcp-Name`、缓存范围和 W3C Trace Context 让网关、限流、缓存与观测更容易接入。
- 长任务、交互式界面和扩展能力从核心协议中解耦，以独立扩展和任务句柄演进。
- 破坏性变更意味着依赖旧会话、旧 Tasks API 或特定错误码的实现需要迁移。

## Related

- [[concepts/agent-loop-engineering]]
- [[concepts/agent-goal-boundary-security]]
- [[references/published-articles-2026-07-29-to-08-11]]

