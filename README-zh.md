# Craftbench 知识创作台

[English](README.md) | 中文

Craftbench 是我用 [BeeWeave](https://github.com/ptonlix/beeweave) 构建的个人知识创作台。

BeeWeave 是一个 Agent 原生的创作工作台。它提供 `bwe` CLI、Agent skills、bootstrap 模板、浏览器捕获扩展和知识库维护流程，用来把素材获取、内容创作、知识沉淀和上下文复用连接成一个持续运转的数据飞轮。

## 与 BeeWeave 的关系

`../beeweave` 是上游工具和技能来源，包含：

- `beeweave/`：Python CLI 和辅助逻辑，提供 `bwe setup`、`bwe info`、`bwe list`、graph、cache、batch、AST 等能力。
- `.skills/`：BeeWeave 的 Agent skills，包括 ingest、query、update、capture、digest、synthesize、article writer、social writer 等。
- `bootstrap/`：安装到不同 Agent 的规则和启动文件模板，例如 `AGENTS.md`、Claude、Cursor、Kiro、Windsurf、Copilot 等适配文件。
- `extensions/brain-capture/`：浏览器捕获扩展，用来把网页和选中文本保存到 workbench inbox。
- `docs/`：BeeWeave 的中英文文档。
- `tests/` 和 `openspec/`：BeeWeave 自身的测试和规格变更记录。

`./craftbench` 是我的个人数据和创作工作区，包含：

- `workbench/`：创作工作台，保存素材、草稿、发布稿和临时输入。
- `vault/`：编译后的 Markdown 知识库，保存可复用、可查询、可链接的稳定知识。
- `AGENTS.md`：当前工作区的 Agent 协作规则。
- `.claude/`、`.codex/`：BeeWeave 为本项目安装的 Agent 本地技能入口。

## 目录结构

```text
.
├── workbench/          # 创作工作台：素材、收件箱、草稿、发布稿
├── vault/              # 知识库：概念、实体、技能、引用、综合分析
├── AGENTS.md           # Agent 在这个工作区里的协作规范
├── CLAUDE.md           # 指向 AGENTS.md 的兼容入口
├── README.md           # 英文说明文件
└── README-zh.md        # 中文说明文件
```

## 本机 setup 文件

Agent 入口文件和技能目录由 BeeWeave 按当前机器生成，已刻意加入
Git 忽略名单：

- `AGENTS.md`、`CLAUDE.md`、`GEMINI.md`、`HERMES.md`
- `.claude/`、`.codex/`
- `.env`、`.serena/`

这些文件可能包含本机路径，或指向 BeeWeave 源码 checkout 的软链接，
不应该提交到 GitHub。其他机器克隆这个工作区后，应重新运行
BeeWeave setup，让工具按新环境重新生成 Agent 入口和技能链接。

## workbench：创作工作台

`workbench/` 是内容进入系统的入口，也是写作和整理发生的地方。这里允许材料保持粗糙，因为它的职责是承接创作过程，而不是直接成为长期知识。

当前主要结构：

- `workbench/inbox/`：素材入口，保存网页捕获、临时记录和待处理输入。
- `workbench/inbox/web/`：来自网页捕获流程的页面快照和 Markdown。
- `workbench/articles/drafts/`：文章草稿区。
- `workbench/articles/published/`：已发布内容区，也是 ingest 到知识库的重要来源。
- `workbench/library/`：资料库，保存较稳定但未必已经进入 vault 的参考材料。

常见动作：

```text
/beeweave-url-capture <url>
/beeweave-article-writer
/beeweave-social-writer
/beeweave-article-publisher
```

## vault：知识库

`vault/` 是 BeeWeave 编译出的稳定知识层，可以直接用 Obsidian 打开，也可以作为 Agent 查询和上下文复用的来源。

当前主要结构：

- `concepts/`：概念、理论、方法论和心智模型。
- `entities/`：工具、项目、组织、产品等具体对象。
- `skills/`：操作流程和实践知识，不是 Agent Skill 源码。
- `references/`：来源记录、文章批次和事实性材料。
- `synthesis/`：跨主题、跨来源的综合分析。
- `projects/`：项目相关知识。
- `journal/`：时间相关记录和阶段性复盘。
- `_raw/`、`_staging/`、`_archives/`、`_meta/`：BeeWeave 维护流程使用的辅助目录。

常见动作：

```text
/beeweave-ingest workbench/articles/published
/beeweave-query 我对 Agent Loop Engineering 已经知道什么？
/beeweave-update
/beeweave-synthesize
/beeweave-digest
```

## 当前知识主题

这个工作区目前沉淀的重点包括：

- BeeWeave：Agent 原生知识工作台、workbench/vault 架构、skill 安装模型。
- AI Agent 工程：Loop Engineering、Prompt/Context/Harness、生产级 Agent 工作流。
- Human-in-the-loop：审批、反馈、人工接管和系统安全边界。
- GoHumanLoop：LangGraph、CrewAI、企业微信审批等具体集成路径。
- 创作方法：从素材到文章，再从文章回流成可复用知识。
- AI 模型竞赛：scale law、预训练规模和 2026 下半年模型竞争判断。

入口索引：

```text
vault/index.md
vault/hot.md
```

## 推荐工作流

1. 捕获素材：把网页、链接、文章、对话或临时想法放入 `workbench/inbox/`。
2. 组织创作：在 `workbench/articles/drafts/` 中写草稿，或用写作 skill 生成初稿。
3. 发布内容：定稿后进入 `workbench/articles/published/`。
4. 沉淀知识：用 `beeweave-ingest` 或 `beeweave-update` 把高价值内容转成 vault 页面。
5. 复用上下文：通过 `beeweave-query`、`beeweave-digest`、`beeweave-context-pack` 把已有知识带回下一轮任务。

## 使用约定

- 新素材先进入 `workbench/`，不要直接堆进 `vault/`。
- 进入 `vault/` 的内容应当是稳定、可复用、可链接的知识。
- 已发布文章是高信号输入，优先从 `workbench/articles/published/` ingest。
- 本工作区内的路径引用优先使用相对路径，避免绑定本机绝对目录。
- Agent 协作时遵守 `AGENTS.md`，尤其是中文输出、变更可追溯和质量验证。
- BeeWeave 源码或工具行为需要调整时，到 `../beeweave` 中修改；不要把源码仓库内容复制进当前工作区。
