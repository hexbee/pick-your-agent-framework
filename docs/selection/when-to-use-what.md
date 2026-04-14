# When to Use What

## Purpose

This page is the practical selection guide for the frameworks currently covered in this repository.

Use it when you know roughly what you want to build, but you are not yet sure which framework should be your starting point.

## Quick Rule

| If the hardest part is... | Start here |
|---------------------------|------------|
| model and tool composition | LangChain |
| orchestration, loops, and state | LangGraph |
| long-running execution, planning, files, delegation | Deep Agents |
| retrieval, indexing, parsing, private-data access | LlamaIndex |

## Scenario Guide

### Use LangChain when

- you want a simple assistant or agent
- you mostly need models, prompts, and tools
- you do not yet need custom graph orchestration

### Use LangGraph when

- the application needs explicit branching
- the flow includes retries, reflection, or fan-out/fan-in
- state transitions are part of the core design

### Use Deep Agents when

- tasks are long-running and open-ended
- the system should manage files as working memory
- planning and subagent delegation are core requirements

### Use LlamaIndex when

- the app lives or dies on retrieval quality
- private data access is the central feature
- documents, parsing, extraction, or graph/data retrieval dominate the design

## Combination Patterns

### LangGraph + LlamaIndex

Use this when custom orchestration sits on top of a strong retrieval layer.

### Deep Agents + LlamaIndex

Use this when a long-running agent system needs a serious private-data backend.

### LangChain + LlamaIndex

Use this when the app shell is simple, but retrieval still deserves a dedicated framework.

## Common Mis-Selections

- choosing LangChain when the real problem is document retrieval quality
- choosing LlamaIndex when the app barely has a data layer
- choosing LangGraph too early for a problem that could stay simple
- choosing Deep Agents for a task that is not actually long-running or open-ended

## Suggested Reading Order

- Read [LangChain](../frameworks/langchain.md)
- Read [LangGraph](../frameworks/langgraph.md)
- Read [Deep Agents](../frameworks/deep-agents.md)
- Read [LlamaIndex](../frameworks/llamaindex.md)
- Read [LangChain vs LlamaIndex](../comparisons/langchain-vs-llamaindex.md)

## Skill Entry Points

For the current skill-based routing logic, start here:

- [framework-selection](../../.agents/skills/framework-selection/SKILL.md)
- [framework-selection reference matrix](../../.agents/skills/framework-selection/references/selection-matrix.md)

If the first answer is LlamaIndex, continue here:

- [llamaindex-selection](../../.agents/skills/llamaindex-selection/SKILL.md)
