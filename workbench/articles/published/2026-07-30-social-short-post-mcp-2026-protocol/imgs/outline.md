---
type: comparison
density: minimal
style: screen-print
palette: warm
image_count: 1
language: zh
aspect_ratio: "16:9"
---

## Illustration 1

**Position**: 社交媒体博文开头，导语之后
**Purpose**: 用一张左右架构对比图直观呈现 MCP 2026-07-28 从有状态协议到无状态协议的核心变化，同时承担社交媒体宣传封面功能。
**Visual Content**: 左侧是旧版客户端经负载均衡后被固定路由到单一 MCP Server，并依赖 Session ID 和共享会话存储；右侧是新版自包含请求经普通轮询负载均衡后可到达任意 MCP Server 实例，无协议级会话存储。中央用箭头表达从 2025-11-25 到 2026-07-28 的迁移。
**Type Application**: 左右分屏 Comparison，左侧强调耦合和运维负担，右侧强调无状态、可扩展和可路由。
**Filename**: 01-comparison-mcp-stateless-architecture.png

