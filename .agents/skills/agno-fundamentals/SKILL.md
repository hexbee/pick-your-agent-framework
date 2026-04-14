---
name: agno-fundamentals
description: "INVOKE THIS SKILL when building any basic Agno Python project. Covers installation, `Agent`, model/tool setup, instructions, session-aware context, and the first single-agent patterns."
---

<overview>
Think about Agno fundamentals as the baseline runtime loop:

`configure model -> define Agent -> add tools/instructions -> choose context and persistence -> run`

Start here when the user still needs to understand how Agno structures a single capable agent before adding teams, workflows, or AgentOS.
</overview>

<core-abstractions>

| Abstraction | Purpose |
|-------------|---------|
| `Agent` | Core unit for instructions, model use, tools, and context handling |
| Model | LLM backend such as OpenAI, Claude, or Gemini adapters |
| Tool | External capability the agent can call while solving a task |
| `instructions` | Behavioral and domain guidance for the agent |
| `db` | Shared persistence layer for sessions, history, and memory-related features |
| Session/history flags | Decide how much prior conversation is brought back into context |

</core-abstractions>

---

## Setup Rule

Follow the current Agno install docs and start in a Python virtual environment.

Typical baseline:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -U agno
```

Then add provider-specific packages only when your chosen model or tool stack requires them.

---

## Core Design Rules

1. Start with one `Agent` before introducing teams or workflows.
2. Keep tools narrow and purposeful instead of giving one agent every capability.
3. Add history or session context deliberately because it changes prompt shape and runtime behavior.
4. Introduce a database early if the app needs persistence, summaries, or memory updates.
5. Move to `agno-teams-workflows` only when one agent is no longer a clean fit.

---

## Minimal Skeleton

<python>

```python
from agno.agent import Agent
from agno.models.openai import OpenAIChat
from agno.tools.duckduckgo import DuckDuckGoTools

agent = Agent(
    name="Research Agent",
    model=OpenAIChat(id="gpt-4o"),
    tools=[DuckDuckGoTools()],
    instructions=["Always cite your sources."],
    markdown=True,
)

agent.print_response("Find two recent articles about vector databases.", stream=True)
```

</python>

Use a `db` when you need session summaries, memory updates, or persistent history across runs.

---

## Upgrade Signals

Move beyond fundamentals when:

- one agent is acting like a dispatcher for multiple specialties
- you need explicit team coordination or workflow steps
- knowledge bases or memory become first-class design elements
- the app should be served and managed as an AgentOS runtime

---

## Routing

- Use `agno-teams-workflows` when the main problem is multi-agent structure or workflow orchestration.
- Use `agno-knowledge-memory` when knowledge, memory, or sessions become the dominant concern.
- Use `agno-agentos` when the app should be exposed and operated through AgentOS.

Read [references/architecture.md](references/architecture.md) for the baseline Agno call chain and upgrade boundaries.
