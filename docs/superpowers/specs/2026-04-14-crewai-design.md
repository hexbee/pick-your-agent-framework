# CrewAI Addition Design

## Goal

Add first-class CrewAI coverage to this repository in the same style as the existing framework families:

- a focused CrewAI skill subtree under `.agents/skills/`
- a framework introduction under `docs/frameworks/`
- updated top-level routing, selection docs, and README summaries

## Scope

Create these new skills:

- `crewai-selection`
- `crewai-fundamentals`
- `crewai-flows`
- `crewai-tools-mcp`
- `crewai-memory-knowledge`

Update these shared entry points:

- `framework-selection`
- `docs/selection/when-to-use-what.md`
- `docs/selection/skill-map.md`
- `docs/selection/skill-map.zh-CN.md`
- `README.md`
- `README.zh-CN.md`

Add this framework doc:

- `docs/frameworks/crewai.md`

## Positioning

Represent CrewAI as a flow-first, Python-centric framework for production automation with role-based agents, task/process orchestration, and crews embedded inside flows.

Distinguish it from:

- LangChain: lighter app primitives and simpler agent loops
- LangGraph: lower-level custom orchestration
- Deep Agents: long-running open-ended work with files, delegation, and skills
- LlamaIndex: retrieval, indexing, and data-centric systems

## Skill Boundaries

- `crewai-selection`: route ambiguous CrewAI questions to the right sub-skill
- `crewai-fundamentals`: installation, `Agent` / `Task` / `Crew` / `Process`, quickstart
- `crewai-flows`: `Flow`, `@start`, `@listen`, `@router`, state, flow-first architecture
- `crewai-tools-mcp`: tools, `crewai[tools]`, MCP servers, transports, filtering, safety
- `crewai-memory-knowledge`: memory vs knowledge, when to preload knowledge, when to recall memories

## Content Style

- Keep SKILL files concise and routing-oriented
- Prefer current CrewAI terminology from official docs
- Avoid copying official docs verbatim
- Keep examples small, modern, and Python-first
