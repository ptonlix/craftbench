# Wiki Index

## Projects

- [[projects/beeweave/beeweave]] — 面向 Agent 的知识工作台，把 workbench 原始材料、vault 稳定知识和 skills 连接成创作与知识复用飞轮。 ( #beeweave #knowledge-workbench #agent #markdown)

## Concepts

- [[concepts/vibe-coding]] — 用 AI 把想法变成产品的编程方式，核心是拆需求、给 AI 完整上下文、调试 AI 生成代码和迭代成品的能力。 ( #vibe-coding #ai-programming #learning #llm)
- [[concepts/human-in-the-loop]] — 在 Agent 关键动作前引入人工输入、审批、反馈或接管的控制机制，用来保留判断权与可追溯性。 ( #ai-agent #governance #safety #workflow)
- [[concepts/agent-loop-engineering]] — 让 AI 从单次对话变成有入口、上下文、工具、验证、记忆和接管点的持续工作系统。 ( #ai-agent #engineering #workflow #automation)
- [[concepts/prompt-context-harness-engineering]] — Prompt、Context、Harness 分别决定任务表达、信息质量和可靠执行环境。 ( #ai-agent #prompt #context #harness)
- [[concepts/jit-learning]] — 在新问题出现时快速理解本质、提出高质量要求、把控结果并沉淀稳定认知的学习方式。 ( #learning #ai-era #meta-skill #judgment)
- [[concepts/agent-skill-as-application]] — 把明确、规则可定义的工具软件能力封装成轻量应用，让 Agent 直接执行分析、报告和受控操作。 ( #agent-skill #software #automation #product)
- [[concepts/ai-model-scaling-race]] — 2026 下半年模型竞赛的一个关键信号是，前沿实验室可能重新把竞争焦点拉回更大规模预训练和 scale law 兑现能力。 ( #ai-models #scale-law #pretraining #competition)
- [[projects/beeweave/concepts/workbench-vault-architecture]] — BeeWeave 用 workbench 保存原始输入、草稿和发布稿，用 vault 保存稳定知识页。 ( #beeweave #architecture #workbench #vault)
- [[projects/beeweave/concepts/agent-skill-install-model]] — BeeWeave 将少量便携技能全局安装，把完整技能集和 bootstrap 模板安装到选定项目。 ( #beeweave #skills #agents #bootstrap)

## Entities

- [[entities/easy-vibe]] — DataWhale 出品的 Vibe Coding 入门实战仓库，16K star，纯项目驱动。 ( #vibe-coding #github #open-source #datawhale)
- [[entities/vibe-coding-cn]] — Vibe Coding 方法论核心仓库，1.4K star，教 Prompt 规范、Skill 库沉淀和工作流搭建。 ( #vibe-coding #github #methodology #workflow)
- [[entities/awesome-vibe-coding]] — Vibe Coding 工具百科仓库，5.5K star，收录完整 AI 编程工具链。 ( #vibe-coding #github #tools #awesome-list)
- [[entities/gohumanloop]] — 一个 Python 库，使 AI Agent 能在关键阶段动态请求人类输入、审批、反馈或对话。 ( #ai-agent #python #human-in-the-loop #framework)
- [[entities/gohumanloop-wework]] — 把 GoHumanLoop 审批和信息获取请求接入企业微信审批体系的示例服务。 ( #ai-agent #wework #approval #go)
- [[projects/beeweave/entities/beeweave-brain-capture-extension]] — 零构建 Chrome 扩展，可把当前网页 URL、可读文本或选中文本保存到 workbench inbox。 ( #beeweave #browser-extension #capture #workbench)

## Skills

- [[skills/vibe-coding-self-learning-path]] — 用三个免费开源仓库组成的 Vibe Coding 完整自学路线，一至三个月从入门到团队级产出。 ( #vibe-coding #learning-path #self-study #ai-programming)
- [[skills/langgraph-human-loop-integration]] — 用 GoHumanLoop adapter 将审批、信息获取和反馈收集包装为 LangGraph 节点或装饰器。 ( #langgraph #ai-agent #human-in-the-loop #python)
- [[skills/crewai-human-loop-integration]] — 用 GoHumanLoop provider 和 manager 将 CrewAI 关键工具调用包装为邮件审批点。 ( #crewai #ai-agent #human-in-the-loop #python)
- [[skills/wework-human-loop-deployment]] — 部署 GoHumanLoop WeWork 需要配置企业微信应用、审批模板、信息模板、API Key、服务端回调和 Agent 侧 APIProvider。 ( #wework #deployment #approval #ai-agent)
- [[projects/beeweave/skills/beeweave-cli-operations]] — BeeWeave 的 `bwe` CLI 负责 setup、profile、uninstall、info、技能列表、graph/cache/batch/AST 等本地辅助操作。 ( #beeweave #cli #setup #operations)
- [[projects/beeweave/skills/beeweave-development-workflow]] — 修改 BeeWeave 本身时，应遵循 OpenSpec、集中 UI helper、非交互兼容和测试验证工作流。 ( #beeweave #development #openspec #testing)

## References

- [[references/vibe-coding-social-post-2026-07-10]] — 一篇知乎短文，揭露 Vibe Coding 付费课 99% 内容来自三个免费开源仓库。 ( #vibe-coding #social-post #zhihu #source)
- [[references/published-article-batch-2026-06]] — 2026 年 6 月已发布文章批次，覆盖 GoHumanLoop、HITL、Agent skill、Loop Engineering、Prompt/Context/Harness 和 JIT Learning。 ( #source-batch #article #ai-agent #workbench)
- [[references/ai-model-race-social-post-2026-07-09]] — 一篇社交短文，把 GPT-6、Anthropic Mythos 5、xAI Grok、DeepSeek V4 和 MiniMax M3 Pro 的传闻压缩成对 2026 下半年模型竞赛的判断。 ( #source #social-post #ai-models #scale-law)
- [[projects/beeweave/references/beeweave-source-repository]] — BeeWeave 源码仓库作为本次 ingest 来源的范围：README、docs、bootstrap、skills、OpenSpec、CLI、测试和扩展。 ( #beeweave #source-repository #documentation #openspec)
- [[projects/beeweave/references/beeweave-creation-workbench-article]] — 已发布文章，用写作和多 Agent 工作流解释 BeeWeave 的问题意识、创作飞轮和技能边界。 ( #beeweave #article #creation-workbench #agent)

## Synthesis

- [[synthesis/ai-agent-production-loop]] — 生产级 Agent Loop 由任务入口、上下文、工具、权限边界、验证、人类审批、日志和外部记忆共同构成。 ( #ai-agent #production #workflow #synthesis)
