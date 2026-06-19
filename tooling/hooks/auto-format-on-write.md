---
title: Auto-format every file Claude writes with a PostToolUse hook
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, hooks, formatting]
source: claude-code-pro-playbook.md (Pattern 2, Hook 1)
---

## Takeaway

Run the formatter automatically after every file Claude touches, so output is team-standard before Claude even responds — no "please run prettier" round-trips.

## When it applies

Any repo with a formatter. Match `Write|Edit|MultiEdit`. Keep it non-fatal (`|| true`) so a format failure never blocks the edit.

## Why

Formatting is deterministic and cheap; making it a hook removes it from the model's responsibility entirely. Claude writes a 200-line file with inconsistent style; the hook normalizes it silently.

## Example

```json
{
  "hooks": {
    "PostToolUse": [{
      "matcher": "Write|Edit|MultiEdit",
      "hooks": [{
        "type": "command",
        "command": "npx prettier --write \"$CLAUDE_TOOL_INPUT_FILE_PATH\" 2>/dev/null || true"
      }]
    }]
  }
}
```

Prefer the repo's own formatter entrypoint (`pnpm prettier`, `pnpm eslint --fix`) over a remote `npx` package where possible.

## Notes

- Part of the [[committed-settings-json-baseline]]. PostToolUse, so it runs *after* the write — pair with PreToolUse guards ([[protect-sensitive-files]]) to stop bad writes before disk.
