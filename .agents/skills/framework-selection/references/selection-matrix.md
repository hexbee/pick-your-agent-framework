# Framework Selection Matrix

Use this file when a request could reasonably fit more than one framework.

## Primary Decision Rule

Pick the framework for the hardest part of the system right now:

- choose **LangChain** when the task is mostly model calls, prompt composition, tools, or a simple agent loop
- choose **LangGraph** when the task is mostly orchestration, branching, loops, or state transitions
- choose **Deep Agents** when the task is mostly long-running execution, planning, files, memory, and delegation
- choose **LlamaIndex** when the task is mostly retrieval, indexing, document parsing, data access, or graph/data-centric querying

## Typical Routes

| Request shape | Start here | Then |
|---------------|------------|------|
| "Build a simple assistant with tools" | `LangChain` | add `LangGraph` only if control flow grows |
| "Build a retrying or branching agent" | `LangGraph` | add `LangChain` primitives inside nodes |
| "Build a long-running coding/research worker" | `Deep Agents` | add `LangGraph` for precise subflows if needed |
| "Build a chatbot over private docs" | `LlamaIndex` | use `llamaindex-rag`, then add agents only if needed |
| "Build a research agent over a document corpus" | `LlamaIndex` | `llamaindex-rag` -> `llamaindex-agents` |
| "Build a durable agent with strong private-data retrieval" | `Deep Agents` | use LlamaIndex as the retrieval layer |
| "Build a workflow over parsed PDFs and extracted entities" | `LlamaIndex` | `llamaindex-cloud-mcp` -> `llamaindex-structured-graph` -> `llamaindex-workflows` if orchestration grows |

## Combination Rules

### LangChain + LlamaIndex

Use this when LangChain is the app shell but LlamaIndex is the better retrieval layer.

Good fit:

- simple agents that need stronger RAG
- existing LangChain codebases adding document retrieval

### LangGraph + LlamaIndex

Use this when orchestration is custom, but retrieval/data access is still the hard backend problem.

Good fit:

- planner/executor flows over a private corpus
- corrective RAG with explicit graph-like control
- multi-step extraction and validation over document sets

### Deep Agents + LlamaIndex

Use this when the top-level system needs planning, files, and delegation, while retrieval should still be handled by specialized LlamaIndex components.

Good fit:

- long-running research assistants over enterprise knowledge bases
- coding agents that must query product docs or internal document stores

## Escalation Rule

Start with one primary framework. Add a second only when a real boundary appears:

- retrieval is weak -> add `LlamaIndex`
- orchestration is messy -> add `LangGraph`
- task scope is open-ended and long-running -> add `Deep Agents`
- app logic is still simple -> stay in `LangChain`
