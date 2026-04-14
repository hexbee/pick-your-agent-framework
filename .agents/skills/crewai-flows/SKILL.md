---
name: crewai-flows
description: "INVOKE THIS SKILL when building a CrewAI application around `Flow`. Covers flow-first architecture, `@start`, `@listen`, `@router`, state management, and embedding crews inside production workflows."
---

<overview>
CrewAI's current production guidance is flow-first:

- use a `Flow` as the application shell
- store durable state in a typed state model
- trigger crews only for the steps that benefit from autonomous collaboration

Think of it as:

`Flow manages state and control -> Crew handles complex role-based work -> Flow decides what happens next`
</overview>

<flow-primitives>

| Primitive | Purpose |
|-----------|---------|
| `Flow[StateModel]` | Application shell with typed state |
| `@start()` | Entry point for the workflow |
| `@listen(...)` | Run a step after another step or route |
| `@router(...)` | Branch execution based on previous output |

</flow-primitives>

---

## Minimal Flow

<python>

```python
from pydantic import BaseModel
from crewai.flow.flow import Flow, listen, start


class ReportState(BaseModel):
    topic: str = ""
    research: str = ""
    report: str = ""


class ReportFlow(Flow[ReportState]):
    @start()
    def gather_topic(self):
        self.state.topic = "CrewAI for internal developer workflows"
        return self.state.topic

    @listen(gather_topic)
    def draft_report(self, topic):
        self.state.report = f"Report topic: {topic}"
        return self.state.report


flow = ReportFlow()
flow.kickoff()
print(flow.state.report)
```

</python>

---

## Crew Inside a Flow

<python>

```python
from crewai import Agent, Crew, Task
from crewai.flow.flow import Flow, listen, start
from pydantic import BaseModel


class ArticleState(BaseModel):
    topic: str = ""
    research: str = ""
    final_article: str = ""


class ArticleFlow(Flow[ArticleState]):
    @start()
    def set_topic(self):
        self.state.topic = "CrewAI framework adoption"
        return self.state.topic

    @listen(set_topic)
    def run_research_crew(self, topic):
        researcher = Agent(
            role="Research Analyst",
            goal=f"Research {topic}",
            backstory="You produce grounded briefs for product teams.",
        )
        task = Task(
            description=f"Research {topic} and produce a concise brief.",
            expected_output="A grounded research summary.",
            agent=researcher,
        )
        result = Crew(agents=[researcher], tasks=[task]).kickoff()
        self.state.research = result.raw
        return result.raw

    @listen(run_research_crew)
    def write_article(self, research):
        self.state.final_article = f"Final article based on:\n{research}"
        return self.state.final_article
```

</python>

---

## Routing and State

- Use `@router(...)` when the flow should branch on classification, validation, or external signals.
- Keep raw business state in the Pydantic model rather than re-deriving it from messages.
- Prefer flows over standalone crews once the app needs retries, loops, resumption, or multiple phases.

Read [references/patterns.md](references/patterns.md) for common flow design patterns and anti-patterns.
