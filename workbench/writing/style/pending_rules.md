# 候选风格规则

用途：保存 learner 从文章、trace、diff、反馈中提炼出的待审候选。默认学习结果先写这里。

## Pending Rules

### PENDING-20260712-001
- status: activated
- scope: article
- suggested_layer: instruction
- confidence: high
- evidence: workbench/articles/published/2026-07-08-article-beeweave-creation-workbench.md；workbench/articles/published/2026-06-12-agent-loop-engineering/index.md；workbench/articles/published/2026-06-20-prompt-context-harness/index.md。多篇观点长文都从具体痛感、真实工作场景或反常识判断切入，再上升到方法论。
- validation: 下次写观点长文时检查开头前 300 字是否先出现具体问题、亲身观察或明确判断，而不是先铺概念定义。
- resolution: activated as RULE-20260712-001 on 2026-07-12 after user confirmation.
- rule: 长文开头优先从“我遇到的具体问题/正在做的具体项目/一个反常识发现”切入，然后再解释概念；不要一上来写宏大背景或百科式定义。

### PENDING-20260712-002
- status: activated
- scope: article
- suggested_layer: instruction
- confidence: high
- evidence: workbench/articles/published/2026-06-01-gohumanloop-langgraph/index.md；workbench/articles/published/2026-06-02-gohumanloop-crewai/index.md；workbench/articles/published/2026-06-02-gohumanloop-wework/index.md；workbench/articles/published/2026-06-05-gohumanloop-wework-langgraph/index.md。GoHumanLoop 系列稳定采用“项目/场景介绍 -> 需求背景 -> 代码或配置 -> 运行过程 -> 示例展示 -> 总结/下一步”的实践路线。
- validation: 下次写技术教程时检查是否包含可执行场景、完整操作路径、运行方式和结果展示；缺任一项则视为不完整。
- resolution: activated as RULE-20260712-002 on 2026-07-12 after user confirmation; merged related series-position signal from PENDING-20260712-009.
- rule: 技术实践文要按“场景-需求-实现-运行-结果-下一步”组织，先让读者知道为什么做，再给可复制的代码/配置，最后展示跑通后的现象和后续入口。

### PENDING-20260712-003
- status: pending
- scope: article
- suggested_layer: instruction
- confidence: medium
- evidence: workbench/articles/published/2026-06-12-agent-loop-engineering/index.md；workbench/articles/published/2026-06-20-prompt-context-harness/index.md；workbench/articles/published/2026-06-25-jit-learning/index.md。观点文常用“三层、三点、三色、同心圆、入口/边界/刹车”等结构，把抽象工程问题压成可记忆框架。
- validation: 下次写方法论文章时检查是否把核心观点压缩成 2-4 个稳定节点，并且每个节点都有解释或例子支撑。
- rule: 讲抽象方法论时，优先把观点压成少量清晰节点，例如三层、三点、几个角色或一组边界；每个节点都要承担不同功能，不能只是排比换词。

### PENDING-20260712-004
- status: activated
- scope: all
- suggested_layer: instruction
- confidence: high
- evidence: workbench/articles/published/2026-06-02-agent-cleaner-skill/index.md；workbench/articles/published/2026-07-08-article-beeweave-creation-workbench.md；workbench/articles/published/2026-07-10-social-zhihu-vibe-coding-free-resources.md。多篇文章使用“我翻了/我发现/我自己一直/我当时”这类真实行动或体感句，配合具体数字、项目名、路径、仓库名。
- validation: 下次生成文章或短内容时，检查每 3-5 段是否有真实行为、具体对象、数字、项目名或使用结果之一；如果只有抽象判断，需要补证据。
- resolution: activated as RULE-20260712-003 on 2026-07-12 after user confirmation.
- rule: 写作要保留作者在场感：用真实动作、具体对象、数字、项目名、路径、工具名和使用后果支撑判断，让观点像从现场长出来，而不是从概念推出来。

### PENDING-20260712-005
- status: activated
- scope: all
- suggested_layer: instruction
- confidence: high
- evidence: workbench/articles/published/2026-06-12-agent-loop-engineering/index.md；workbench/articles/published/2026-06-20-prompt-context-harness/index.md；workbench/articles/published/2026-06-25-jit-learning/index.md；workbench/articles/published/2026-06-02-agent-cleaner-skill/index.md。多篇文章把 AI 能力与权限边界、验证、人工审批、回滚、可追溯放在一起讲。
- validation: 下次写 AI Agent、自动化、工具或工作流时，检查是否说明能力边界、验证方式或人类接管点；没有则补一段风险与护栏。
- resolution: activated as RULE-20260712-004 on 2026-07-12 after user confirmation.
- rule: 写 AI 工具和 Agent 时，不只写“能做什么”，还要写“哪里该停、怎么验证、谁来确认、出错怎么恢复”；安全护栏和人类判断是作者稳定视角。

### PENDING-20260712-006
- status: pending
- scope: article
- suggested_layer: instruction
- confidence: medium
- evidence: workbench/articles/published/2026-07-08-article-beeweave-creation-workbench.md；workbench/articles/published/2026-06-12-agent-loop-engineering/index.md；workbench/articles/published/2026-06-20-prompt-context-harness/index.md。长文常用短句单独成段、连续追问和口语化转折，例如“挺离谱的”“这就很可怕”“但问题来了”“说到底”。
- validation: 下次写长文时检查是否有适度短句断裂和口语转场；同时人工确认没有过度口水化或情绪堆砌。
- rule: 长文可以用短句单独成段制造节奏，用追问和口语转折推进阅读，但每个短句都要承担推进、强调或转向功能，不能只为“活人感”而断句。

