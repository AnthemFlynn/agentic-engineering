---
title: Keep a thin CLAUDE.md and @import detailed docs conditionally
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code (@import supported)
tags: [claude-code, context, claude-md]
source: claude-code-staff-engineer-patterns.md (Pattern 10)
---

## Takeaway

As a project grows, a flat CLAUDE.md bloats every session. Instead, keep a thin root (~60–80 lines of invariants + one-liner architecture) and `@import` detailed docs under task-scoped headings. The imports load based on task relevance, so a 200-line migration doc never costs an API-routes session.

## When it applies

Projects large enough that one CLAUDE.md would mix many domains (auth, payments, migrations, workers). Small projects don't need the indirection.

## Why

Every token in the root file is paid on every session. Pushing domain detail behind conditional `@import` headings keeps the always-loaded surface small while still making deep context available exactly when the task touches that area.

## Example

```markdown
# Root .claude/CLAUDE.md (thin)
## Hard rules
NEVER use npm/yarn — pnpm only. NEVER push to main. NEVER log PII (see @docs/logging-policy.md).
## When working on database migrations
@docs/migration-protocol.md
## When working on payments or billing
@docs/payments-runbook.md
```

Each imported file can run 200 lines of detail without bloating unrelated sessions.

## Notes

- The BEHAVIORAL layer of [[enforcement-layer-cake]] — still advisory (~70–80%); back must-hold rules with enforcement controls like [[allowed-tools-hard-contract]].
- Session *state* (not static knowledge) belongs in [[memory-md-session-handoff]], not here.
