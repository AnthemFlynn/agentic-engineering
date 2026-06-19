---
title: A /plan slash command that produces an approved spec before any code
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, commands, planning]
source: claude-code-pro-playbook.md (Pattern 7)
---

## Takeaway

Encode a slash command that forces a written spec — clarifying questions, scope, explicit non-goals, affected files, verification criteria — and then *stops* and waits for "approved" before writing code. Treat the spec as a PR artifact.

## When it applies

Any non-trivial session, especially team settings where vague asks yield vague implementations. Skip for one-line mechanical changes.

## Why

A spec is cheap to change; code is not. Catching "Claude planned to put this in the monolith instead of the payments service" at the spec stage costs five minutes versus hours of wrong implementation.

## Example

```markdown
# .claude/commands/plan-feature.md
Before writing any code:
1. Ask clarifying questions if requirements are ambiguous (scope, edge cases, success criteria, what NOT to build).
2. Write a spec to docs/specs/$CURRENT_DATE-$FEATURE_NAME.md: problem · what we're building ·
   what we're NOT building · affected files (with why) · verification criteria · open questions.
3. Stop. Show the spec path. Wait for "approved" before writing code.
The spec is cheap to change. The code is not.
```

Invoke: `/plan-feature add-stripe-webhook-handler`.

## Notes

- Have it spec the increments as [[vertical-slice-prompt]]s. The written-spec discipline mirrors [[memory-md-session-handoff]]'s "decisions" capture.
