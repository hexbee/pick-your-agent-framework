# LlamaIndex Architecture

## Canonical Call Chain

1. Read source data into `Document`s
2. Parse/split/enrich into `Node`s
3. Build an index or attach storage
4. Retrieve nodes for a query
5. Synthesize a response
6. Expose that interface as a query engine, chat engine, or tool

## Boundary Rules

- `Document` is source-oriented.
- `Node` is retrieval-oriented.
- Indexes organize nodes.
- Retrievers fetch candidates.
- Response synthesizers turn candidates into answers.
- Query/chat engines provide the application-facing interface.

## Anti-Patterns

- Do not put all app logic in one `as_query_engine()` call without knowing the retrieval path.
- Do not use an agent when a query engine alone can solve the task.
- Do not keep ingestion, retrieval, and UI glue mixed in one file if the project is growing.
