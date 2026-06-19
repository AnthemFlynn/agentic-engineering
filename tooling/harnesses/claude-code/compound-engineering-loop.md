---
title: Compound engineering — every session should make the next one smarter
type: pattern
confidence: proven
date: 2026-06-18
model:
version:
tags: [claude-code, mindset, claude-md]
source: claude-code-mastery-v3_2.html (E7)
---

## Takeaway

Treat your config as a compound-interest vehicle: every wrong assumption is an opportunity to prevent it permanently, and every *repeated* correction signals you used the wrong primitive. The escalation ladder decides where a fix belongs.

## When it applies

Continuously. The discipline is recognizing which rung a recurring problem is on, and moving the fix to the right primitive instead of re-correcting in-session.

## Why

A fix encoded at the wrong altitude doesn't stick — advisory text for something that must always hold, a conversation for something that recurs. Routing each fix to the right primitive is what makes the setup compound instead of staying flat.

## Example

```
Wrong assumption        → encode the rule in CLAUDE.md, commit with the fix
Corrected the same      → it's not a CLAUDE.md problem, it's a HOOK problem
  thing twice              (make it deterministic, not advisory)
Workflow recurs > twice → it's not a conversation, it's a SKILL problem
  (package once, invoke forever)
Session went wrong      → root cause to MEMORY.md; the WHY to CLAUDE.md
At 6 months: CLAUDE.md + hooks + skills encode your team's hard-won decisions.
  Teams running this loop compound. Teams that don't stay flat.
```

## Notes

- The rungs map to existing notes: [[claude-md-living-document]] / [[diagnostic-prompt-to-claude-md]] (rule), [[committed-settings-json-baseline]] (hook), [[create-pr-skill]] + [[skills-subagents-agent-teams-spectrum]] (skill), [[memory-md-session-handoff]] (decision log).
