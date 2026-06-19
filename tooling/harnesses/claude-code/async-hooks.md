---
title: Run non-blocking hooks with async: true — but never for security gates
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code (async hooks, Jan 2026)
tags: [claude-code, hooks, performance]
source: claude-code-mastery-v3_2.html (E4)
---

## Takeaway

`async: true` on a hook handler runs it in the background without blocking Claude's execution — the hook fires, Claude continues, and the hook's result (success or failure) is ignored. Use it to keep latency-insensitive work off the critical path.

## When it applies

Audit logging, session/PreCompact backups, Slack notifications, metrics. **Never** for security gates: an async hook's block decision is ignored, so an async security hook provides zero protection. Those must run synchronously.

## Why

PreToolUse/PostToolUse hooks fire on every matched call; a slow synchronous hook degrades the whole session (keep sync hooks <200 ms). Marking fire-and-forget work async removes its latency entirely while keeping blocking gates synchronous.

## Example

```json
{ "hooks": { "PostToolUse": [{ "matcher": "Write|Edit", "hooks": [
  {"type":"command","async":true,  "command":"jq -c '{ts:now|todate,tool:.tool_name}' >> ~/.claude/audit.jsonl"},
  {"type":"command","async":false, "command":"npx prettier --write \"$CLAUDE_TOOL_INPUT_FILE_PATH\" 2>/dev/null || true"}
]}]}}
```

Audit writes async (zero latency); prettier runs sync (Claude waits for clean output).

## Notes

- The mechanism behind [[precompact-postcompact-backup]] and the audit trail in [[governance-audit-shadow-mcp]]. Sync gates: [[block-destructive-bash]], [[test-gate-on-stop]].
