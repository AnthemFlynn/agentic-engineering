---
title: A committed .claude/settings.json baseline — permissions + the four hooks
type: reference
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, settings, permissions, hooks, enforcement]
source: claude-code-pro-playbook.md (Pattern 2, combined config)
---

## Takeaway

Commit a `.claude/settings.json` so the team shares one enforcement baseline: a `permissions` block (allow / ask / deny) plus the four baseline hooks wired up. `allow` runs without prompting, `ask` prompts, `deny` is a hard block.

## When it applies

Every team repo. Committing it (not leaving it in user settings) is what makes the guarantees portable across machines and teammates.

## Example

```json
{
  "permissions": {
    "allow": ["Bash(pnpm test:*)","Bash(pnpm lint:*)","Bash(pnpm build:*)",
              "Bash(git status)","Bash(git diff:*)","Bash(git add:*)",
              "Bash(git commit:*)","Bash(git log:*)","Read","Glob","Grep"],
    "ask":   ["Bash(git push:*)","Bash(pnpm db:migrate:*)"],
    "deny":  ["Read(./.env)","Read(./.env.*)","Read(./secrets/**)",
              "Bash(curl:*)","Bash(wget:*)"]
  },
  "hooks": { "PostToolUse": [ /* prettier */ ],
             "PreToolUse":  [ /* guard-bash.sh, protect-files.sh */ ],
             "Stop":        [ /* test gate */ ] }
}
```

Wire the four hooks from [[auto-format-on-write]], [[block-destructive-bash]], [[protect-sensitive-files]], and [[test-gate-on-stop]].

## Notes

- `deny` makes files invisible (e.g. `.env`) — the ENFORCEMENT layer of the [[enforcement-layer-cake]]. In headless runs the equivalent hard boundary is [[allowed-tools-hard-contract]].
- When a hook doesn't fire, see [[debugging-hooks]].
