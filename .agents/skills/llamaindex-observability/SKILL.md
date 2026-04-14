---
name: llamaindex-observability
description: "INVOKE THIS SKILL when instrumenting, evaluating, tracing, debugging, or cost-checking a LlamaIndex app. Covers source inspection, tracing, instrumentation, evaluation datasets, retrieval/response evaluation, and observability integrations."
---

<overview>
Use observability early.

For most LlamaIndex failures, the real bug is one of these:

- bad retrieval
- bad chunking
- wrong tool choice
- overstuffed prompts
- schema mismatch

Tracing and evaluation make those visible.
</overview>

<debug-surface>

| Question | Inspect |
|----------|---------|
| Did retrieval fetch the right chunks? | `source_nodes`, retriever output, filters |
| Did synthesis distort the answer? | response mode, prompts, source grounding |
| Did an agent pick the wrong tool? | streaming events, tool calls, tool results |
| Is cost too high? | token counting, trace spans, response fan-out |

</debug-surface>

---

## First-Line Debugging

Start with local inspection before adding a full observability platform:

1. Print or inspect retrieved nodes and metadata.
2. Check `response.source_nodes`.
3. Stream agent or workflow events.
4. Compare retrieved evidence with the final answer.
5. Reduce complexity before tuning prompts.

---

## Instrumentation Guidance

The docs expose both older callback-based integrations and newer instrumentation-oriented approaches.

Use this rule:

- Prefer current instrumentation APIs and provider guides for new systems.
- Accept `set_global_handler(...)` only when a partner integration still documents that path.

When integrating a tracing platform, confirm whether it expects callbacks, instrumentation, or both.

---

## Evaluation Strategy

Split evaluation into at least two layers:

| Layer | Measure |
|-------|---------|
| Retrieval | relevance, recall-like behavior, filtering quality |
| Response | faithfulness, correctness, completeness, style constraints |

Evaluate retrieval separately before blaming the LLM answer.

---

## Cost and Performance

- Count tokens around retrieval expansion and synthesis.
- Watch for redundant multi-step retrieval.
- Use smaller models where orchestration or classification is simple.
- Avoid expensive agents when a query engine can answer directly.

---

## Routing

- Use `llamaindex-rag` to improve retrieval architecture once you know what failed.
- Use `llamaindex-agents` to improve tool descriptions or agent structure after a trace reveals bad decisions.
- Use `llamaindex-workflows` when traces show orchestration, branching, or concurrency issues.

Read [references/eval-debug.md](references/eval-debug.md) for a concrete debug order and evaluation split.
