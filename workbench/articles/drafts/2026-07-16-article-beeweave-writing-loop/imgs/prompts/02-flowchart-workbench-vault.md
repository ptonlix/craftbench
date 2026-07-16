---
illustration_id: 02
type: flowchart
style: screen-print
palette: warm
language: zh
aspect_ratio: "16:9"
---

Workbench 与 Vault 双层记忆架构图

Layout: 16:9 横向上下双层架构。上层约 48% 为 Workbench 创作现场，下层约 38% 为 Vault 稳定知识层，中间约 14% 是双向流动通道。整体像一座剖开的双层工作台。

ZONES:
- 上层 Workbench，包含四个大图标和短标签：网页素材、文章草稿、配图提示词、过程 trace。元素略显活跃和未完成，用散落纸张与修订线表现创作现场
- 中间通道，向下箭头标注：ingest / update，向上箭头标注：query / context
- 下层 Vault，包含四个整齐归档的知识模块：概念、实体、方法、项目知识。用书库、卡片盒和连接节点表现稳定可复用
- 右侧增加一个小型循环箭头，从 Vault 回到下一篇草稿

LABELS:
- 只显示：Workbench、创作现场、网页素材、文章草稿、配图提示词、过程 trace、ingest / update、query / context、Vault、稳定知识、概念、实体、方法、项目知识
- 中文必须准确清晰，英文仅保留以上命令词

COLORS:
- 暖米色背景 #F5E6D0
- 暖橙色 #E8751A 表现 Workbench 的活动与生成
- 金黄色 #F4A623 表现输入和创意
- 深棕色 #4A2C20 表现结构、文字和 Vault
- 猩红色 #C0392B 只标示从草稿直接污染 Vault 的禁止路径，画一个小叉号
- 色值仅用于渲染，不得成为可见文字

STYLE:
- Screen print / silkscreen poster infographic
- 上下层用粗几何框架和负空间区分
- 半色调网点、纸张颗粒、轻微套色偏移，平面色块，无渐变
- 图标简洁，最多五种颜色，不使用写实照片、3D 或复杂界面截图
- 中文大而易读，短标签，不写长句
- Clean composition with generous white space

ASPECT: 16:9, 2K, medium complexity.
