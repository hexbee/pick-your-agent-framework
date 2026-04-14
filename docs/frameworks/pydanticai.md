# Pydantic AI

## What It Is

Pydantic AI is a Python-first agent framework built around typed outputs, explicit tool wiring, dependency injection, and production-oriented ergonomics.

In this repository, treat Pydantic AI as the strongest option when the goal is to build a typed Python agent service without starting from a graph-first orchestration model.

## Best For

- typed agent responses backed by Pydantic models
- Python services that want explicit tool and dependency boundaries
- request-scoped context passed through the app, not hidden globals
- production-oriented tracing, evaluation, and durable execution
- tool-driven assistants where agent ergonomics matter more than custom graph control

## Not Ideal For

- graph orchestration, loops, and state machines as the main design problem
- retrieval-heavy systems where indexing and document access dominate the architecture
- long-running systems centered on files, planning, and subagent delegation
- role/task/crew workflows as the primary abstraction

## Core Concepts

The main Pydantic AI mental model is:

- define an `Agent`
- give it `instructions`
- use `output_type` when structure matters
- add function tools or toolsets when capability is needed
- pass request-scoped data through `deps_type` and `RunContext`
- use message history intentionally
- instrument and evaluate the system as it matures

This gives Pydantic AI a strong center of gravity around typed Python application design.

## How It Fits In This Repository

Pydantic AI is covered as a full framework family with four focused skills:

- [pydanticai-dependencies](../../.agents/skills/pydanticai-dependencies/SKILL.md)
- [pydanticai-fundamentals](../../.agents/skills/pydanticai-fundamentals/SKILL.md)
- [pydanticai-tools-mcp](../../.agents/skills/pydanticai-tools-mcp/SKILL.md)
- [pydanticai-production](../../.agents/skills/pydanticai-production/SKILL.md)

Start with dependencies when setup is still unclear. Otherwise start with fundamentals and branch only when tools/MCP or production concerns become the real bottleneck.

## Relationship to Other Frameworks

- Compared with [LangChain](./langchain.md), Pydantic AI is more opinionated around typed Python agents and dependency injection.
- Compared with [LangGraph](./langgraph.md), Pydantic AI is less about explicit orchestration and more about a strong default agent surface.
- Compared with [LlamaIndex](./llamaindex.md), Pydantic AI is less retrieval-centric and better framed as an app/service shell for agents.
- Compared with [Agno](./agno.md), Pydantic AI is narrower and lighter, not an integrated agents-plus-runtime stack.

## Common Upgrade Path

Start with Pydantic AI when:

- the app is Python-first
- structured outputs matter
- tools and request-scoped context should be explicit
- tracing and evaluation should fit cleanly into the app lifecycle

Then add:

- LlamaIndex if retrieval and private-data access become the hard backend problem
- LangGraph only if explicit orchestration and graph control become the real challenge
- Deep Agents only if the top-level task grows into long-running, file-centered delegated work

## Where To Go Next

- Read [When to Use What](../selection/when-to-use-what.md) for cross-framework routing.
- Browse the Pydantic AI skill family through [pydanticai-fundamentals](../../.agents/skills/pydanticai-fundamentals/SKILL.md) and adjacent skills.
