---
name: crewai-tools-mcp
description: "INVOKE THIS SKILL when connecting CrewAI agents to tools, `crewai_tools`, or MCP servers. Covers agent tools, `crewai[tools]`, MCP transports, filtering, and practical safety guidance."
---

<overview>
CrewAI agents can gain capabilities in two main ways:

- direct tools via `tools=[...]`
- MCP-connected tools via `mcps=[...]`

Use regular tools when the capability is local and explicit. Use MCP when you want a standardized tool interface to external or remote systems.
</overview>

<capability-selection>

| Need | Use |
|------|-----|
| A direct Python tool or packaged integration | `tools=[...]` |
| Search, file, browser, or other packaged CrewAI tools | `crewai[tools]` and `crewai_tools` |
| Remote or standardized external tool servers | `mcps=[...]` |
| Fine-grained MCP transport and filtering control | structured MCP server config objects |

</capability-selection>

---

## Direct Tools

<python>

```python
from crewai import Agent
from crewai_tools import SerperDevTool, FileReadTool

research_agent = Agent(
    role="Research Analyst",
    goal="Find and summarize useful information",
    backstory="You know how to turn search results into clean summaries.",
    tools=[SerperDevTool(), FileReadTool()],
    verbose=True,
)
```

</python>

---

## MCP Quick Start

<python>

```python
from crewai import Agent

agent = Agent(
    role="Research Assistant",
    goal="Use external tools through MCP servers",
    backstory="You know how to combine multiple tool sources safely.",
    mcps=[
        "https://mcp.exa.ai/mcp?api_key=your_key&profile=research",
        "github#search_repositories",
    ],
)
```

</python>

---

## Structured MCP Configuration

<python>

```python
from crewai import Agent
from crewai.mcp import MCPServerHTTP, MCPServerStdio
from crewai.mcp.filters import create_static_tool_filter

agent = Agent(
    role="Advanced Research Analyst",
    goal="Use curated MCP tool access",
    backstory="You work with external tools, but only the allowed ones.",
    mcps=[
        MCPServerStdio(
            command="npx",
            args=["-y", "@modelcontextprotocol/server-filesystem"],
            tool_filter=create_static_tool_filter(
                allowed_tool_names=["read_file", "list_directory"]
            ),
            cache_tools_list=True,
        ),
        MCPServerHTTP(
            url="https://api.example.com/mcp",
            headers={"Authorization": "Bearer token"},
            streamable=True,
            cache_tools_list=True,
        ),
    ],
)
```

</python>

---

## Safety Guidance

1. Prefer the narrowest tool set that still solves the task.
2. Filter MCP tools when the server exposes more capability than the agent should have.
3. Treat remote MCP endpoints as infrastructure dependencies that can fail or time out.
4. Use CrewAI flows around tool-heavy crews when you need retries, auditability, or post-processing.

Read [references/mcp-patterns.md](references/mcp-patterns.md) for selection guidance across direct tools and MCP.
