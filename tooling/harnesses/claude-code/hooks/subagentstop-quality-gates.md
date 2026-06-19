---
title: Gate subagent output with a SubagentStop hook
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, hooks, subagents, quality]
source: claude-code-mastery-v3_2.html (E3)
---

## Takeaway

`SubagentStop` fires when a subagent finishes, *before* it returns to the main agent. Returning `decision: "block"` keeps the subagent running and delivers the reason as its next instruction — an automated retry loop the main agent never has to orchestrate.

## When it applies

When a subagent must meet a contract before its result is trusted (e.g. a code-reviewer that must cite `file:line` and use severity levels). The hook receives `agent_id`, `agent_type`, `agent_transcript_path`, and `last_assistant_message` (the final output text — no transcript parsing needed).

## Why

Quality enforcement on subagent output otherwise falls to the main agent's judgment. A SubagentStop gate makes it mechanical and self-correcting: block with a specific reason, the subagent fixes it and re-submits.

## Example

```bash
INPUT=$(cat)
[ "$(echo "$INPUT" | jq -r '.agent_type')" != "code-reviewer" ] && exit 0
MSG=$(echo "$INPUT" | jq -r '.last_assistant_message')
echo "$MSG" | grep -qE '[a-zA-Z]+\.[a-zA-Z]+:[0-9]+' || \
  { echo '{"decision":"block","reason":"Review lacks file:line references."}'; exit 2; }
echo "$MSG" | grep -qE 'CRITICAL|IMPORTANT|SUGGESTION' || \
  { echo '{"decision":"block","reason":"Review must use severity levels."}'; exit 2; }
exit 0
```

## Notes

- Enforces the contract of [[subagent-code-reviewer]] automatically. Can also be an `agent`-type hook (review-the-reviewer) — see [[hook-handler-types]].
