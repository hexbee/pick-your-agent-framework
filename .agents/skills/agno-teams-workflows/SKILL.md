---
name: agno-teams-workflows
description: "INVOKE THIS SKILL when an Agno project needs `Team`, `Workflow`, multi-agent coordination, or structured execution across specialists."
---

<overview>
Agno grows beyond one agent in two main ways:

- `Team` for coordinated specialists under a shared lead
- `Workflow` for explicit step-based execution across a larger process

Use teams when the hard part is collaboration. Use workflows when the hard part is staged execution.
</overview>

<selection-table>

| Need | Start Here |
|------|------------|
| A lead model coordinating specialists | `Team` |
| Explicit step-by-step execution | `Workflow` |
| Specialists with different tools or modalities | `Team` |
| Reusable process with ordered stages | `Workflow` |

</selection-table>

---

## Team Pattern

Use a `Team` when the system should delegate work to specialized members while preserving one application-facing surface.

<python>

```python
from agno.agent import Agent
from agno.models.openai import OpenAIChat
from agno.team import Team
from agno.tools.duckduckgo import DuckDuckGoTools

web_agent = Agent(
    name="Web Agent",
    model=OpenAIChat(id="gpt-4o"),
    tools=[DuckDuckGoTools()],
    instructions=["Find current information and include sources."],
)

writer_agent = Agent(
    name="Writer Agent",
    model=OpenAIChat(id="gpt-4o"),
    instructions=["Turn research into a concise brief."],
)

research_team = Team(
    name="Research Team",
    model=OpenAIChat(id="gpt-4o"),
    members=[web_agent, writer_agent],
    markdown=True,
    show_members_responses=True,
)
```

</python>

---

## Workflow Pattern

Use a `Workflow` when the task should be decomposed into explicit stages with stable boundaries between steps.

Keep workflows process-shaped. Keep teams intelligence-shaped.

---

## Design Guidance

1. Introduce a `Team` when specialization is clearer than one giant prompt.
2. Introduce a `Workflow` when execution order matters more than agent autonomy.
3. Keep member responsibilities distinct so delegation is obvious.
4. Add `db` support early if teams or workflows should preserve history or memory across runs.
5. Pair with `agno-agentos` when these systems need to be served and monitored in production.

---

## Routing

- Use `agno-fundamentals` if the user still needs the basic `Agent` model.
- Use `agno-knowledge-memory` when the hard part is grounding, sessions, or persistence.
- Use `agno-agentos` when the question shifts toward runtime serving or control-plane operations.

Read [references/patterns.md](references/patterns.md) for team-versus-workflow heuristics and escalation patterns.
