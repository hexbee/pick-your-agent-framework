---
name: crewai-fundamentals
description: "INVOKE THIS SKILL when building any basic CrewAI Python project. Covers installation, CLI scaffolding, `Agent`, `Task`, `Crew`, `Process`, and the core `kickoff()` workflow."
---

<overview>
CrewAI's core runtime model is:

`define agents -> assign tasks -> assemble a crew -> choose a process -> kickoff`

Prefer CrewAI when you want role-based agents working through explicit tasks inside a Python application. For production apps, CrewAI's own docs recommend a flow-first architecture, but the `Agent` / `Task` / `Crew` model is still the foundation.
</overview>

<installation>

| Need | Command |
|------|---------|
| Install core package | `pip install crewai` |
| Install with tool integrations | `pip install 'crewai[tools]'` |
| Scaffold a crew project | `crewai create crew <project_name>` |
| Scaffold a flow project | `crewai create flow <project_name>` |
| Install project dependencies | `crewai install` |
| Run the project | `crewai run` |

</installation>

---

## Core Objects

| Object | Purpose |
|--------|---------|
| `Agent` | A role-based worker with goals, backstory, tools, and optional knowledge |
| `Task` | A concrete unit of work with a description and expected output |
| `Crew` | A team of agents and tasks executed together |
| `Process` | Execution style such as sequential or hierarchical |

---

## Minimal Crew

<python>

```python
from crewai import Agent, Task, Crew, Process

researcher = Agent(
    role="Research Analyst",
    goal="Find the most relevant facts for the topic",
    backstory="You turn scattered information into a clean research brief.",
    verbose=True,
)

writer = Agent(
    role="Writer",
    goal="Turn research into a clear final answer",
    backstory="You write concise, useful explanations for busy readers.",
    verbose=True,
)

research_task = Task(
    description="Research the main tradeoffs of CrewAI for internal tooling.",
    expected_output="A concise research summary with the most important tradeoffs.",
    agent=researcher,
)

write_task = Task(
    description="Write a final recommendation based on the research summary.",
    expected_output="A short recommendation in markdown.",
    agent=writer,
)

crew = Crew(
    agents=[researcher, writer],
    tasks=[research_task, write_task],
    process=Process.sequential,
    verbose=True,
)

result = crew.kickoff()
print(result.raw)
```

</python>

---

## Planning and Processes

- Use `Process.sequential` as the default when tasks should run in a clear order.
- Use hierarchical or hybrid process patterns only when task delegation structure is the real requirement.
- Enable planning when the crew should reason about task execution before acting.

<python>

```python
crew = Crew(
    agents=[researcher, writer],
    tasks=[research_task, write_task],
    process=Process.sequential,
    planning=True,
    planning_llm="gpt-4o",
)
```

</python>

---

## Design Guidance

1. Start with a small number of sharply-defined agents.
2. Write tasks so the expected output is concrete and testable.
3. Treat a crew as a unit of work, not the whole application shell.
4. Move to `crewai-flows` once the app needs durable state, branching, external triggers, or multiple crew invocations.
