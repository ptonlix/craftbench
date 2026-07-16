# 写作风格演进日志

用途：记录初始化、激活、拒绝、回滚和 compaction，保证风格系统可追溯。

## Log

## 2026-07-16 21:31 激活观点金句与局部清单规则

- action: activate
- affected_layer: resource
- affected_files: writing/style/active_style_rules.md；writing/style/pending_rules.md；writing/style/evolution_log.md
- evidence: PENDING-20260716-001；PENDING-20260716-002；workbench/articles/drafts/2026-07-16-social-short-post-one-person-company-risk/2026-07-16-social-short-post-one-person-company-risk.md；workbench/writing/traces/2026-07-16-social-one-person-company-risk/trace.json；用户明确说明正文为手动改写
- validation: writing/eval/ 暂无相关 social case；本次基于用户手动改稿强信号、规则重叠审阅和用户在 2026-07-16 明确确认激活
- summary: 新增观点型社交短文的独立对照金句规则；将局部短清单作为 RULE-20260712-006“正文尽量不用 bullet”的受限例外合并，避免规则冲突和 active 条目碎片化
- rollback: 删除 RULE-20260716-001；将 RULE-20260712-006 的 evidence、validated_by 和 rule 恢复为本次变更前内容；把 PENDING-20260716-001 恢复为 pending 并删除 resolution；把 PENDING-20260716-002 恢复为 pending 并删除 resolution

## 2026-07-12 22:52 激活首批发布稿风格规则

- action: activate
- affected_layer: resource
- affected_files: writing/style/active_style_rules.md；writing/style/author_profile.md；writing/style/pending_rules.md
- evidence: PENDING-20260712-001 至 PENDING-20260712-010；workbench/articles/published 下 11 篇已发布 Markdown 材料；用户在 2026-07-12 明确确认按审阅建议执行
- validation: writing/eval/ 暂无 rubric 或 eval case；本次基于多篇发布采纳样本、候选置信度和用户确认激活
- summary: 激活 6 条稳定写作规则，保留 2 条待验证规则，合并 1 条系列文章规则，并将 1 条主题偏好下沉到作者画像
- rollback: 从 active_style_rules.md 删除 RULE-20260712-001 至 RULE-20260712-006；从 author_profile.md 移除本次新增长期关注和证据；将 pending_rules.md 中 PENDING-20260712-001/002/004/005/007/008/009/010 的 status 和 resolution 恢复为 pending 状态

## 条目格式

```text
## YYYY-MM-DD HH:MM 变更标题

- action: initialize | learn | activate | reject | rollback | compact | source_patch
- affected_layer: route | instruction | resource
- affected_files: 文件或章节
- evidence: trace、历史文章、用户反馈或 eval case
- validation: 验证结果或用户确认
- summary: 这次变更解决的问题
- rollback: 回滚方式
```

## 初始化日志示例

```text
## YYYY-MM-DD HH:MM 默认初始化

- action: initialize
- affected_layer: resource
- affected_files: writing/style/*
- evidence: user requested default initialization
- validation: not required
- summary: 创建写作风格资产模板，等待后续从历史文章和 trace 学习
- rollback: 删除本次创建且未被用户编辑的模板文件
```
