# Deep Agents

## What It Is

Deep Agents is an opinionated agent framework for long-running, open-ended tasks that need planning, files, memory, delegation, and skills.

In this repository, treat Deep Agents as the highest-level execution framework among the currently covered options.

## Best For

- long-running research or coding tasks
- agents that need files as working memory
- subagent delegation
- task planning and todo tracking
- systems that should load skills on demand

## Not Ideal For

- small assistants where a simple tool loop is enough
- cases where you want total control over every orchestration edge
- cases where the main problem is retrieval architecture instead of execution behavior

## Core Concepts

The most important Deep Agents ideas are:

- planning middleware
- filesystem-backed context
- subagents
- skills
- optional long-term memory
- human approval for risky actions

You configure these capabilities instead of building them from scratch.

## How It Fits In This Repository

Use Deep Agents when the problem is bigger than "call a model and maybe some tools."

In the current skill tree, the main Deep Agents entry points are:

- [deep-agents-core](../../.agents/skills/deep-agents-core/SKILL.md)
- [deep-agents-memory](../../.agents/skills/deep-agents-memory/SKILL.md)
- [deep-agents-orchestration](../../.agents/skills/deep-agents-orchestration/SKILL.md)

## Relationship to Other Frameworks

- Compared with [LangChain](./langchain.md), Deep Agents is much more opinionated and much more capable for long-running tasks.
- Compared with [LangGraph](./langgraph.md), Deep Agents gives you built-in system behavior instead of low-level orchestration control.
- Compared with [LlamaIndex](./llamaindex.md), Deep Agents is an execution framework, while LlamaIndex is a retrieval and data framework.

## Common Upgrade Path

Use Deep Agents as the top-level system when you need:

- planning
- files
- delegation
- long-lived execution

Then add:

- LangGraph for tightly controlled subflows
- LlamaIndex for retrieval over documents, data stores, or knowledge bases

## Where To Go Next

- Read [LangGraph](./langgraph.md) if you need finer orchestration control.
- Read [LlamaIndex](./llamaindex.md) if the agent needs strong RAG or document retrieval.
- Read [When to Use What](../selection/when-to-use-what.md) for cross-framework recommendations.
