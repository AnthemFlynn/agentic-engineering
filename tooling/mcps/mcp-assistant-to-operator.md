---
title: MCP is what turns a coding assistant into an operator
type: pattern
confidence: anecdotal
date: 2026-06-18
model:
version:
tags: [mcp, integrations, operator]
source: claude-code-field-guide-may2026.md (section 10)
---

## Takeaway

Without MCP, an agent edits files and runs shell. With MCP servers, it can pull the Linear/Jira issue, query the DB, check Sentry for the trace, read Confluence for context, and open the PR — all in one loop. That shift, from "edit code" to "operate the system," is the point of MCP.

## When it applies

When the agent needs to understand *why* something is being built and *whether* what shipped works. Highest-value integrations: issue tracker (Linear, Jira), docs (Notion, Confluence), observability (Sentry, Datadog).

## Why

Those external systems hold the context and feedback loops that file access alone can't reach. Connecting them closes the loop from intent → implementation → verification inside a single agent run.

## Example

Strategy that holds up in practice:

- Start with official Anthropic and well-maintained community servers before building custom.
- Scope each server to only the tools a given project needs.
- Cache where appropriate — a chatty MCP that pulls live data on every turn slows the agent meaningfully.

## Notes

- MCP is cross-harness (Claude Code, Codex, Cursor), which is why this lives in `tooling/mcps/` rather than under a harness. Harness-specific MCP *wiring* quirks go under that harness.
- The "expanded tool access" tier of the operator stack — see [[delegation-vs-supervision-spectrum]] and [[enforcement-layer-cake]].
