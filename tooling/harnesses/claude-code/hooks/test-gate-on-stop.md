---
title: Don't let Claude stop until tests pass (Stop hook with loop guard)
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, hooks, testing]
source: claude-code-pro-playbook.md (Pattern 2, Hook 4)
---

## Takeaway

A Stop hook that runs the test suite when Claude declares done and `exit 2`s on failure, so Claude keeps working until green. A `stop_hook_active` check prevents an infinite stop loop.

## When it applies

Repos with a fast, reliable test command. If the suite is slow or flaky, scope it (affected files only) or it will make every turn painful.

## Why

Claude tends to declare done before verifying. The Stop hook makes "done" mean "tests pass" mechanically, not by self-assessment. Implements [[rubric-as-self-verification]] as an external gate.

## Example

```json
{
  "hooks": {
    "Stop": [{
      "hooks": [{
        "type": "command",
        "command": "INPUT=$(cat); [ \"$(echo $INPUT | jq -r '.stop_hook_active')\" = 'true' ] && exit 0; pnpm test --silent 2>&1 | tail -5 || exit 2"
      }]
    }]
  }
}
```

Claude declares done → hook runs tests → 2 fail → `exit 2` → Claude sees the failures and continues.

## Notes

- The `stop_hook_active` guard is mandatory — without it, a failing test loops forever. See [[debugging-hooks]].
- Part of [[committed-settings-json-baseline]].