### PENDING-20260712-007
- status: activated
- scope: social
- suggested_layer: instruction
- confidence: high
- evidence: workbench/articles/published/2026-07-09-social-short-post-ai-model-race.md；workbench/articles/published/2026-07-10-social-zhihu-vibe-coding-free-resources.md。两篇 social 均为已发布短内容，并附带质检报告；开头使用“最有意思的点，不是 X，而是 Y”或“我翻了以后发现一个荒谬事实”作为钩子。
- validation: 下次写短内容时检查前两段是否提出一个可传播的反常识、信息差或判断转向；如果只是介绍主题，需要重写开头。
- resolution: activated as RULE-20260712-005 on 2026-07-12 after user confirmation.
- rule: 社交短内容开头优先用“不是 X，而是 Y”“我做了一个具体动作后发现 Z”“大家以为 A，其实 B”建立钩子，尽快给出判断转向。

### PENDING-20260712-008
- status: activated
- scope: social
- suggested_layer: instruction
- confidence: high
- evidence: workbench/articles/published/2026-07-09-social-short-post-ai-model-race.md；workbench/articles/published/2026-07-10-social-zhihu-vibe-coding-free-resources.md。短内容正文保持 300-600 字左右，无正文 bullet，段落短，每段推进一个信息单元，结尾给明确判断而非口号。
- validation: 下次写 social short-post 时检查字数、段落推进、正文是否无列表化，以及结尾是否落在具体判断上。
- resolution: activated as RULE-20260712-006 on 2026-07-12 after user confirmation.
- rule: 社交短内容正文保持短段落和高信息密度，正文尽量不用 bullet；每段只推进一个信息单元，结尾落在一句有判断力的话，而不是泛泛号召。

### PENDING-20260712-009
- status: merged
- scope: article
- suggested_layer: instruction
- confidence: medium
- evidence: workbench/articles/published/2026-06-01-gohumanloop-langgraph/index.md；workbench/articles/published/2026-06-02-gohumanloop-crewai/index.md；workbench/articles/published/2026-06-02-gohumanloop-wework/index.md；workbench/articles/published/2026-06-05-gohumanloop-wework-langgraph/index.md。系列文章会回扣前文、说明本篇位置，并在结尾给下一步或更多示例入口。
- validation: 下次写系列内容时检查开头是否交代系列上下文，结尾是否告诉读者下一篇或下一步可以做什么。
- resolution: merged into RULE-20260712-002 on 2026-07-12 after user confirmation to avoid fragmented active rules.
- rule: 系列文章要显式标出本篇在系列中的位置：开头回扣前文或说明当前任务，结尾给下一篇、更多示例或实践入口，让读者知道这篇不是孤立内容。

### PENDING-20260712-010
- status: profiled
- scope: methodology
- suggested_layer: resource
- confidence: medium
- evidence: workbench/articles/published/2026-06-20-prompt-context-harness/index.md；workbench/articles/published/2026-06-12-agent-loop-engineering/index.md；workbench/articles/published/2026-06-25-jit-learning/index.md。稳定出现“Prompt/Context/Harness”“Loop Engineering”“JIT Learning”等 AI 工程认知框架，关注从技巧到系统、从单次回答到闭环工作流。
- validation: 后续写 AI 工程类内容时，观察是否继续围绕“上下文、循环、工具外壳、验证、人类判断”展开；若连续新稿命中，可升级为作者画像或主题偏好。
- resolution: moved into author_profile.md on 2026-07-12 after user confirmation; not activated as an instruction rule.
- rule: 作者长期关注 AI Agent 工程化：不满足于提示词技巧，而是倾向讨论上下文组织、工作循环、工具外壳、验证机制、人工接管和长期记忆。

### PENDING-20260714-001
- status: pending
- scope: social
- suggested_layer: instruction
- confidence: high
- evidence: workbench/writing/traces/2026-07-13-social-chatcut-pricing/trace.json；用户明确认可素材中的铺垫式开头，并指令将原有问句钩子改为“热点讨论—网友质疑—主动研究—直接结论”的完整开场，属于用户指令驱动的强改稿信号。
- validation: 后续撰写热点解释、收费澄清或争议回应类短帖时，分别测试直接问句钩子与四步铺垫开场；检查四步开场是否能在前 4 个短段内交代讨论背景、核心质疑、作者行动和明确结论，且没有拖慢正文。
- rule: 写热点解释、收费澄清或争议回应类短帖时，开头优先按“热点讨论—外部质疑—我去研究/核实—先给结论”推进；先让读者知道争议从哪里来、作者为何介入，再进入具体解释。该规则是 RULE-20260712-005 的场景化补充，不替代一般社交短内容的反常识钩子规则。

## 条目格式

```text
### PENDING-YYYYMMDD-001
- status: pending
- scope: article | social | all | methodology
- suggested_layer: route | instruction | resource
- confidence: low | medium | high
- evidence: trace 路径、历史文章路径、用户反馈或 diff 摘要
- validation: 建议如何验证
- rule: 候选规则
```

## 写入规则

- 单次反馈、低置信观察、未验证模式写入 pending。
- 用户手动改稿和用户指令驱动 AI 改稿是强信号，但仍需判断是否稳定。
- 被发布、标记 final 或明确采纳的版本可以提高 confidence。
