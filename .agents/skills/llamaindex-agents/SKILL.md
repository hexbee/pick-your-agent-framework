---
name: llamaindex-agents
description: "INVOKE THIS SKILL when building LlamaIndex agents, agent tools, or multi-agent systems. Covers `FunctionAgent`, function tools, query engines as tools, state, streaming events, handoffs, and current multi-agent patterns."
---

<overview>
In LlamaIndex, an agent is usually an LLM plus tools plus a reasoning loop.

Start simple:

- Use `FunctionAgent` for most modern tool-calling agents.
- Expose retrieval through `QueryEngineTool` when an agent should consult data selectively.
- Use `AgentWorkflow` when multiple agents need built-in handoffs.
- Drop to custom workflows only when the built-in agent patterns are not expressive enough.
</overview>

<agent-patterns>

| Pattern | Use When |
|---------|----------|
| Single `FunctionAgent` | One agent with tools is enough |
| `AgentWorkflow` | Multiple specialists need handoffs |
| Orchestrator agent | One top-level agent should call other agents as tools |
| Custom planner | You need total control over planning and execution |

</agent-patterns>

---

## Tool Design

Prefer these tool shapes:

1. Plain Python functions for deterministic actions
2. `QueryEngineTool` for RAG access
3. Agent-as-tool wrappers for specialist sub-agents

Give every tool a clear name and a description that explains when it is useful. LlamaIndex agents rely heavily on tool descriptions.

<ex-function-agent>
<python>
Build a tool-calling agent with one regular tool and one retrieval tool.
```python
from llama_index.core.agent.workflow import FunctionAgent
from llama_index.core.tools import FunctionTool, QueryEngineTool

search_tool = QueryEngineTool.from_defaults(
    query_engine=index.as_query_engine(),
    name="search_docs",
    description="Useful for answering questions about the indexed documents.",
)

def record_note(note: str) -> str:
    return f"Recorded: {note}"

agent = FunctionAgent(
    llm=llm,
    tools=[
        search_tool,
        FunctionTool.from_defaults(fn=record_note),
    ],
    system_prompt="Use tools whenever the answer depends on indexed data.",
)
```
</python>
</ex-function-agent>

---

## State and Memory

- Use `initial_state` for structured per-run state.
- Use workflow `Context` and `ctx.store` when state must evolve across steps.
- Keep state compact and serializable.
- Store durable facts or intermediate artifacts, not full prompt strings unless you truly need them.

---

## Streaming and Inspection

Use streaming during development and UI integration so you can observe:

- agent deltas
- selected tool calls
- tool results
- current active agent

This is especially useful for debugging wrong tool choice or bad handoff behavior.

---

## Multi-Agent Guidance

- Start with `AgentWorkflow` if you just need specialist handoffs.
- Use an orchestrator agent when you want one central decision-maker.
- Use a custom planner only when you need explicit XML/JSON plans, custom scheduling, or richer state transitions.

If the task is more about orchestration than about agents themselves, switch to `llamaindex-workflows`.

---

## Agent Quality Checklist

- Make tool descriptions concrete.
- Keep system prompts role-specific and narrow.
- Prefer retrieval tools over stuffing all corpus text into the prompt.
- Inspect streaming events before concluding the model is "bad".
- Add structured output only when consumers need machine-readable results.

---

## Routing

- Use `llamaindex-workflows` for `Workflow`, event loops, concurrency, or checkpoint-like orchestration.
- Use `llamaindex-rag` when retrieval design is the real problem.
- Use `llamaindex-structured-graph` when the final output must be typed or schema-bound.

Read [references/patterns.md](references/patterns.md) for single-agent, orchestrator, and multi-agent pattern examples.
