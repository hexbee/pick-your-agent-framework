# LlamaIndex RAG Patterns

## Index Selection

| Situation | Suggested start |
|-----------|-----------------|
| General semantic QA | `VectorStoreIndex` |
| Corpus summarization | `SummaryIndex` |
| Relationship-heavy questions | `PropertyGraphIndex` |

## Retriever Composition

Start with:

1. one index
2. one retriever
3. one response synthesizer

Then add:

- metadata filters
- rerankers or node postprocessors
- routers
- multi-step decomposition

only when the baseline misses specific cases.

## Router Use

Use routers when different backends are clearly specialized, such as:

- summary index vs vector index
- SQL/query tool vs document retrieval
- general corpus vs domain-specific corpus

## Healthy Build Order

1. Validate chunking
2. Validate retrieval
3. Validate synthesis
4. Then add routing or multi-step logic
