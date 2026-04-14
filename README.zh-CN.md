# pick-your-agent-framework

[English](./README.md) | [简体中文](./README.zh-CN.md)

一个面向 AI Agent Framework 的实用指南与 Codex Skills 仓库，用来帮助你理解、比较并选择合适的框架。

这个仓库主要服务两件事：

- 帮助开发者根据问题类型选择合适的框架
- 围绕这些框架组织可复用的 Codex Skills

它是一个强调选型、强调对比、并且为后续扩展预留了清晰结构的仓库。

## 为什么会有这个仓库

Agent 生态发展很快，但很多框架讨论最后都会变成模糊的判断，比如“最适合做 Agent”或者“最适合生产环境”。

这个仓库希望用更实用的方式来处理这个问题：

- 解释每个框架真正擅长什么
- 说明不同框架的重叠点和边界
- 提供可复用的选型启发，而不是泛泛的排名
- 把这些经验整理成可直接触发的 Codex Skills

目标不是选出唯一赢家，而是让框架选型更清晰、更稳定、更容易复用。

## 当前覆盖范围

仓库目前覆盖以下几类框架：

| 框架 | 最适合的场景 |
|------|--------------|
| LangChain | 模型调用、工具调用、chains、简单 agent、通用基础构件 |
| CrewAI | 以 Flow 为中心的自动化、角色化 agent 团队、tasks/processes、生产工作流 |
| LangGraph | 显式编排、分支、循环、持久化、人类介入 |
| Deep Agents | 长时运行的 agent 系统，包括规划、文件、委派与记忆 |
| LlamaIndex | RAG、索引、文档智能、图与数据检索、数据中心型 agent |

这些内容既体现在框架选型逻辑里，也体现在 `.agents/skills/` 下的 skill 体系里。

## 快速选型指南

可以先用下面这条粗粒度规则判断起点：

| 如果最难的问题是…… | 优先从这里开始 |
|--------------------|----------------|
| 模型与工具组合 | LangChain |
| 以 Flow 为中心的自动化与角色化 agent 协作 | CrewAI |
| 编排与状态流转 | LangGraph |
| 长时执行、规划和文件操作 | Deep Agents |
| 检索、索引、解析或私有数据问答 | LlamaIndex |

当前顶层选型逻辑可以看：

- [framework-selection](./.agents/skills/framework-selection/SKILL.md)
- [framework-selection 参考矩阵](./.agents/skills/framework-selection/references/selection-matrix.md)

如果第一层判断结果是 `LlamaIndex`，下一层细分可以看：

- [llamaindex-selection](./.agents/skills/llamaindex-selection/SKILL.md)

如果第一层判断结果是 `CrewAI`，下一层细分可以看：

- [crewai-selection](./.agents/skills/crewai-selection/SKILL.md)

## 这个仓库里有什么

这个仓库目前包含：

- 顶层框架选型 skills
- 各框架对应的 skill 套件
- 针对 RAG、workflows、observability、graph retrieval 等方向拆分的子 skill 树
- 为未来框架介绍、框架对比、选型文档预留的结构

它现在已经可以作为一个实用的 skill 仓库使用，同时也在逐步演进成一个更完整的框架比较与选型资源库。

## 当前 Skill 地图

当前 skill 体系主要分成这些组：

- 顶层选型 skills
- CrewAI skills
- LangChain skills
- LangGraph skills
- Deep Agents skills
- LlamaIndex skills

完整的当前 skill 清单可以看：

- [docs/selection/skill-map.md](./docs/selection/skill-map.md)
- [docs/selection/skill-map.zh-CN.md](./docs/selection/skill-map.zh-CN.md)

## 仓库结构

这个仓库的结构把“可复用的 skills”和“后续逐步扩展的文档”分开组织：

```text
.
├── .agents/
│   └── skills/
│       ├── framework-selection/
│       ├── crewai-*/
│       ├── langchain-*/
│       ├── langgraph-*/
│       ├── deep-agents-*/
│       └── llamaindex-*/
├── docs/
│   ├── frameworks/
│   ├── comparisons/
│   ├── selection/
│   └── superpowers/specs/
└── README.md
```

### 各目录放什么

- `.agents/skills/`：可复用的 Codex Skills 以及它们的 reference 文档
- `docs/frameworks/`：各框架的介绍与更深入的框架说明
- `docs/comparisons/`：框架对比、取舍和 side-by-side 分析
- `docs/selection/`：选型启发、决策树、场景化推荐
- `docs/superpowers/specs/`：设计 spec 和规划文档

## 为扩展而设计

这个仓库从一开始就预留了以下扩展空间：

- 更多框架家族
- 更完整的框架介绍
- 更多横向对比文档
- 更多真实场景下的选型启发
- 更多按框架拆分的 skill 套件

未来可能会加入的框架包括 AutoGen、PydanticAI 等，但这里提到它们只是说明扩展方向，不代表已经承诺全部覆盖。

## 如何继续扩展

如果后续要新增一个框架家族，建议按下面的顺序做：

1. 更新顶层选型逻辑
2. 在 `.agents/skills/` 下新增对应的 skill 或 skill 套件
3. 在 `docs/frameworks/`、`docs/comparisons/` 或 `docs/selection/` 下补更深入的文档
4. 回到 README 更新摘要和 skill 地图

尽量让 README 保持高信息密度，但不要把所有细节都堆在首页。更深入的内容应该沉到 skills 和 docs 里。

## 当前方向

目前这个仓库最强的价值在于：

- 一个实用的框架选型 skill 库
- 一个结构化的框架对比入口
- 一个可以持续长出更多框架介绍与取舍文档的仓库基础

下一步最自然的扩展方向是：

- 在 `docs/frameworks/` 下补每个框架的介绍
- 在 `docs/comparisons/` 下补更具体的框架对比
- 在 `docs/selection/` 下补更贴近真实场景的选型建议
