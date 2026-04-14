# pick-your-agent-framework

[English](./README.md) | [简体中文](./README.zh-CN.md)

Practical guidance and Codex skills for understanding, comparing, and choosing AI agent frameworks.

This repository is designed for two jobs:

- help developers decide which framework fits a given problem
- organize reusable Codex skills around those frameworks

It is intentionally opinionated, comparison-driven, and built to expand over time.

## Why This Repository Exists

The agent ecosystem is crowded, and most framework discussions collapse into vague claims like "best for agents" or "best for production."

This repository takes a more practical approach:

- explain what each framework is actually good at
- show where frameworks overlap and where they do not
- provide selection heuristics instead of generic rankings
- package that guidance as reusable Codex skills

The goal is not to crown one winner. The goal is to make framework choice easier, clearer, and more repeatable.

## Current Coverage

The repository currently covers these framework families:

| Framework | Best fit |
|-----------|----------|
| LangChain | model calls, tools, chains, simple agents, general building blocks |
| Pydantic AI | typed Python agents, structured output, explicit tools/dependencies, observability, and durable execution |
| Agno | integrated agents, teams, workflows, memory/knowledge, and runtime operations |
| CrewAI | flow-first automations, role-based agent teams, tasks/processes, production workflows |
| LangGraph | explicit orchestration, branching, loops, persistence, human-in-the-loop |
| Deep Agents | long-running agent systems with planning, files, delegation, and memory |
| LlamaIndex | RAG, indexing, document intelligence, graph/data retrieval, data-centric agents |

These are reflected both in the framework selection guidance and in the skill suite under `.agents/skills/`.

## Quick Selection Guide

Start with this rough rule of thumb:

| If the hardest part is... | Start here |
|---------------------------|------------|
| model/tool composition | LangChain |
| typed Python agents with structured output and explicit tools | Pydantic AI |
| one integrated agent/runtime stack | Agno |
| flow-first automation with role-based agents | CrewAI |
| orchestration and state transitions | LangGraph |
| long-running execution with planning and files | Deep Agents |
| retrieval, indexing, parsing, or private-data QA | LlamaIndex |

For the current top-level routing logic, see:

- [framework-selection](./.agents/skills/framework-selection/SKILL.md)
- [framework-selection reference matrix](./.agents/skills/framework-selection/references/selection-matrix.md)

If the answer is "LlamaIndex", the next layer of routing lives here:

- [llamaindex-selection](./.agents/skills/llamaindex-selection/SKILL.md)

If the answer is "CrewAI", the next layer of routing lives here:

- [crewai-selection](./.agents/skills/crewai-selection/SKILL.md)

If the answer is "Agno", the next layer of routing lives here:

- [agno-selection](./.agents/skills/agno-selection/SKILL.md)

If the answer is "Pydantic AI", start here:

- [pydanticai-dependencies](./.agents/skills/pydanticai-dependencies/SKILL.md) for package and provider setup
- [pydanticai-fundamentals](./.agents/skills/pydanticai-fundamentals/SKILL.md) for the default build path

## What You Will Find Here

This repository currently contains:

- top-level framework selection skills
- framework-specific skill suites
- framework subtrees for focused topics such as RAG, workflows, observability, and graph retrieval
- a growing structure for future framework introductions, comparisons, and selection guides

It is already useful as a skill library today, and it is being shaped to become a more complete framework comparison resource over time.

## Current Skill Map

The skill suite is grouped into:

- top-level selection skills
- Agno skills
- CrewAI skills
- LangChain skills
- Pydantic AI skills
- LangGraph skills
- Deep Agents skills
- LlamaIndex skills

For the full current skill inventory, see:

- [docs/selection/skill-map.md](./docs/selection/skill-map.md)
- [docs/selection/skill-map.zh-CN.md](./docs/selection/skill-map.zh-CN.md)

## Repository Structure

The repository is structured to separate reusable skills from future written documentation:

```text
.
├── .agents/
│   └── skills/
│       ├── framework-selection/
│       ├── agno-*/
│       ├── crewai-*/
│       ├── langchain-*/
│       ├── pydanticai-*/
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

### What goes where

- `.agents/skills/`: reusable Codex skills and their references
- `docs/frameworks/`: framework introductions and deeper framework-specific guides
- `docs/comparisons/`: side-by-side comparisons and tradeoff writeups
- `docs/selection/`: selection heuristics, decision trees, and scenario-based guidance
- `docs/superpowers/specs/`: design specs and planning artifacts

## Designed to Grow

This repository is intentionally leaving room for:

- more framework families
- more detailed framework introductions
- more comparison documents
- more selection heuristics for real-world scenarios
- more framework-specific skill suites

Likely future additions could include frameworks such as AutoGen, but the structure is meant to support any framework that deserves a serious introduction and comparison path.

## How to Extend It

When adding a new framework family, prefer this pattern:

1. update the top-level selection logic
2. add a focused skill or skill suite under `.agents/skills/`
3. add deeper docs under `docs/frameworks/`, `docs/comparisons/`, or `docs/selection/`
4. update the README summary and skill map

Keep the README high-signal. Put deep detail in skills and docs rather than turning this page into a giant encyclopedia.

## Current Direction

Right now, the repository is strongest as:

- a practical framework-selection skill library
- a structured place to compare framework strengths
- an expandable home for more framework introductions and tradeoff guides

The next natural step is to populate:

- `docs/frameworks/` with per-framework introductions
- `docs/comparisons/` with targeted side-by-side comparisons
- `docs/selection/` with scenario-based recommendations
