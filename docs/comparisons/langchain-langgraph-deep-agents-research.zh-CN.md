# LangChain / LangGraph / Deep Agents 横纵分析调研

> 截止时间：2026-04-14  
> 研究对象：LangChain 出品的三层 Agent 框架栈 `LangChain / LangGraph / Deep Agents`  
> 说明：本文把这三个对象视为同一技术家族中的三个层级，而不是三个彼此正面竞争的独立产品。这个判断来自它们当前官方文档的分工表述，以及本仓库现有的选型矩阵。

## 先说结论

如果只用一句话概括，这三者的演化，其实就是 LangChain 对“Agent 工程化”难题的一次逐层加码：

- `LangChain` 解决的是“先把模型、工具和应用原语拼起来”
- `LangGraph` 解决的是“原语拼起来以后，真正难的是状态、持久化、分支、恢复和人类介入”
- `Deep Agents` 解决的是“就算有了运行时，很多复杂任务仍然需要一套更像 Claude Code / Deep Research 的现成 agent harness”

因此，研究这三个框架，最重要的不是问“谁更强”，而是看 LangChain 团队如何随着行业瓶颈的变化，把自己的重心从“抽象层”一路推到“运行时层”，再推到“agent harness 层”。这也是它们今天最核心的竞争优势：不是单点最好，而是提供了一条从轻量原语到重型执行系统的连续升级路径。

---

## 一、纵向分析：从“可组合原语”到“运行时”再到“harness”

### 1. 起点不是 Agent，而是“让 LLM 应用可编程”

LangChain 的原点，和今天很多人对“Agent 框架”的想象并不一样。它不是从“多智能体”或“自治执行”起家，而是从一个更早也更朴素的问题起家：2022 年底，GPT 类模型突然可用之后，开发者很快发现，调用模型本身不难，难的是怎么把 prompt、外部工具、文档检索、记忆和输出格式组织成一个可以重复使用的应用结构。

`langchain-ai/langchain` GitHub 仓库创建于 **2022-10-17**。这个时间点很关键：它比 ChatGPT 的大众爆发还略早，说明最初的 LangChain 更像是“面向早期 LLM 应用开发者的工程抽象”，而不是后来的“Agent 平台”。官方在更早的对外叙事里把 LangChain描述为“通过可组合性来构建 LLM 应用”，这基本定义了它第一阶段的精神气质：先把组件抽象出来，让开发者能搭东西。  

这也解释了 LangChain 为什么早期声量会那么大。它踩中的不是某一个窄场景，而是整波 LLM 应用开发的共性痛点：模型会换，向量库会换，工具会换，但“需要一个统一应用层”这件事不会消失。

### 2. 2023：爆红、扩张、商业化，也埋下了“抽象过重”的种子

LangChain 的第一阶段增长非常像 AI 基础设施公司在 2023 年的标准轨迹：开源先爆红，随后迅速公司化。LangChain 官方在 2023 年的种子轮公告里写得很直白：从第一个版本发布算起，不过六个月，节奏已经快得像过了几年。这个表述并不夸张。2023 年的开源 Agent 生态本来就被 AutoGPT、BabyAGI、向量数据库、RAG Demo 推着狂奔，LangChain 恰好成了“默认集成层”。

这时的 LangChain 有两股力量同时把它往前推。

- 第一股力量来自开发者市场。大家需要一个足够通用的工具箱，能同时接模型、提示词、检索、Agent、Memory。
- 第二股力量来自商业化。LangChain 不满足于做一个开源包，而是很快把重心延伸到 LangSmith 这类可观测、测试和部署能力上。

2024-02-15，LangChain 宣布 **LangSmith GA** 和 **2500 万美元 Series A**。这不是一个普通融资节点，而是一个叙事转折点：LangChain 开始把自己从“开源抽象库”重新描述成“面向生产环境的 LLM/Agent 工程平台”。如果说 2023 年的 LangChain 在解决“怎么搭起来”，那么 2024 年它已经开始解决“怎么把这种东西真正上线并持续改进”。

