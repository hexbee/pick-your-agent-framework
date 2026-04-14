---
name: llamaindex-cloud-mcp
description: "INVOKE THIS SKILL when working with LlamaParse, LlamaCloud, or MCP in the LlamaIndex ecosystem. Covers managed parsing, extraction, indexing/retrieval pipelines, MCP clients and tools, and when to choose cloud-managed services over OSS-only building blocks."
---

<overview>
Use this skill when the OSS framework alone is not the whole story.

It covers three adjacent capabilities:

- LlamaParse for high-fidelity document parsing
- LlamaCloud for managed ingestion, indexing, retrieval, and sync
- MCP for consuming or exposing tools in a standard protocol

Choose managed services when operational complexity or document quality is the real bottleneck, not because the local framework feels unfamiliar.
</overview>

<selection-guide>

| Need | Use |
|------|-----|
| Hard PDFs, tables, charts, messy layouts | LlamaParse |
| Managed connectors, sync, indexing, retrieval | LlamaCloud |
| Tool interoperability via protocol | MCP |
| Full local control with simple inputs | OSS readers and stores |

</selection-guide>

---

## LlamaParse Guidance

Reach for LlamaParse when documents are visually complex or structurally messy.

Typical cases:

- nested tables
- scans and OCR-heavy PDFs
- presentations
- charts and embedded images

If plain text files or simple markdown are enough, stay in OSS readers first.

---

## LlamaCloud Guidance

Use LlamaCloud when you need managed document operations such as:

- source connectors
- recurring sync
- production-grade indexing
- managed retrieval surfaces
- cloud extraction workflows

This is usually the right choice when the hardest problem is data operations, not custom retrieval logic.

---

## MCP Guidance

Use MCP when a LlamaIndex agent or workflow should consume external tools through a protocol instead of custom adapters.

<ex-mcp-tools>
<python>

Load MCP tools into a LlamaIndex agent.
```python
from llama_index.core.agent import FunctionAgent
from llama_index.tools.mcp import BasicMCPClient, McpToolSpec

client = BasicMCPClient("https://developers.llamaindex.ai/mcp")
tool_spec = McpToolSpec(client=client)
tools = await tool_spec.to_tool_list_async()

agent = FunctionAgent(
    llm=llm,
    tools=tools,
    system_prompt="Use MCP tools when the answer depends on remote documentation or services.",
)
```

</python>
</ex-mcp-tools>

Also consider MCP when you want to expose existing workflows or tools for other clients to consume.

---

## Cloud vs OSS Decision Rule

Stay OSS-first when:

- data sources are simple
- you need low-level retrieval control
- local execution is a hard requirement

Move to LlamaParse or LlamaCloud when:

- document parsing quality dominates answer quality
- managed sync/connectors matter
- you are rebuilding ingestion plumbing that the cloud product already solves

---

## Routing

- Use `llamaindex-rag` after parsed or managed data reaches the retrieval layer.
- Use `llamaindex-structured-graph` for schema-based extraction after parsing quality is solved.
- Use `llamaindex-workflows` if MCP tools or cloud operations need custom event-driven orchestration.

Read [references/managed-services.md](references/managed-services.md) for OSS-vs-cloud decision rules and MCP usage boundaries.
