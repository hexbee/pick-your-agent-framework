---
name: llamaindex-rag
description: "INVOKE THIS SKILL when building ANY LlamaIndex retrieval-augmented generation system. Covers readers, ingestion, node parsing, metadata extraction, index selection, retrievers, query engines, routers, node postprocessors, response synthesis, and persistence."
---

<overview>
Use the LlamaIndex RAG stack in this order:

1. Load data into `Document`s
2. Transform documents into `Node`s
3. Build an index or connect a store
4. Retrieve candidate nodes
5. Postprocess, rerank, filter, or route
6. Synthesize the final answer

LlamaIndex is strongest when you customize each stage deliberately instead of treating RAG as one opaque helper.
</overview>

<index-selection>

| Need | Start Here |
|------|------------|
| General semantic retrieval | `VectorStoreIndex` |
| Summarization over a corpus | `SummaryIndex` |
| Hierarchical composition | `TreeIndex` |
| Exact keyword-heavy lookups | keyword-style indexes |
| Relationship-heavy retrieval | See `llamaindex-structured-graph` |

</index-selection>

---

## Loading and Ingestion

Use readers for source-specific loading and `IngestionPipeline` for repeatable preprocessing.

<ex-ingestion-pipeline>
<python>

Split, enrich, and embed documents through an explicit ingestion pipeline.
```python
from llama_index.core import VectorStoreIndex
from llama_index.core.ingestion import IngestionPipeline
from llama_index.core.node_parser import SentenceSplitter
from llama_index.core.extractors import TitleExtractor

documents = SimpleDirectoryReader("data").load_data()

pipeline = IngestionPipeline(
    transformations=[
        SentenceSplitter(chunk_size=1024, chunk_overlap=100),
        TitleExtractor(),
    ]
)

nodes = pipeline.run(documents=documents)
index = VectorStoreIndex(nodes)
```

</python>
</ex-ingestion-pipeline>

Use metadata extraction when filters, routing, or citation quality matter. Keep metadata small, stable, and query-relevant.

---

## Retrieval Stack

<retrieval-stack>

| Layer | Responsibility |
|-------|----------------|
| Retriever | Fetch candidate nodes |
| Node postprocessor | Filter, rerank, dedupe, or rewrite candidates |
| Response synthesizer | Turn candidates into the final answer |
| Query engine | Package the whole retrieval path into one interface |

</retrieval-stack>

<ex-custom-query-engine>
<python>

Build a custom query engine from explicit components.
```python
from llama_index.core.retrievers import VectorIndexRetriever
from llama_index.core.response_synthesizers import get_response_synthesizer
from llama_index.core.query_engine import RetrieverQueryEngine

retriever = VectorIndexRetriever(index=index, similarity_top_k=5)
synthesizer = get_response_synthesizer(response_mode="refine")

query_engine = RetrieverQueryEngine(
    retriever=retriever,
    response_synthesizer=synthesizer,
)
```

</python>
</ex-custom-query-engine>

---

## Response Modes and Routing

- Use compact/default synthesis for standard QA.
- Use refine or tree-style synthesis for larger context or summarization-heavy answers.
- Use routers when different indexes, tools, or retrievers should answer different question types.
- Use sub-question or multi-step strategies only when a single retriever is not enough.

---

## Persistence and Stores

Choose persistence based on scale:

| Need | Approach |
|------|----------|
| Quick local prototyping | Persist local storage context |
| Production vector retrieval | Attach a vector store backend |
| Mixed storage needs | Configure `StorageContext` explicitly |

Prefer explicit vector stores when data volume, tenancy, or sync requirements exceed local disk persistence.

---

## Quality Checklist

- Verify chunk size against the target model context window.
- Keep metadata filters simple and deterministic.
- Inspect `response.source_nodes` during development.
- Tune `similarity_top_k` before adding more complicated logic.
- Add reranking or routing only after baseline retrieval is healthy.

---

## Routing

- Use `llamaindex-fundamentals` for baseline framework structure.
- Use `llamaindex-structured-graph` for `PropertyGraphIndex`, structured extraction, or typed retrieval outputs.
- Use `llamaindex-observability` for retrieval evaluation, tracing, and cost analysis.

Read [references/patterns.md](references/patterns.md) for index selection, retriever composition, and router patterns.
