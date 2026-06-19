---
title: Governance — audit trail, a committed .mcp.json, security on hard boundaries
type: pattern
confidence: proven
date: 2026-06-18
model:
version:
tags: [claude-code, governance, security, mcp, runtime]
source: claude-code-mastery-v3_2.html (Level 4, P5)
---

## Takeaway

At the runtime level, security must rest on technical limits, not prompt instructions (CLAUDE.md is advisory; `--allowedTools` is the only hard boundary). Three non-negotiables: **least privilege per task**, **human checkpoints at irreversible boundaries** (prod deploys, external sends, DB mutations), and **observability before autonomy** (full audit trail before expanding permissions).

## When it applies

Any autonomous agent with access to real systems. Log every tool call (async, so it adds no latency); expand permissions only once you can see what the agent does.

## Why

**The Shadow MCP Problem:** MCP adoption spreads from a few developers to dozens managing hundreds of locally-configured connections with scattered credentials and no central visibility. The fix is a single team-committed `.mcp.json` as the source of truth, reviewed like code.

## Example

```json
// audit logging (async — zero latency)
{"hooks":{"PostToolUse":[{"hooks":[{"type":"command","async":true,
  "command":"jq -c '{ts:now|todate,session:env.CLAUDE_SESSION_ID,tool:.tool_name,status:\"ok\"}' >> ~/.claude/audit.jsonl"}]}]}}
// .mcp.json — team-committed registry, the single source of truth
{"mcpServers":{"internal":{"command":"npx","args":["tsx","mcp-servers/internal/index.ts"],
  "env":{"API_KEY":"${INTERNAL_API_KEY}"}}}}
```

## Notes

- The hard boundary is [[allowed-tools-hard-contract]]; the committed-config discipline extends [[committed-settings-json-baseline]]; the supervise-vs-delegate calibration is [[delegation-vs-supervision-spectrum]]. Audit logging uses [[async-hooks]]. Below [[the-line]].
