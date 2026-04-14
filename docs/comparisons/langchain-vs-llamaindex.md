# LangChain vs LlamaIndex

## Why This Comparison Matters

LangChain and LlamaIndex overlap enough that many teams treat them as interchangeable, but they are not optimized for the same center of gravity.

The practical question is usually not "which one is better?" It is:

- is this primarily an application-framework problem
- or is this primarily a retrieval and data-access problem

## Short Answer

Use LangChain first when:

- the app is mostly model calls, tools, and simple agents
- retrieval is present but not the dominant challenge
- you want a general-purpose app layer

Use LlamaIndex first when:

- retrieval quality is central
- the system depends on private data
- indexing, parsing, or graph/data retrieval matter
- the app is really a document or knowledge system

## Main Overlap

Both can help with:

- RAG
- tools
- agents
- model integrations

This is why they are often compared directly.

## Main Difference

LangChain is broader as a general application toolkit.

LlamaIndex is deeper in retrieval, indexing, and data-centric workflows.

That is the most useful practical distinction.

## Choose LangChain When

- you are building a general agent or assistant shell
- you want a simple tool loop first
- retrieval is only one subsystem among many
- you expect orchestration to move toward LangGraph later

## Choose LlamaIndex When

- you are building over private docs, data sources, or knowledge stores
- retrieval relevance and source quality are the main product risks
- document parsing and extraction quality matter
- graph-aware retrieval or structured extraction may become important

## Combine Them When

Combining them is a valid pattern.

Typical combination:

- use LangChain for model/tool app structure
- use LlamaIndex for retrieval, indexing, query engines, or parsing

This is often better than forcing one framework to cover both concerns equally.

## Common Misread

One common mistake is choosing LangChain for a system that is really a retrieval-quality problem.

Another common mistake is choosing LlamaIndex for a system that barely has a data layer and really just needs a simple agent loop.

## Where To Go Next

- Read [LangChain](../frameworks/langchain.md)
- Read [LlamaIndex](../frameworks/llamaindex.md)
- Read [When to Use What](../selection/when-to-use-what.md)