但问题也在这一阶段被放大了。LangChain 的优点是覆盖面广，代价是概念面也会越铺越大。社区里对 LangChain 的典型吐槽，几乎从 2023 年就已经成型：抽象层次多、API 变化快、文档和包结构经常调整、简单事情有时也会被包进一套偏重的 mental model。官方后续对 `langchain` 1.0 的“重写”与“聚焦”叙事，某种意义上正是在修这笔历史账。

### 3. LangGraph 的出现，是 LangChain 对自己第一阶段局限的正面回应

`langchain-ai/langgraph` 仓库创建于 **2023-08-09**。这个时间点非常值得玩味。它说明 LangChain 团队在 2023 年中后期就已经意识到：真正难的不是“把模型和工具串起来”，而是当 Agent 开始进入生产环境后，开发者需要的是一种更底层的运行时能力。

LangGraph 当前官方文档的定位非常清晰：它是一个 **low-level orchestration framework and runtime**，重点不是 prompt，不是现成 agent，而是长期运行、带状态、可恢复、可人为打断和检查的执行系统。官方甚至明确提醒：如果你只是刚开始做 agent，或者想要更高层抽象，应该先用 LangChain 的 prebuilt agents；LangGraph 专注的是 orchestration 本身。

这背后是 2024 年 Agent 工程现实的一次校正。早期社区很容易把 Agent 理解成“模型 + 工具循环”，但一旦进入真实业务，问题马上变成：

- 失败了从哪一步恢复？
- 人工审批插在哪里？
- 状态怎么跨轮次保存？
- 多分支流程如何调试？
- 长任务怎么追踪和部署？

也就是说，LangGraph 的诞生不是为了取代 LangChain，而是为了给 LangChain 提供一个它此前缺少的底座。它把 LangChain 家族从“抽象库”推进到了“运行时系统”。

这也是为什么 2025 年官方开始越来越频繁地用“framework / runtime / harness”这组词来区分三层角色。它们不是营销修辞，而是产品边界被真实工程压力逼出来之后的再命名。

### 4. 2024 到 2025：LangChain 从“工具箱公司”变成“Agent Engineering 公司”

如果把 2023 年看成 LLM 应用工具链爆发年，那么 2024-2025 年就是 LangChain 把“Agent 工程”正式制度化的阶段。

2025-05-14，LangChain 宣布 **LangGraph Platform 正式 GA**。这意味着它不再只是一个开源 graph 框架，而是已经开始与部署、可观测和生产工作流深度绑定。到了 **2025-10-22** 的 1.0 节点，官方表述更进一步：`langchain` 被“完全重写”为一个更有主见、更聚焦、并且**由 `langgraph` runtime 驱动**的框架；LangGraph 则被稳稳放在底层运行时位置。

2025 年的另一个关键信号来自商业叙事。LangChain 在 Series B 公告里明确提出自己在建设的是 **platform for agent engineering**，并给出非常清晰的三层结构：

- `LangChain`：帮助开发者快速起步，提供更高层的常见 agent 架构
- `LangGraph`：提供低层 orchestration、memory、human-in-the-loop、durable execution
- `LangSmith`：负责观测、评估、部署和生产闭环

这一版叙事比早年成熟得多。它等于承认了一个事实：Agent 开发不是“写 prompt + 接工具”就结束，而是一整套围绕非确定性系统展开的工程学。而 LangChain 想占据的，不再只是 open-source 入口，而是这整条工程链路的标准位置。

### 5. Deep Agents：从“runtime”再向上长出一层现成 harness

到 2025 年中，行业又发生了一次变化。大家开始发现，哪怕有 LangGraph 这样的运行时，复杂任务 agent 仍然需要很多“约定俗成但又非常关键”的做法：规划、todo list、子代理、文件系统工作区、上下文压缩、长期记忆、权限和人类审批。Claude Code、OpenAI Deep Research、Manus 之类产品之所以让人感觉“更能干”，不是因为底层 loop 完全不同，而是它们在 loop 外面包了一层更适合长任务的执行 harness。

LangChain 对这个趋势的回应，就是 **Deep Agents**。

