# Framework Selection Matrix

Use this file when a request could reasonably fit more than one framework.

## Primary Decision Rule

Pick the framework for the hardest part of the system right now:

- choose **LangChain** when the task is mostly model calls, prompt composition, tools, or a simple agent loop
- choose **Pydantic AI** when the task is mostly building a typed Python agent service with explicit tools, dependency injection, structured output, or production-friendly tracing/evals
- choose **CrewAI** when the task is mostly flow-first automation, role-based agent teamwork, and bounded crews inside a broader Python workflow
- choose **LangGraph** when the task is mostly orchestration, branching, loops, or state transitions
- choose **Deep Agents** when the task is mostly long-running execution, planning, files, memory, and delegation
- choose **LlamaIndex** when the task is mostly retrieval, indexing, document parsing, data access, or graph/data-centric querying
- choose **Agno** when the task is mostly building an integrated agent system that may need teams, workflows, persistence, and runtime operations in one stack

## Typical Routes

| Request shape | Start here | Then |
|---------------|------------|------|
| "Build a simple assistant with tools" | `LangChain` | add `LangGraph` only if control flow grows |
| "Build a typed Python agent with validated outputs and explicit tools" | `Pydantic AI` | add `LlamaIndex` only if retrieval becomes the hard backend |
| "Build a flow-first business automation with role-based agents" | `CrewAI` | use `crewai-flows`, then add crews for complex steps |
| "Build a retrying or branching agent" | `LangGraph` | add `LangChain` primitives inside nodes |
| "Build a long-running coding/research worker" | `Deep Agents` | add `LangGraph` for precise subflows if needed |
| "Build a chatbot over private docs" | `LlamaIndex` | use `llamaindex-rag`, then add agents only if needed |
| "Build an agent app that should scale into a managed runtime" | `Agno` | use `agno-fundamentals` -> `agno-agentos` as the system matures |
| "Build a research agent over a document corpus" | `LlamaIndex` | `llamaindex-rag` -> `llamaindex-agents` |
| "Build a durable agent with strong private-data retrieval" | `Deep Agents` | use LlamaIndex as the retrieval layer |
| "Build an automation that invokes agent teams and external tools" | `CrewAI` | add `crewai-tools-mcp` and `crewai-memory-knowledge` as needed |
| "Build one framework surface for agents, teams, and workflows" | `Agno` | add `agno-teams-workflows` and `agno-knowledge-memory` as needed |
| "Build a workflow over parsed PDFs and extracted entities" | `LlamaIndex` | `llamaindex-cloud-mcp` -> `llamaindex-structured-graph` -> `llamaindex-workflows` if orchestration grows |

## Combination Rules

### LangChain + LlamaIndex

Use this when LangChain is the app shell but LlamaIndex is the better retrieval layer.

Good fit:

- simple agents that need stronger RAG
- existing LangChain codebases adding document retrieval

### Pydantic AI + LlamaIndex

Use this when Pydantic AI is the typed Python application shell, but LlamaIndex is the better retrieval backend.

Good fit:

- typed service responses grounded in private docs
- agent apps where retrieval quality is more important than changing the agent surface
- Python backends that want Pydantic AI ergonomics plus a stronger data layer

### LangGraph + LlamaIndex

Use this when orchestration is custom, but retrieval/data access is still the hard backend problem.

Good fit:

- planner/executor flows over a private corpus
- corrective RAG with explicit graph-like control
- multi-step extraction and validation over document sets

### Deep Agents + LlamaIndex

Use this when the top-level system needs planning, files, and delegation, while retrieval should still be handled by specialized LlamaIndex components.

Good fit:

- long-running research assistants over enterprise knowledge bases
- coding agents that must query product docs or internal document stores

### CrewAI + LlamaIndex

Use this when CrewAI should remain the application and workflow shell, but private-data retrieval or document grounding needs a stronger specialized layer.

Good fit:

- support or ops flows grounded in internal documents
- research automations where a crew should query a separate retrieval system

### Agno + LlamaIndex

Use this when Agno should remain the integrated application and runtime shell, but retrieval and data access deserve a stronger specialized backend.

Good fit:

- managed agent systems grounded in large document sets
- AgentOS applications whose real data challenge is retrieval quality

## Escalation Rule

Start with one primary framework. Add a second only when a real boundary appears:

- retrieval is weak -> add `LlamaIndex`
- typed Python agent ergonomics matter most -> choose `Pydantic AI`
- workflow should be flow-first and role-based -> add `CrewAI`
- app should unify build and runtime concerns -> add `Agno`
- orchestration is messy -> add `LangGraph`
- task scope is open-ended and long-running -> add `Deep Agents`
- app logic is still simple -> stay in `LangChain`
