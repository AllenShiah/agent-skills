---
name: coding-agent
description: Entry point for software-coding tasks in a repository. Routes to sub-skills in references/. Currently covers codebase exploration with the codebase-memory MCP knowledge graph. Use when the user wants to explore or understand a codebase, see its architecture or structure, find where a function is defined, find who calls a function or what it calls, trace a call chain, check dependencies, assess the impact of a change, find dead code or unused functions, find high fan-in or fan-out code, pick refactor candidates, or run a code-quality audit.
---

# Coding Agent

Router for coding tasks. Pick the row that matches the task, read that file in full, then follow it.

## Sub-skills

| Task | Read this file |
|------|----------------|
| Understand structure, find callers or callees, trace calls, dependencies, impact analysis, dead code, architecture | [references/codebase-memory/SKILL.md](references/codebase-memory/SKILL.md) |

If no row matches, do the task normally. Do not force a sub-skill.

## Tool availability

`codebase-memory` is an MCP server named `codebase-memory-mcp`. It is a set of tools, not a command or a skill. It may be installed on some agents and not on others.

1. Look at your tool list for tools such as `search_graph`, `trace_path`, `get_code_snippet`, `index_repository`.
2. Your agent may add a prefix to the tool name. Claude Code shows `mcp__codebase-memory-mcp__search_graph`. The reference file uses the short names. Use whatever name your agent shows.
3. If the tools are there: use them first for structure questions. Use grep or file reads for exact text, config and non-code files.
4. If the tools are not there: tell the user the MCP server is not available in this agent. Fall back to grep, file reads and editor symbol search. Do not invent graph results. Do not try to install the server unless the user asks.
