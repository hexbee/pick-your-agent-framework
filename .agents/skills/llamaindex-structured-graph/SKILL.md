---
name: llamaindex-structured-graph
description: "INVOKE THIS SKILL when using structured output, schema-based extraction, typed LLM responses, or graph-oriented retrieval in LlamaIndex. Covers structured LLMs, structured prediction, extraction patterns, and `PropertyGraphIndex`."
---

<overview>
Use this skill for two related advanced cases:

1. The output must obey a schema
2. Retrieval depends on entities and relationships, not just chunk similarity

Start with the smallest abstraction that solves the problem. Do not jump to graph retrieval if typed JSON output or standard vector retrieval is enough.
</overview>

<selection-guide>

| Need | Use |
|------|-----|
| Typed response from an LLM call | structured LLM output |
| Schema-based extraction from text or docs | structured extraction / prediction |
| Agent output consumed by code | `output_cls` or equivalent typed schema |
| Entity/relationship reasoning over a corpus | `PropertyGraphIndex` |

</selection-guide>

---

## Structured Outputs

Use structured outputs when downstream code should parse the result deterministically.

<ex-structured-llm>
<python>

Ask an LLM to return a typed object instead of raw prose.
```python
from pydantic import BaseModel

class CompanySummary(BaseModel):
    name: str
    sector: str
    risks: list[str]

sllm = llm.as_structured_llm(CompanySummary)
response = await sllm.achat("Summarize the company and list key risks.")
summary = response.raw
```

</python>
</ex-structured-llm>

Prefer schemas with stable field names, modest nesting, and unambiguous semantics.

---

## Structured Extraction

Use extraction when you need to pull records from documents according to a known schema.

Good fits:

- contracts
- invoices
- forms
- tables converted to structured records
- entity extraction from long text

Keep the schema tight. Overly broad schemas make extraction less reliable and harder to validate.

---

## Property Graph Guidance

Use `PropertyGraphIndex` when the question depends on relationships such as:

- who reports to whom
- which systems depend on which services
- how entities connect across documents

Prefer vector RAG first if the task is mostly semantic lookup. Switch to graph retrieval when relationship traversal or entity linkage is the core requirement.

---

## Design Rules

- Validate structured outputs before persisting them.
- Separate extraction schema design from retrieval schema design.
- Keep graph entities and relations normalized.
- Combine graph retrieval with vector retrieval when answers need both relationship context and raw evidence.

---

## Routing

- Use `llamaindex-rag` for standard chunk retrieval and response synthesis.
- Use `llamaindex-agents` when typed outputs are part of an agent loop.
- Use `llamaindex-cloud-mcp` when document parsing quality is the bottleneck before extraction.

Read [references/structured-vs-graph.md](references/structured-vs-graph.md) when deciding between typed extraction, vector retrieval, and graph retrieval.
