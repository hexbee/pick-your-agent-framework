# CrewAI Tools and MCP Patterns

## Choose Direct Tools When

- the integration is local, explicit, and already packaged
- you want simple dependency management
- the agent only needs a small fixed capability set

## Choose MCP When

- the tool source is remote or standardized
- you want one integration pattern across multiple systems
- the same external server may be reused by different agents

## Reliability Notes

- MCP servers may be unreachable or slow; design flows to handle partial capability
- cache tool lists when the server supports stable discovery
- filter exposed tools when the raw server surface is too broad
