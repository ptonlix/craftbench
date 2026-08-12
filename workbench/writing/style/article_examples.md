# 长文示例

用途：保存用户确认可复用的长文结构、段落写法、开头、结尾、转场或 before/after 对比摘要。

## Examples

### EXAMPLE-20260809-003
- scope: article
- source: workbench/articles/published/2026-07-10-article-beeweave-knowledge-workbench.md；workbench/articles/published/2026-07-16-article-beeweave-writing-loop/2026-07-16-article-beeweave-writing-loop.md
- status: observed
- why_it_matters: 两篇已发布 BeeWeave 长文都从作者亲历的具体工作摩擦或当天创作过程切入，沿“问题—机制—真实运行—限制—行动入口”推进，并主动说明工具不适合的场景和实际失败。该模式与现有长文 active 规则一致，可作为结构示例，但没有单独的用户确认，因此记为 observed。
- pattern: 开头用真实项目现场建立问题；中段让系统结构跟着具体流程逐层出现；在宣传项目价值时同时保留失败、成本、不适用对象和人工判断边界；结尾给可执行的快速开始或参与入口，再回扣作者最初的问题。
- excerpt_or_summary: 一篇以多 Agent 会话中的重复解释切入，另一篇以当天从知乎链接到发布、配图、风格学习的完整流程切入；二者都把 BeeWeave 的机制放进正在发生的案例，而不是先罗列功能。

## 条目格式

```text
### EXAMPLE-YYYYMMDD-001
- scope: article
- source: 文件路径或 trace 路径
- status: accepted | observed | pending
- why_it_matters: 为什么这个例子值得学习
- pattern: 可复用写法
- excerpt_or_summary: 示例片段摘要，避免无必要复制全文
```

## 使用约束

- 默认只保存片段摘要或路径，不复制完整文章。
- 用户明确要求保存全文样本时，记录用户确认。
- 示例不能自动升级为 active 规则，除非有明确证据和确认。
