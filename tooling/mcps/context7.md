---
title: Context7 — an MCP server for live, version-accurate library docs
type: reference
confidence: anecdotal
date: 2026-06-18
model:
version:
tags: [mcp, context7, documentation]
source: claude-code-mastery-v3_2.html (S3)
---

## Takeaway

Context7 is an MCP server that fixes stale training data: it intercepts library-related questions, fetches current documentation from the source, and injects it into context before the model answers. Accurate API usage even for libraries that post-date the model's training cutoff.

## When it applies

Fast-moving ecosystems where docs change between training cycles (React, Next.js, Tailwind, Prisma, Drizzle, tRPC, .NET packages — 10,000+ libraries). Less needed for stable, slow-changing APIs.

## Example

```json
// .mcp.json
{ "mcpServers": { "context7": { "command": "npx", "args": ["-y", "@context7/mcp@latest"] } } }
```

Then in a session: *"How do I set up Drizzle with Turso? use context7"* → Claude fetches current docs before answering.

## Notes

- A standalone MCP server (cross-harness), so it lives here rather than under a harness. For designing your *own* MCP servers, see [[mcp-server-intent-grouped-design]]; commit servers to a team `.mcp.json` registry per [[governance-audit-shadow-mcp]].
