---
title: Five hook handler types — command, prompt, agent, HTTP, mcp_tool
type: reference
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x (mcp_tool added v2.1.118)
tags: [claude-code, hooks]
source: claude-code-mastery-v3_2.html (E1, E2, E5)
---

## Takeaway

A hook isn't only a shell script. There are five handler types, each trading speed for capability:

| Type | What it does | Use when |
|------|--------------|----------|
| `command` | runs a shell script | deterministic checks — fastest, ~80% of cases |
| `prompt` | one LLM yes/no (30s default) | the input data alone is enough to decide |
| `agent` | spawns a subagent with Read/Grep/Glob (60s) | the decision needs codebase exploration |
| `http` | POSTs the event JSON to a URL | enterprise gateway / external validation |
| `mcp_tool` | invokes a configured MCP tool | validation logic already lives in an MCP server |

## When it applies

Choose the cheapest type that can make the decision. Reserve `agent` (slow, spawns a model) for verifications that genuinely require exploring code; reserve `http`/`mcp_tool` for centralized, version-controlled enforcement infrastructure.

## Example

```json
// agent hook — explores before deciding
{"type":"agent","prompt":"Run the test suite, check for TS errors. Return ok:true only if all pass.","timeout":120}
// http hook — non-2xx = non-blocking error; to block, return 2xx with {decision:"block"}
{"type":"http","url":"https://security-gateway.internal/claude/pre-tool","timeout":5000,
 "headers":{"Authorization":"Bearer $GATEWAY_TOKEN"},"allowedEnvVars":["GATEWAY_TOKEN"]}
// mcp_tool hook — same stdin JSON in, {decision,reason,additionalContext} out
{"type":"mcp_tool","server":"internal","tool":"validate_file_edit"}
```

## Notes

- All five return the same `{decision, reason, additionalContext}` contract. `mcp_tool` pairs with [[mcp-server-intent-grouped-design]] for centralized validation; `agent`/`http` push enforcement into infra (see [[governance-audit-shadow-mcp]]).
- Cross-agent gating uses these on [[subagentstop-quality-gates]]. Debugging: [[debugging-hooks]]. Baseline wiring: [[committed-settings-json-baseline]].
