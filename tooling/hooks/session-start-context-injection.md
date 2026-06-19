---
title: Inject branch and sprint context at session start with a SessionStart hook
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, hooks, context]
source: claude-code-pro-playbook.md (Pattern 9)
---

## Takeaway

A SessionStart hook returns `additionalContext` so every session begins already knowing the branch, last commit, and active sprint state — no re-explaining each time.

## When it applies

Team repos with shared sprint state. Pull dynamic facts (branch, last commit) inline; keep slower-changing context in a committed file the hook references.

## Why

Without it, each session re-discovers the same situational facts. Injecting them once at start removes that overhead and prevents Claude from acting on stale assumptions about what's in flight.

## Example

```json
{
  "hooks": {
    "SessionStart": [{
      "hooks": [{
        "type": "command",
        "command": "echo '{\"additionalContext\": \"Branch: '$(git branch --show-current)'. Last commit: '$(git log -1 --format=\"%s\")'. See .claude/sprint-context.md if present.\"}'"
      }]
    }]
  }
}
```

Maintain `.claude/sprint-context.md` (regenerated weekly at standup): focus, DO-NOT-touch areas, blockers, key decisions, active tickets + branches.

## Notes

- This carries *current* situational context; durable cross-session state belongs in [[memory-md-session-handoff]], static rules in [[claude-md-living-document]].
