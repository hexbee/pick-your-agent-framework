---
name: llamaindex-workflows
description: "INVOKE THIS SKILL when implementing LlamaIndex event-driven workflows or custom orchestration. Covers `Workflow`, `Event`, `StartEvent`, `StopEvent`, `Context`, `@step`, branches, loops, concurrency, and `AgentWorkflow` fit."
---

<overview>
LlamaIndex workflows are event-driven and async-first.

Use them when you need explicit control flow such as:

- loops
- branching
- parallel fan-out and collection
- human approval points
- custom planner/executor patterns

They are a better fit than a simple agent loop when orchestration is the hard part.
</overview>

<workflow-vs-agent>

| Need | Prefer |
|------|--------|
| One agent with tools | `FunctionAgent` |
| Multiple agents with simple handoffs | `AgentWorkflow` |
| Arbitrary event-driven control flow | `Workflow` |
| Parallel steps, retries, or custom planner logic | `Workflow` |

</workflow-vs-agent>

---

## Core Primitives

| Primitive | Role |
|-----------|------|
| `Workflow` | Main orchestration class |
| `Event` | Typed payload passed between steps |
| `StartEvent` | Entry event for `.run()` inputs |
| `StopEvent` | Exit event carrying final result |
| `@step` | Declare a workflow step |
| `Context` | Shared store, event streaming, and coordination |

---

## Minimal Pattern

<ex-basic-workflow>
<python>

Define a two-step workflow with typed intermediate state.
```python
from llama_index.core.workflow import Workflow, Event, StartEvent, StopEvent, step

class JokeEvent(Event):
    joke: str

class JokeFlow(Workflow):
    @step
    async def generate(self, ev: StartEvent) -> JokeEvent:
        return JokeEvent(joke=f"Joke about {ev.topic}")

    @step
    async def finalize(self, ev: JokeEvent) -> StopEvent:
        return StopEvent(result=ev.joke)
```

</python>
</ex-basic-workflow>

The step type hints define valid event flow, so keep them accurate.

---

## Workflow Design Rules

1. Model each step around one responsibility.
2. Keep events small and typed.
3. Use `Context` for shared evolving state instead of overloading event payloads.
4. Write loops and branches explicitly; do not simulate them with prompt hacks.
5. Embrace async from the start.

---

## Concurrency and Collection

Use workflow events when one decision should trigger multiple downstream actions.

Typical pattern:

1. Evaluate the input
2. `ctx.send_event(...)` for each subtask
3. Collect results through follow-up events
4. Stop only when all required events are gathered

This is the right tool for query planning, document pipelines, and multi-source orchestration.

---

## Human-in-the-Loop and Reliability

Use workflows when you need clear pause/resume or validation boundaries.

- Put approval checks between risky steps.
- Keep state in `Context` so a run can resume coherently.
- Use explicit validation steps for structured generation, corrective RAG, or planner loops.

---

## Practical Guidance

- Keep business logic in plain Python; use the workflow runtime for coordination.
- Use workflow streaming to surface progress to users or logs.
- If the implementation starts to look like one giant agent prompt, split it into steps instead.

---

## Routing

- Use `llamaindex-agents` when the main need is tool-calling behavior, not orchestration.
- Use `llamaindex-cloud-mcp` when exposing workflows or tools through MCP is part of the design.
- Use `llamaindex-rag` when retrieval components are the main design surface.

Read [references/patterns.md](references/patterns.md) for branch, loop, fan-out, and planner workflow patterns.
