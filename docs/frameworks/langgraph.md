# LangGraph

## What It Is

LangGraph is a framework for explicit orchestration of LLM applications through graph-based control flow.

In this repository, treat LangGraph as the right tool when the system needs custom execution logic, not just model calls or tool use.

## Best For

- branching workflows
- loops and retries
- stateful multi-step execution
- human-in-the-loop checkpoints
- fan-out and fan-in orchestration

## Not Ideal For

- the simplest assistants where a direct LangChain agent is enough
- long-running systems where planning, files, and delegation should be built in
- retrieval-first systems where indexing and data design dominate the problem

## Core Concepts

The core LangGraph model is:

- state
- nodes
- edges
- conditional routing
- persistence

The graph is the application logic. That is the key difference from lighter frameworks.

## How It Fits In This Repository

Use LangGraph when the hardest part is getting the control flow right.

In the current skill tree, the main LangGraph entry points are:

- [langgraph-fundamentals](../../.agents/skills/langgraph-fundamentals/SKILL.md)
- [langgraph-human-in-the-loop](../../.agents/skills/langgraph-human-in-the-loop/SKILL.md)
- [langgraph-persistence](../../.agents/skills/langgraph-persistence/SKILL.md)

## Relationship to Other Frameworks

- Compared with [LangChain](./langchain.md), LangGraph gives you explicit orchestration instead of a simpler agent loop.
- Compared with [Deep Agents](./deep-agents.md), LangGraph gives you more control but fewer built-in system features.
- Compared with [LlamaIndex](./llamaindex.md), LangGraph is stronger at orchestration, while LlamaIndex is stronger at retrieval and data workflows.

## Common Upgrade Path

Start with LangGraph when you already know the flow will branch, loop, or need durable state.

Combine it with:

- LangChain for model and tool primitives
- LlamaIndex when the graph needs strong retrieval or document pipelines
- Deep Agents only when the top-level problem grows into a broader long-running agent system

## Where To Go Next

- Read [Deep Agents](./deep-agents.md) if you need planning, files, and delegation.
- Read [LlamaIndex](./llamaindex.md) if the graph should sit on top of a stronger retrieval layer.
- Read [When to Use What](../selection/when-to-use-what.md) for scenario-based routing.
