# Structured Output vs Graph Retrieval

## Use Structured Output When

- the result must be JSON-like or schema-bound
- you need extraction from documents into records
- downstream code expects typed fields

## Use Graph Retrieval When

- questions depend on relationships between entities
- traversal matters more than plain chunk similarity
- the corpus contains durable entities and edges worth modeling

## Use Plain Vector RAG When

- the task is mostly semantic lookup
- relationships are incidental rather than the core retrieval primitive

## Mixed Pattern

It is valid to:

1. parse/extract structured entities
2. build or enrich a graph
3. combine graph lookup with vector evidence for final answers
