# Pydantic AI Addition Design

## Goal

Add first-class Pydantic AI coverage to this repository in the same style as the existing framework families:

- a focused Pydantic AI skill subtree under `.agents/skills/`
- a framework introduction under `docs/frameworks/`
- updated top-level routing, selection docs, and README summaries

## Scope

Create these new skills:

- `pydanticai-dependencies`
- `pydanticai-fundamentals`
- `pydanticai-tools-mcp`
- `pydanticai-production`

Update these shared entry points:

- `framework-selection`
- `docs/selection/when-to-use-what.md`
- `docs/selection/skill-map.md`
- `docs/selection/skill-map.zh-CN.md`
- `README.md`
- `README.zh-CN.md`

Add this framework doc:

- `docs/frameworks/pydanticai.md`

## Positioning

Represent Pydantic AI as a Python-first agent framework with strong typed ergonomics, structured output, dependency injection, tool integration, model-provider flexibility, and production-oriented support for observability, evaluation, MCP, and durable execution.

Distinguish it from:

- LangChain: broader app primitives for models, tools, chains, and lightweight agents
- LangGraph: stronger when explicit graph orchestration, branching, loops, and state machines are the primary design problem
- Deep Agents: stronger for long-running coding-style systems centered on files, delegation, planning, and skill loading
- CrewAI: more flow-first and role/task-centric for business workflow automation
- LlamaIndex: stronger when retrieval, indexing, document parsing, and private-data access are the main challenge
- Agno: stronger when the user wants one integrated framework surface spanning agents, teams, workflows, knowledge, memory, sessions, and runtime operations

## Skill Boundaries

- `pydanticai-dependencies`: installation, supported Python versions, package selection, provider integrations, optional extras, and project setup expectations
- `pydanticai-fundamentals`: `Agent`, instructions/system prompts, typed output, message history, basic tools, result handling, and the default single-agent path
- `pydanticai-tools-mcp`: function tools, `RunContext`, dependency injection via `deps_type`, toolsets, MCP client/server usage, and when protocol-level tool interoperability is the hard part
- `pydanticai-production`: observability with Logfire, testing with Pydantic Evals, durable execution, multi-agent patterns, and production reliability guidance

## Routing Design

The Pydantic AI subtree should mirror the repository's current family pattern:

- top-level `framework-selection` decides whether Pydantic AI is the right starting point at all
- the four Pydantic AI sub-skills handle second-stage routing by dominant concern
- each sub-skill can point to another when a request spans multiple layers

Suggested routing rules:

- choose Pydantic AI when the user wants a Python agent framework with a Pydantic-native feel, typed results, explicit tool wiring, and production-oriented ergonomics without starting from a graph framework
- choose `pydanticai-dependencies` when package setup, installation, provider choices, or environment requirements are the main uncertainty
- choose `pydanticai-fundamentals` when the user is building a first agent or asking about core abstractions and default patterns
- choose `pydanticai-tools-mcp` when tools, dependency injection, MCP servers, or external capability integration are the dominant concern
- choose `pydanticai-production` when the main concern is tracing, evals, durable execution, reliability, or coordinating multiple agents

## Official Terminology Alignment

Use current Pydantic AI terminology from the official docs and keep wording consistent with those concepts:

- `Agent`
- `instructions`
- `deps_type`
- `RunContext`
- function tools via `@agent.tool` and `@agent.tool_plain`
- `toolsets`
- message history
- structured or typed output
- MCP
- durable execution / durable agents
- Logfire
- Pydantic Evals

Do not force LangChain-, LangGraph-, or CrewAI-specific mental models onto Pydantic AI material unless the document is explicitly doing cross-framework comparison.

## Content Style

- Keep SKILL files concise, routing-oriented, and Python-first
- Avoid copying official docs verbatim
- Prefer small modern examples centered on the current `Agent` API
- Emphasize what Pydantic AI is best at, not generic "best for agents" language
- Keep English as the primary language for new framework-specific material, while updating existing bilingual shared entry points in both English and Chinese

## Documentation Impact

The Pydantic AI addition should change the repository in two layers:

1. Framework-family coverage
   - add Pydantic AI to the README framework tables and repository structure examples
   - add Pydantic AI to the skill maps
   - add Pydantic AI to the top-level selection docs and routing skill

2. Pydantic-AI-specific guidance
   - introduce the framework in `docs/frameworks/pydanticai.md`
   - make the new skill subtree discoverable from the framework doc and shared docs

No Pydantic AI comparison doc is required in this phase. Cross-framework positioning should stay in the top-level docs and the framework introduction.

## Selection Positioning

At the top-level selection layer, Pydantic AI should be described as the best fit when:

- the user is working in Python
- typed and validated outputs are a first-class requirement
- the user wants simple agent construction with strong tool ergonomics
- dependency injection for tools and prompts is a feature, not an implementation detail
- production tracing, evals, or durable execution matter, but the user does not necessarily want a graph-first framework

It should not be presented as the best default when:

- graph orchestration and explicit state transitions are the real hard part
- retrieval and indexing dominate the architecture
- long-running work revolves around files, planning, and subagent delegation
- the app is mainly a role/task/crew workflow rather than a typed Python agent system

## Error Handling And Testing

This phase is documentation and skill-authoring work, not runnable product code. Validation should focus on:

- internal consistency between `framework-selection`, `when-to-use-what`, README summaries, and the new Pydantic AI docs
- realistic trigger descriptions for the four new skills
- clear boundaries so Pydantic AI does not blur into LangChain, LangGraph, Deep Agents, CrewAI, LlamaIndex, or Agno
- link integrity between README, docs, and skill files

## Out Of Scope

- adding runnable demo apps to the repository
- introducing a separate `pydanticai-selection` skill in this phase
- writing dedicated comparison docs such as `pydanticai-vs-langchain.md`
- translating all new framework-specific docs into Chinese unless the file is part of an existing bilingual shared entry-point set

## Assumptions

- Pydantic AI is being added as a full framework family rather than as a small extension to LangChain or LangGraph guidance
- the current Pydantic AI docs are stable enough to support the four-skill split above
- the repository's existing family pattern remains the target structure for new framework additions
