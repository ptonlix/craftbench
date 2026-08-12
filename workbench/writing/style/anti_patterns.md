# 反模式

用途：记录用户明确拒绝、历史改稿中稳定删除或验证失败的写法。

## 默认反模式

### ANTI-DEFAULT-001
- status: active
- scope: all
- evidence: BeeWeave 默认初始化
- avoid: 空泛套话，例如“随着技术的发展”“值得注意的是”“综上所述”。
- prefer: 直接从具体事件、判断、场景或问题切入。

### ANTI-DEFAULT-002
- status: active
- scope: all
- evidence: BeeWeave 默认初始化
- avoid: 未经证实的“我朋友”“有一次”“我亲测”等编造式例子。
- prefer: 使用用户提供的真实经历；没有经历时明确说还没验证。

## Learned Anti-patterns

### ANTI-20260809-001
- status: active
- scope: social
- evidence: PENDING-20260809-002；workbench/writing/traces/2026-08-06-social-ai-mvp-closed-loop/trace.json；用户明确要求将“奉为圭臬”改为“追捧”，对应 v3 终稿已发布；用户在 2026-08-09 确认按审阅建议执行
- avoid: 为了显得有文采而使用生僻成语、过度书面化措辞或脱离日常语境的修辞，例如用“奉为圭臬”代替“追捧”。
- prefer: 使用直接、日常、读一遍就懂的词，把表达力量放在判断和事实本身，而不是词藻上。

## 条目格式

```text
### ANTI-YYYYMMDD-001
- status: active
- scope: article | social | all
- evidence: trace 路径、用户反馈或 before/after diff
- avoid: 需要避免的写法
- prefer: 推荐替代方式
```
