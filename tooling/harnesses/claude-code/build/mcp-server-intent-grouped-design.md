---
title: Design MCP tools around intent, not as a 1:1 API mirror
type: pattern
confidence: proven
date: 2026-06-18
model:
version:
tags: [claude-code, mcp, tool-design, runtime]
source: claude-code-mastery-v3_2.html (Level 4, P2)
---

## Takeaway

At the runtime level, tool design is the primary leverage point — above model choice or prompt quality. Group tools by *task/intent*, not by API endpoint. One rich `get_project_status` (that fans out to project + metrics + blockers internally) beats four primitives the model must orchestrate. Past ~15 tools, selection accuracy degrades measurably.

## When it applies

Building a custom MCP server. For APIs with hundreds of endpoints (AWS, Kubernetes, Cloudflare), use the **dispatcher pattern**: one tool accepts a script, runs it sandboxed against the API, returns the result — Cloudflare covers ~2,500 endpoints with two tools.

## Why

The model picks tools from their descriptions. Vague docstrings ("Get data") wreck selection; rich ones ("Fetch the last 30 days of Stripe charges for a customer ID, returning amount, status, created_at") make it pick right every time. Fewer, intent-shaped tools keep selection accurate and context small.

## Example

```ts
server.tool("get_project_status",
  `Get current status, health metrics, and active blockers for a project.
   Use when answering questions about project health or before status reports.`,
  { projectId: z.string().describe("Project ID e.g. 'proj-1234'") },
  async ({ projectId }) => { /* Promise.all([fetchProject, fetchMetrics, fetchBlockers]) */ });
```

Tool search helps too: configure many tools but withhold their definitions from context until needed (e.g. 50 configured, 3–5 loaded per turn).

## Notes

- The build-your-own counterpart to installing servers like [[context7]]; the operator payoff is [[mcp-assistant-to-operator]]. Rich-but-flat tool *output* should be a [[structured-output-contract]]. Centralize servers via [[governance-audit-shadow-mcp]]. Below [[the-line]].