`langchain-ai/deepagents` 仓库创建于 **2025-07-27**。仅三天后，2025-07-30，Harrison Chase 在博客里发表《Deep Agents》，明确把“deep agents”定义为一类能够在更长时间跨度上规划和执行复杂任务的 agent，并点名其灵感来自 Claude Code、OpenAI 的 Deep Research 和 Manus。文章非常坦率：所谓 deep，不是换了什么神秘算法，核心 loop 仍然是“LLM 调工具”；真正拉开差距的，是详细系统提示、规划工具、子代理、文件系统这四件事。

这篇文章很重要，因为它揭示了 Deep Agents 的产品哲学：它不是再造一个新 runtime，而是在 LangGraph 之上，总结出一套更适合复杂任务的“默认做法”。换句话说，LangGraph 解决的是“你可以怎么搭”；Deep Agents 解决的是“如果你懒得自己搭一遍，这里先给你一套更像现代 coding/research agent 的现成 harness”。

官方文档今天也明确承认这一点：Deep Agents 是一个 **standalone library built on top of LangChain’s core building blocks**，同时使用 **LangGraph runtime** 提供 durable execution、streaming、human-in-the-loop 等能力。它当前官方首页几乎就是在列它帮你内置了什么：

- 任务规划与 `write_todos`
- 文件系统作为上下文管理层
- `execute` 支持 shell 执行
- 子代理隔离上下文
- 跨会话长期记忆
- 权限规则
- 可复用 skills
- 智能默认 prompt

到了 2025-10-30，Deep Agents CLI 发布，LangChain 已经不满足于让它停留在 SDK，而是把它推进到终端 agent 场景，直接对接 coding、research 和 agent-building 工作流。这一步很像从“框架能力”走向“可直接操作的产品入口”。

### 6. 今天的状态：不是三个框架争一个位置，而是一条分层升级路线

截至 **2026-04-14**，这三个项目在 GitHub 上的公开体量大致是：

- `langchain`: 创建于 2022-10-17，约 13.3 万 stars
- `langgraph`: 创建于 2023-08-09，约 2.9 万 stars
- `deepagents`: 创建于 2025-07-27，约 2.0 万 stars

这组数据本身就很能说明问题。

LangChain 仍然是流量入口和认知入口；LangGraph 是真正把系统推向生产复杂度的技术中枢；Deep Agents 则是增长最快、概念最贴近当代“coding agent / deep research agent”想象的上层包装。  

官方当前文档也把三者并列放在同一开源导航里，但分工写得很明白：

- LangChain 是高层 framework
- LangGraph 是低层 orchestration runtime
- Deep Agents 是建立在前两者之上的 harness

这意味着 LangChain 团队并没有让这三个东西互相内耗，而是在主动制造“向上升级但不出生态”的迁移路径。用户可以从轻量 agent 起步，进入 stateful orchestration，再进入 complex-task harness，而不用换生态、换文档体系、换 tracing 与 deployment 体系。这种连贯性，是它们今天最强的战略资产。

---

## 二、横向分析：作为一个“分层 Agent 家族”，它在和谁竞争？

### 先判断竞品场景

这里属于**场景 C：竞品充分**。  

如果把 `LangChain / LangGraph / Deep Agents` 看成一个三层技术家族，那么它面对的并不是单一竞品，而是几类不同逻辑的对手：

- 更强调类型边界与 Python 服务体验的 `Pydantic AI`
- 更强调 flow、role、task 的 `CrewAI`
- 更强调一体化 agents + runtime 栈的 `Agno`
- 更强调数据与检索层的 `LlamaIndex`

从仓库已有资料看，这四类正好分别代表了几种很典型的选型重心，也能更清楚地照出 LangChain 家族的生态位。

### 1. 与 Pydantic AI 对比：宽平台 vs 强边界的 Python agent 服务

Pydantic AI 的吸引力不在“层次很多”，恰恰在于它把边界划得很清楚。它特别适合 Python 后端团队：结构化输出、显式工具、依赖注入、请求级上下文，这些概念和传统 Web 服务开发的习惯高度一致。  

