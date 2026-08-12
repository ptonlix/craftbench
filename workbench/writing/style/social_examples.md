# 社交短内容示例

用途：保存用户确认可复用的推文、thread、朋友圈短文、短观点写法和 before/after 对比摘要。

## Examples

### EXAMPLE-20260716-001
- scope: social
- format: short-post
- source: workbench/articles/drafts/2026-07-16-social-short-post-one-person-company-risk/2026-07-16-social-short-post-one-person-company-risk.md
- status: accepted
- why_it_matters: 用户明确说明正文由其手动改写；改稿展示了观点短文如何用独立金句强化主轴，并在保持短段落的同时，用局部问题清单提升扫读性。
- pattern: 首段先给风险判断，随后用一句独立对照金句压缩核心矛盾；论证阶段保持短段落，进入行动检查时再局部切换为 3 项左右的短清单；结尾回扣开头并形成可独立传播的判断句。
- excerpt_or_summary: 围绕“一人公司最大的风险”，把生产效率与商业验证的错位作为主轴，使用“软件门槛/生意门槛”的对照金句，并把需求验证拆成简短检查项。

### EXAMPLE-20260809-001
- scope: social
- format: short-post
- source: workbench/articles/published/2026-08-06-social-short-post-ai-mvp-closed-loop.md；workbench/writing/traces/2026-08-06-social-ai-mvp-closed-loop/trace.json
- status: accepted
- why_it_matters: 用户两次明确指导改稿，要求先交代外部观点来源再自然引出自己的思考，并把刻意书面化的成语改成日常表达；最终 v3 已发布，是来源式开头和直接语言偏好的强证据。
- pattern: 用一两句交代看到的人物、视频或观点，随后迅速提出自己的判断；正文用具体案例扩展观点，再补充旧方法仍然有效的边界；词语选择直接、日常，不使用幕后素材分析口吻或为修辞而修辞。
- excerpt_or_summary: 从 Patrick Collison 讨论 AI 创业的视频切入，提出“AI 降低的是做产品的门槛，不是做生意的门槛”，再用 Stripe 早期客户路径解释最小业务闭环，并保留“MVP 仍负责验证方向”的边界。

### EXAMPLE-20260809-004
- scope: social
- format: short-post
- source: workbench/articles/published/2026-07-13-social-short-post-chatcut-pricing.md；workbench/writing/traces/2026-07-13-social-chatcut-pricing/trace.json；PENDING-20260714-001
- status: accepted
- why_it_matters: 这是 RULE-20260809-001 的热点争议与收费澄清细分写法。用户明确要求把直接问句改为完整来源铺垫，最终稿用四个紧凑步骤交代讨论背景、外部质疑、作者核实和明确结论；该模式有效但适用范围窄，不单独升级为 active rule。
- pattern: 热点解释、收费澄清或争议回应类短帖，可在前四个短段内依次完成“热点讨论—外部质疑—主动研究或核实—先给结论”，随后再拆分费用、条件或事实边界。
- excerpt_or_summary: 从“很多人在聊 ChatCut”及网友对收费的质疑切入，说明作者专门研究后先给出“插件本身不用额外付费”的结论，再区分基础编辑、生成素材和 Agent 原有订阅成本。

### EXAMPLE-20260809-002
- scope: social
- format: short-post
- source: workbench/articles/published/2026-07-28-social-short-post-vibe-coding-ownership.md；workbench/writing/traces/2026-07-28-social-vibe-coding-ownership/trace.json
- status: accepted
- why_it_matters: 用户明确要求增加当天在 X 上看到的案例，并删除按代码行数判断工具规模的武断标准；发布终稿展示了如何由外部案例进入观点，同时把判断标准落在边界、复杂度和维护责任上。
- pattern: 先讲一个来源明确、足够短的真实案例，再用对照句提出核心矛盾；论证不依赖表面数量指标，而是沿生命周期、责任和适用条件推进，结尾把长文压回一句可传播判断。
- excerpt_or_summary: 从团队用 AI 快速自研 JIRA 替代品却最终回购 SaaS 的案例切入，区分软件的创造成本与拥有成本，最后落到“便宜的是第一版，昂贵的是接下来几年”。

## 条目格式

```text
### EXAMPLE-YYYYMMDD-001
- scope: social
- format: x | thread | short-post | wechat-moments
- source: 文件路径或 trace 路径
- status: accepted | observed | pending
- why_it_matters: 为什么这个例子值得学习
- pattern: 可复用写法
- excerpt_or_summary: 示例片段摘要，避免无必要复制全文
```

## 使用约束

- 社交示例优先记录钩子、节奏、断句、互动方式和平台格式。
- 不把某一次热点表达直接泛化成长期规则。
- 示例不能自动升级为 active 规则，除非有明确证据和确认。
