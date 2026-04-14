# Agno Addition Design

## Goal

Add first-class Agno coverage to this repository in the same style as the existing framework families:

- a focused Agno skill subtree under `.agents/skills/`
- a framework introduction under `docs/frameworks/`
- updated top-level routing, selection docs, and README summaries

## Scope

Create these new skills:

- `agno-selection`
- `agno-fundamentals`
- `agno-teams-workflows`
- `agno-knowledge-memory`
- `agno-agentos`

Update these shared entry points:

- `framework-selection`
- `docs/selection/when-to-use-what.md`
- `docs/selection/skill-map.md`
- `docs/selection/skill-map.zh-CN.md`
- `README.md`
- `README.zh-CN.md`

Add this framework doc:

- `docs/frameworks/agno.md`

## Positioning

Represent Agno as an integrated Python framework for building agents, teams, and workflows with built-in support for tools, memory, knowledge, sessions, and a production runtime layer through AgentOS.

Distinguish it from:

- LangChain: lighter and more composable primitives for model and tool workflows
- CrewAI: more flow-first and task/crew-oriented for structured business automations
- LangGraph: lower-level, more explicit control over branching, loops, and state transitions
- Deep Agents: stronger for coding-style long-running work centered on files, delegation, and skill loading
- LlamaIndex: stronger when retrieval, indexing, parsing, and private-data access are the primary design concern

## Skill Boundaries

- `agno-selection`: route ambiguous Agno questions to the right sub-skill
- `agno-fundamentals`: installation, project shape, `Agent`, models, tools, instructions, sessions, and basic single-agent patterns
- `agno-teams-workflows`: `Team`, `Workflow`, multi-agent coordination, and when to move from one agent to a coordinated system
- `agno-knowledge-memory`: knowledge bases, vector DB choices, retrieval grounding, memory, persistence, and how Agno separates stable knowledge from learned user context
- `agno-agentos`: AgentOS runtime, control plane, API surface, serving, monitoring, and production-oriented architecture

## Routing Design

The Agno subtree should mirror the repository's existing family pattern:

- a top-level framework-selection layer decides whether Agno is the right starting point at all
- `agno-selection` handles Agno-specific second-stage routing
- each Agno sub-skill covers one dominant concern and can chain to another when requests span multiple layers

Suggested routing rules:

- choose Agno when the user wants one framework that spans agents, teams, workflows, memory/knowledge, and runtime operations
- choose `agno-fundamentals` when the question is still about basic agent construction
- choose `agno-teams-workflows` when the main question is multi-agent coordination or structured orchestration inside Agno
- choose `agno-knowledge-memory` when grounding, recall, sessions, or persistence are the hard part
- choose `agno-agentos` when the main concern is deployment, serving, management, or observability through AgentOS

## Content Style

- Keep SKILL files concise, routing-oriented, and consistent with the existing Agno-free framework skills
- Prefer current Agno terminology from the official docs, especially `Agent`, `Team`, `Workflow`, `Knowledge`, `Memory`, `Sessions`, and `AgentOS`
- Avoid copying official docs verbatim
- Keep examples small, modern, and Python-first
- Treat English as the primary content language, while syncing Chinese where the repository already maintains bilingual entry points

## Documentation Impact

The Agno addition should change the repository in two layers:

1. Framework-family coverage
   - add Agno to the README framework tables and repository structure examples
   - add Agno to the skill maps
   - add Agno to the top-level selection docs and routing skill

2. Agno-specific guidance
   - introduce Agno in `docs/frameworks/agno.md`
   - make the new skill subtree discoverable from the framework doc and shared docs

No Agno comparison doc is required in this phase. Cross-framework positioning should live in the top-level docs and in the Agno framework introduction.

## Error Handling And Testing

This phase is documentation and skill-authoring work, not runnable product code. Validation should focus on:

- internal consistency between `framework-selection`, `when-to-use-what`, README summaries, and the new Agno docs
- skill descriptions that trigger on realistic Agno user requests
- clear boundaries so Agno does not blur into CrewAI, LangGraph, or LlamaIndex in the routing guidance
- link integrity between README, docs, and skill files

## Out Of Scope

- adding Agno code examples outside skills and docs
- building runnable Agno demo apps in the repository
- adding Agno comparison docs such as `agno-vs-crewai.md` in this iteration
- translating all Agno-specific documents into Chinese unless a file is already part of the repository's bilingual entry-point set

## Assumptions

- Agno is being added as a full framework family rather than a single tactical skill
- official Agno terminology and structure are stable enough to support a five-skill subtree
- the current repository pattern for framework families remains the target pattern for expansion
