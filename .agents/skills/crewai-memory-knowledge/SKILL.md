---
name: crewai-memory-knowledge
description: "INVOKE THIS SKILL when a CrewAI project needs memory, knowledge sources, or grounded context. Covers the difference between memory and knowledge, recall patterns, and when to preload information at the crew or agent level."
---

<overview>
CrewAI separates two related concerns:

- **Memory**: preserve and recall relevant information across execution
- **Knowledge**: preload external information sources so agents can ground answers in domain data

Use memory for evolving context. Use knowledge for reference material the system should already know how to access.
</overview>

<distinction-table>

| Need | Use |
|------|-----|
| Recall prior findings or observations | Memory |
| Ground agents in docs, URLs, or structured domain content | Knowledge |
| Share the same grounding across a whole crew | Crew-level `knowledge_sources` |
| Give one specialist extra context | Agent-level `knowledge_sources` |

</distinction-table>

---

## Memory in a Flow

<python>
```python
from crewai.flow.flow import Flow, listen, start


class ResearchFlow(Flow):
    @start()
    def gather_data(self):
        findings = "PostgreSQL handles 10k concurrent connections."
        self.remember(findings, scope="/research/databases")
        return findings

    @listen(gather_data)
    def write_report(self, findings):
        past = self.recall("database performance benchmarks")
        context = "\n".join(f"- {m.record.content}" for m in past)
        return f"New findings: {findings}\nPrevious context:\n{context}"
```
</python>

---

## Knowledge Sources

<python>
```python
from crewai import Agent, Crew, Process, Task
from crewai.knowledge.source.string_knowledge_source import StringKnowledgeSource

user_profile = StringKnowledgeSource(
    content="The user is John, age 30, living in San Francisco."
)

agent = Agent(
    role="About User",
    goal="Answer questions about the user accurately.",
    backstory="You are good at grounded personal context lookup.",
)

task = Task(
    description="Answer the following question: {question}",
    expected_output="A short grounded answer.",
    agent=agent,
)

crew = Crew(
    agents=[agent],
    tasks=[task],
    process=Process.sequential,
    knowledge_sources=[user_profile],
)

result = crew.kickoff(
    inputs={"question": "Which city does John live in?"}
)
```
</python>

---

## Design Guidance

1. Use knowledge when the agent should start grounded in stable reference material.
2. Use memory when relevant context emerges during execution and should be recalled later.
3. Put shared sources on the `Crew` and specialist-only sources on the `Agent`.
4. If the app needs durable control flow around memory-heavy behavior, pair this with `crewai-flows`.

Read [references/patterns.md](references/patterns.md) for practical memory-versus-knowledge heuristics.
