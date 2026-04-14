# Managed Services and MCP

## Use OSS Only When

- files are simple
- local control matters most
- custom retrieval logic is the main work

## Use LlamaParse When

- parsing quality is the bottleneck
- PDFs or slides have complex layouts
- OCR/table/chart extraction matters

## Use LlamaCloud When

- managed connectors and sync matter
- you need hosted indexing and retrieval operations
- data plumbing is becoming the real project

## Use MCP When

- you want protocol-level tool interoperability
- LlamaIndex agents should consume remote tools through a standard interface
- you want to expose tools or workflows for external clients