跟它相比，LangChain 家族的长处是“纵深更完整”。你可以从 `create_agent` 走到 LangGraph，再走到 Deep Agents，几乎把从简单 agent 到复杂执行系统的路线都包了。问题也在这里：它的学习面更宽，概念切换更多，团队如果只是想做一个“类型清楚、工具边界清楚”的 Python agent 服务，很可能觉得 Pydantic AI 更顺手。

用户为什么会选 Pydantic AI？真实理由通常不是“它功能更多”，而是“它更像我熟悉的 Python 应用框架”。用户为什么会选 LangChain 家族？则往往是因为它给了更大的上升空间，尤其当项目未来可能走向复杂编排、运行时控制和更长任务时，Pydantic AI 的优势就没那么明显了。

一句话说，Pydantic AI 赢在“干净”，LangChain 家族赢在“梯子长”。

### 2. 与 CrewAI 对比：flow-first 团队协作 vs 分层执行栈

CrewAI 的世界观非常鲜明：agent 是“角色”，工作是“任务”，系统是“flow”。这种建模方式对业务自动化团队很友好，因为它贴近组织分工，也贴近很多人理解多智能体的直觉。

而 LangChain 家族并不试图把所有人都拉进“角色化团队协作”的叙事里。它的做法更工程化一些：先给原语，再给运行时，再给 harness。这样做的好处是弹性更强，坏处是起步时不如 CrewAI 那样直观。  

用户为什么会偏爱 CrewAI？往往因为它在“我已经知道我要一个 flow 和一组 agent 角色”这个前提下，非常好讲、也非常好卖。用户为什么会更偏向 LangChain 家族？通常是因为他们担心系统后面会复杂到需要 durable execution、state、debugging、deployment 和更底层控制。CrewAI 更像一套 workflow 产品思维，LangChain 家族更像一套逐层下钻的工程思维。

### 3. 与 Agno 对比：一体化单栈 vs 有意分层

Agno 的优势，在于它试图把 agent、team、workflow、memory、knowledge、runtime 管理都放进一套比较统一的表面。对于不想在“框架、运行时、harness、观测层”之间来回切换概念的团队，这非常有吸引力。

LangChain 家族则几乎反着来。它承认不同层有不同问题，所以宁可把它们拆开讲，也不把一切塞进一个统一 API 表面。这会带来更高的概念成本，但也带来更强的可替换性与更清晰的技术边界。

换句话说，Agno 更像“我希望一站式待在这里”；LangChain 家族更像“你可以一路往上升，但每一层都知道自己在解什么问题”。  

对很多成熟团队来说，后者更像工程系统；对很多想快速上手的团队来说，前者更像产品系统。

### 4. 与 LlamaIndex 对比：执行家族 vs 数据家族

严格说，LlamaIndex 不是 LangChain 家族最直接的正面对手，因为两者的主轴不同。LlamaIndex 的中心是检索、索引、文档解析、图与数据访问；LangChain 家族的中心是 agent 的执行、编排和运行时。

但二者经常在真实项目里被拿来一起比较，因为用户常常一开始并不知道自己的 hardest problem 究竟是“让 agent 会做事”，还是“让 agent 拿到靠谱的数据”。  

如果难点主要在 RAG、文档理解、知识库质量，LlamaIndex 往往更像正解。  
如果难点主要在状态流转、工具循环、长任务执行和 agent 系统工程化，LangChain 家族更像正解。  

这也是为什么在本仓库的选型矩阵里，LlamaIndex 经常被放在“检索层”，而 LangGraph / Deep Agents 经常被放在“执行层”。它们最常见的关系不是二选一，而是组合。

### 5. 用户视角：这套家族最常被夸什么，又最常被骂什么？

把官方叙事放到一边，用户对 LangChain 家族的真实感受其实很稳定。

最常见的优点有四个：

