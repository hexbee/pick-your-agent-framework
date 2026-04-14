# LlamaIndex Install Matrix

## Starter Bundles

| Goal | Packages |
|------|----------|
| Quick prototype | `llama-index` |
| Explicit production stack | `llama-index-core` + exact provider integrations |
| Local model stack | `llama-index-core`, file reader package, local LLM package, local embedding package |

## Common Integrations

| Concern | Typical package family |
|---------|------------------------|
| LLM provider | `llama-index-llms-*` |
| Embeddings | `llama-index-embeddings-*` |
| Readers | `llama-index-readers-*` |
| Vector stores | integration-specific vector-store package |
| Managed parsing/cloud | LlamaCloud/LlamaParse client packages if needed |

## Rules

- Keep integration packages explicit in app dependencies.
- Avoid mixing very old examples with current installs; imports drift over time.
- Prefer `llama-index-core` imports in code examples unless the umbrella package is deliberately chosen for convenience.
- Re-check docs if an example still centers `ServiceContext`; modern code should usually use `Settings`.
