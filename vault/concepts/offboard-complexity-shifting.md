---
title: Offboard Complexity Shifting
category: concepts
tags: [systems-engineering, aerospace, reusability, optimization]
aliases: [箭地复杂度转移, 地面系统吸收复杂度]
relationships:
  - target: "[[concepts/human-in-the-loop]]"
    type: related_to
  - target: "[[concepts/agent-loop-engineering]]"
    type: related_to
sources: [/Users/atlas/WorkStation/craftbench/workbench/articles/published/2026-07-11-social-short-post-china-rocket-recovery.md]
summary: 在可重复使用系统中，把质量、容错和维护复杂度从昂贵移动端转移到可复用地面设施，可能提升载荷与综合经济性。
provenance:
  extracted: 0.55
  inferred: 0.30
  ambiguous: 0.15
base_confidence: 0.37
lifecycle: draft
lifecycle_changed: 2026-07-17
tier: supporting
created: 2026-07-17T07:06:00Z
updated: 2026-07-17T07:06:00Z
---

# Offboard Complexity Shifting

可重复使用火箭的系统优化不只发生在箭体上。一个重要方向是把支撑、捕获和误差吸收能力留在地面，让每次飞行都必须携带的箭上质量更少。

## Key Ideas

- 着陆腿等随箭往返的结构会占用质量和燃料预算；地面捕获设施可以承担部分支撑功能。
- 在捕获装置中增加柔性，有机会由地面系统吸收更多姿态与位置误差，从而降低箭上控制装置与回收燃料负担。
- 这种设计把复杂度转移到更容易维护和重复使用的固定资产，体现的是系统级成本优化，而不只是单个零件改良。 ^[inferred]
- 谁的方案综合更优仍取决于捕获载荷、材料疲劳、检修成本和长期复用数据，现阶段不能只凭概念判断。 ^[ambiguous]

## Related

- [[concepts/agent-loop-engineering]] — 同样强调优化整条系统链路而非局部能力。
- [[concepts/human-in-the-loop]] — 都体现把容错与控制放在更可治理的系统层。 ^[inferred]

## Open Questions

- 柔性捕获带来的地面设施成本，能否被更高载荷和更低箭上复杂度抵消？
- 不同捕获载荷对箭体寿命与复飞检修的长期影响如何？

## Sources

- 中国火箭回收方案的系统工程优势（2026-07-11 已发布短文）。