- 生态最宽，几乎任何模型、工具、部署或 tracing 讨论都绕不开它
- 升级路径清楚，小项目可以从 LangChain 起步，复杂后上 LangGraph，再往上套 Deep Agents
- 生产化意识强，尤其在 observability、deployment、human-in-the-loop、durable execution 这些问题上，LangGraph 把很多别家只在 PPT 里的东西做成了正式能力
- Deep Agents 很贴近当下 coding agent / deep research agent 的“工作手感”，对很多用户来说，比手搓 prompt 和工具 loop 更接近他们想要的东西

最常见的槽点也同样稳定：

- 概念多，层次多，命名和包结构调整频繁，新人很容易迷路
- LangGraph 的低层控制很强，但学习成本也明显更高；社区里有人直接把它形容为在高级图编排上“restrictive and hacky”
- Deep Agents 虽然很抓眼球，但也因为新、快、强依赖上下文工程，给人一种“离最佳实践很近，也离概念包装很近”的感觉

这里有个很有意思的现象：LangChain 团队自己其实是知道这些批评的。从官方 1.0 重写、文档改版，到明确用“framework / runtime / harness”重新划边界，可以看出它在努力把早年“什么都想包进去”的印象，改造成“每一层只解决一类核心问题”。  

这是一个重要信号。很多框架面对复杂性膨胀时，会继续加抽象；LangChain 家族这两年的做法更像是“先承认复杂，再重新分层”。

### 6. 生态位分析：它占的是“连续升级路径”，而不是单点最简洁

如果把当下 Agent 框架赛道画成一张地图，LangChain 家族占据的位置并不是“最易上手”，也不是“最窄最锋利”，而是**最连续的升级路径**。

它的真正护城河主要有三层：

- 第一层是认知入口。LangChain 仍然是很多人接触 agent framework 的第一站。
- 第二层是技术迁移成本。项目一旦从 LangChain 走到 LangGraph，再接 LangSmith，团队通常不太愿意换出生态。
- 第三层是叙事统一性。LangChain 现在讲的是一整套“agent engineering”故事，而不是若干零散功能点。

这也是为什么它的竞争不是“某个 feature 输给别人就结束”。它更像一个平台家族。单点上，Pydantic AI 可能更顺，CrewAI 可能更直观，Agno 可能更一体化，LlamaIndex 在数据层可能更专业；但很少有对手能同时在“原语、运行时、harness、观测、部署”这几层都形成同样连续的路径。

### 7. 趋势判断：机会很大，风险也很具体

这套家族接下来的机会主要在三件事上：

- Agent 应用进一步走向生产，LangGraph 那套 durability、memory、HITL、deployment 会越来越像基础设施
- coding agent 和 deep research agent 继续升温，Deep Agents 有机会成为更多团队的“默认 harness”
- LangChain 继续作为入口，把用户自然分流到更高层的 LangGraph / Deep Agents / LangSmith

但风险也同样明确：

- 如果概念继续膨胀，用户会重新转向更窄、更干净的框架
- Deep Agents 所代表的那层价值，很容易被模型厂商自带 agent、IDE 原生 agent 或更强的 hosted harness 吃掉一部分
- LangGraph 的价值很强，但也决定了它不可能成为最轻量的那个选择；一旦项目复杂度不够，团队会本能地寻找更简单替代品

所以它最好的走法，并不是“让所有人都用最全套栈”，而是继续把升级路径打磨得足够顺滑：小项目别被吓跑，大项目别被逼走。

---

## 三、横纵交汇：这三层栈今天到底处在什么位置，接下来会往哪走？

如果把纵向发展史和横向竞争格局叠在一起看，会发现一个很清楚的脉络：

LangChain 家族的每一次“长新层”，都不是拍脑袋扩品类，而是在追一个新的工程瓶颈。

- 当行业难题是“怎么把 LLM 应用搭起来”时，LangChain 长出来
- 当难题变成“怎么让 agent 在生产里跑得住”时，LangGraph 长出来
- 当难题变成“怎么让 agent 真正处理复杂、长时、开放式任务”时，Deep Agents 长出来

所以它的竞争力，不在于提前预判所有未来，而在于它总能比较快地把“社区里已经出现、但还没被系统化”的做法收编进自己的栈里。LangGraph 是把 agent runtime 正式化；Deep Agents 是把 coding/deep-research style harness 正式化。  

