# LlamaIndex Eval and Debug Order

## Debug Order

1. inspect source data quality
2. inspect chunks and metadata
3. inspect retrieved nodes
4. inspect synthesized response
5. inspect agent/workflow events
6. then add tracing/evaluation platforms

## Evaluation Split

| Layer | Questions |
|-------|-----------|
| Retrieval | Did we fetch the right evidence? |
| Response | Did the answer stay faithful to evidence? |
| Agent | Did the right tool or path get chosen? |
| Workflow | Did the orchestration follow the intended route? |

## Cost Checks

- watch token growth from large retrieval fan-in
- watch repeated retrieval inside loops
- watch agent plans that could be direct query-engine calls instead
