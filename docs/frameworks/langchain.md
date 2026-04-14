# LangChain

## What It Is

LangChain is a general-purpose application framework for working with language models, tools, prompts, chains, and lightweight agents.

In this repository, treat LangChain as the most direct starting point when the problem is mostly:

- model calls
- prompt composition
- tool integration
- simple agent loops
- basic retrieval pipelines

## Best For

- straightforward tool-calling assistants
- prompt and model orchestration without custom graph logic
- reusable model, tool, and output-parsing primitives
- quick prototypes that should stay easy to read

## Not Ideal For

- complex branching, retry loops, or custom state machines
- long-running agent systems with files, delegation, and persistent memory
- retrieval-heavy systems where indexing and data access are the hardest problem

## Core Concepts

The most important mental model is that LangChain gives you building blocks first:

- models
- prompts
- tools
- output parsers
- retrievers
- simple agents

This makes it flexible and approachable, but it also means you often need another layer when orchestration or data access becomes the real challenge.

## How It Fits In This Repository

Use LangChain when you want the lightest framework that still gives you a real app structure.

In the current skill tree, the main LangChain entry points are:

- [langchain-dependencies](../../.agents/skills/langchain-dependencies/SKILL.md)
- [langchain-fundamentals](../../.agents/skills/langchain-fundamentals/SKILL.md)
- [langchain-middleware](../../.agents/skills/langchain-middleware/SKILL.md)
- [langchain-rag](../../.agents/skills/langchain-rag/SKILL.md)

## Relationship to Other Frameworks

- Compared with [LangGraph](./langgraph.md), LangChain is simpler and less explicit about orchestration.
- Compared with [Deep Agents](./deep-agents.md), LangChain is much lighter but far less batteries-included.
- Compared with [LlamaIndex](./llamaindex.md), LangChain is broader as an app framework but less specialized for retrieval and document/data systems.

## Common Upgrade Path

Start with LangChain and move up only when a real boundary appears:

- move to LangGraph when control flow becomes the hard part
- move to Deep Agents when long-running execution and delegation become the hard part
- add LlamaIndex when retrieval, indexing, or document intelligence become the hard part

## Where To Go Next

- Read [LangGraph](./langgraph.md) if you expect branching, loops, or persistence.
- Read [LlamaIndex](./llamaindex.md) if your task centers on RAG or private-data retrieval.
- Read [LangChain vs LlamaIndex](../comparisons/langchain-vs-llamaindex.md) if both seem plausible.
- Read [When to Use What](../selection/when-to-use-what.md) for cross-framework selection guidance.