从这个角度看，LangChain 家族今天最像的不是单一框架，而是一个正在成形的 agent engineering 标准栈。

我对它未来两三年的判断是：

第一，`LangChain` 会继续弱化“万能抽象层”形象，强化“高层起步入口”角色。它不会再试图解释一切，而是负责把大多数人先带上桌。  

第二，`LangGraph` 会越来越像真正的核心资产。因为 durable execution、memory、HITL、stateful orchestration 这些东西，一旦 Agent 进入生产，就不是可选项，而是系统边界本身。  

第三，`Deep Agents` 会是增长最快但波动也最大的一层。它最贴近今天市场对“强 agent”的想象，因此增长会很快；但它也最容易被模型厂商自带 agent、IDE 原生能力和 hosted coding/research products 正面冲击。

因此，最值得记住的判断不是“LangChain、LangGraph、Deep Agents 谁会赢”，而是：

**它们本来就是被设计成一起赢的。**  

LangChain 负责入口，LangGraph 负责底座，Deep Agents 负责贴近现代复杂任务的默认执行形态。只要 LangChain 公司还能持续把新的工程瓶颈翻译成清晰分层，这套家族在 Agent 框架版图里就会一直占据一个很难被完全替代的位置。

---

## 参考来源

### 官方文档

1. LangChain Docs, LangChain overview  
   https://docs.langchain.com/oss/python/langchain/overview
2. LangChain Docs, LangGraph overview  
   https://docs.langchain.com/oss/python/langgraph/overview
3. LangChain Docs, Deep Agents overview  
   https://docs.langchain.com/oss/python/deepagents/overview

### 官方博客与公告

4. LangChain 官方种子轮公告  
   https://blog.langchain.com/announcing-our-10m-seed-round-led-by-benchmark/
5. LangSmith GA 与 Series A  
   https://blog.langchain.com/langsmith-ga/
6. LangGraph Platform GA  
   https://blog.langchain.com/langgraph-platform-ga/
7. LangChain 与 LangGraph 1.0 里程碑  
   https://blog.langchain.com/langchain-langgraph-1dot0/
8. Building LangGraph: Designing an Agent Runtime from first principles  
   https://blog.langchain.com/building-langgraph/
9. Deep Agents  
   https://blog.langchain.com/deep-agents/
10. Introducing Deep Agents CLI  
   https://blog.langchain.com/introducing-deepagents-cli/
11. LangChain Series B: platform for agent engineering  
   https://blog.langchain.com/series-b/

### GitHub 仓库与时间快照

12. LangChain repo / GitHub API  
   https://github.com/langchain-ai/langchain  
   https://api.github.com/repos/langchain-ai/langchain
13. LangGraph repo / GitHub API  
   https://github.com/langchain-ai/langgraph  
   https://api.github.com/repos/langchain-ai/langgraph
14. Deep Agents repo / GitHub API  
   https://github.com/langchain-ai/deepagents  
   https://api.github.com/repos/langchain-ai/deepagents

### 社区讨论与用户反馈参考

15. Hacker News: Ask HN: Is it just me or LangChain/LangGraph DevEx horrible?  
   https://news.ycombinator.com/item?id=41530288
16. Hacker News: Agent design is still hard  
   https://news.ycombinator.com/item?id=46013935
17. Hacker News: Agent Skills  
   https://news.ycombinator.com/item?id=46871173

### 本仓库已有资料

18. [framework-selection](../../.agents/skills/framework-selection/SKILL.md)
19. [selection-matrix](../../.agents/skills/framework-selection/references/selection-matrix.md)
20. [LangChain](../frameworks/langchain.md)
21. [LangGraph](../frameworks/langgraph.md)
22. [Deep Agents](../frameworks/deep-agents.md)
23. [Pydantic AI](../frameworks/pydanticai.md)
24. [CrewAI](../frameworks/crewai.md)
25. [Agno](../frameworks/agno.md)
26. [LlamaIndex](../frameworks/llamaindex.md)
