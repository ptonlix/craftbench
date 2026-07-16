# 生效风格规则

用途：保存已经确认或高置信的长期写作规则。writer skills 只应把这里的匹配 scope 规则当作用户生效风格。

## 默认规则

### RULE-DEFAULT-001
- status: active
- scope: all
- layer: instruction
- evidence: BeeWeave 默认初始化
- validated_by: default
- rule: 用自然、具体、有判断力的中文表达，优先写真实观察、明确判断和可感知细节，避免空泛套话。

### RULE-DEFAULT-002
- status: active
- scope: all
- layer: instruction
- evidence: BeeWeave 默认初始化
- validated_by: default
- rule: 不编造第一手经历、人物、数据或使用结果；缺少事实时先标明不确定或向用户补问。

## Learned Rules

### RULE-20260712-001
- status: active
- scope: article
- layer: instruction
- evidence: PENDING-20260712-001；workbench/articles/published/2026-07-08-article-beeweave-creation-workbench.md；workbench/articles/published/2026-06-12-agent-loop-engineering/index.md；workbench/articles/published/2026-06-20-prompt-context-harness/index.md
- validated_by: user confirmation on 2026-07-12；published article samples
- rule: 长文开头优先从具体痛感、正在做的项目、真实工作场景或反常识发现切入，然后再解释概念；避免一上来写宏大背景或百科式定义。

### RULE-20260712-002
- status: active
- scope: article
- layer: instruction
- evidence: PENDING-20260712-002；merged PENDING-20260712-009；workbench/articles/published/2026-06-01-gohumanloop-langgraph/index.md；workbench/articles/published/2026-06-02-gohumanloop-crewai/index.md；workbench/articles/published/2026-06-02-gohumanloop-wework/index.md；workbench/articles/published/2026-06-05-gohumanloop-wework-langgraph/index.md
- validated_by: user confirmation on 2026-07-12；published article samples
- rule: 技术实践文按“场景-需求-实现-运行-结果-下一步”组织，先说明为什么做，再给可复制的代码或配置，最后展示跑通后的现象和后续入口；系列文章开头应回扣前文或说明本篇位置。

### RULE-20260712-003
- status: active
- scope: all
- layer: instruction
- evidence: PENDING-20260712-004；workbench/articles/published/2026-06-02-agent-cleaner-skill/index.md；workbench/articles/published/2026-07-08-article-beeweave-creation-workbench.md；workbench/articles/published/2026-07-10-social-zhihu-vibe-coding-free-resources.md
- validated_by: user confirmation on 2026-07-12；published article and social samples
- rule: 写作要保留作者在场感：用真实动作、具体对象、数字、项目名、路径、工具名和使用后果支撑判断，让观点像从现场长出来，而不是从概念推出来。

### RULE-20260712-004
- status: active
- scope: all
- layer: instruction
- evidence: PENDING-20260712-005；workbench/articles/published/2026-06-12-agent-loop-engineering/index.md；workbench/articles/published/2026-06-20-prompt-context-harness/index.md；workbench/articles/published/2026-06-25-jit-learning/index.md；workbench/articles/published/2026-06-02-agent-cleaner-skill/index.md
- validated_by: user confirmation on 2026-07-12；published article samples
- rule: 写 AI 工具、Agent、自动化或工作流时，不只写“能做什么”，还要写“哪里该停、怎么验证、谁来确认、出错怎么恢复”；安全护栏和人类判断是稳定视角。

### RULE-20260712-005
- status: active
- scope: social
- layer: instruction
- evidence: PENDING-20260712-007；workbench/articles/published/2026-07-09-social-short-post-ai-model-race.md；workbench/articles/published/2026-07-10-social-zhihu-vibe-coding-free-resources.md
- validated_by: user confirmation on 2026-07-12；published social samples with quality reports
- rule: 社交短内容开头优先用“不是 X，而是 Y”“我做了一个具体动作后发现 Z”“大家以为 A，其实 B”建立钩子，尽快给出判断转向。

### RULE-20260712-006
- status: active
- scope: social
- layer: instruction
- evidence: PENDING-20260712-008；PENDING-20260716-002；workbench/articles/published/2026-07-09-social-short-post-ai-model-race.md；workbench/articles/published/2026-07-10-social-zhihu-vibe-coding-free-resources.md；workbench/articles/drafts/2026-07-16-social-short-post-one-person-company-risk/2026-07-16-social-short-post-one-person-company-risk.md
- validated_by: user confirmation on 2026-07-12 and 2026-07-16；published social samples；user manual revision
- rule: 社交短内容正文保持短段落和高信息密度，正文尽量不用 bullet；每段只推进一个信息单元。遇到约 3 项需要逐项核对的判断标准或行动问题时，可以局部使用短而具体的清单，但不要把全文写成列表。结尾落在一句有判断力的话，而不是泛泛号召。

### RULE-20260716-001
- status: active
- scope: social
- layer: instruction
- evidence: PENDING-20260716-001；workbench/articles/drafts/2026-07-16-social-short-post-one-person-company-risk/2026-07-16-social-short-post-one-person-company-risk.md；workbench/writing/traces/2026-07-16-social-one-person-company-risk/trace.json
- validated_by: user manual revision and explicit activation confirmation on 2026-07-16
- rule: 观点型社交短文可以在开头判断之后增加一句独立成段的对照式金句，用更短、更可传播的表达钉住全文核心矛盾；金句必须推进或压缩观点，不能只是重复标题。

## 条目格式

```text
### RULE-YYYYMMDD-001
- status: active
- scope: article | social | all | methodology
- layer: instruction | resource | route
- evidence: trace 路径、历史文章路径或用户反馈摘要
- validated_by: eval case、人工确认或发布采纳
- rule: 具体规则
```
