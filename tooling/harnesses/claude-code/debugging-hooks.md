---
title: Debugging hooks when they don't fire
type: reference
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, hooks, debugging]
source: claude-code-pro-playbook.md (Debugging hooks section)
---

## Takeaway

When a hook silently doesn't run, work the short checklist of usual causes before rewriting anything: matcher mismatch, non-executable script, broken `jq`, or a missing Stop-loop guard.

## When it applies

Any time a configured hook appears to have no effect. Start by confirming it's even registered with `/hooks`.

## Why

Hooks fail quietly — a regex that doesn't match the (case-sensitive) tool name, or a `jq` expression that errors, produces no visible signal. Reproducing the exact stdin the hook receives is the fastest way to localize the fault.

## Example

```bash
/hooks            # inside Claude Code: lists configured hooks + matchers + events
Ctrl+O            # verbose mode — see hook output inline
claude --debug    # full debug mode

# Feed a hook script the exact JSON it would receive:
echo '{"tool_name":"Bash","tool_input":{"command":"rm -rf dist"},"session_id":"t","cwd":"/tmp"}' \
  | ./.claude/hooks/guard-bash.sh; echo "Exit: $?"
```

Common causes: matcher regex doesn't match the case-sensitive tool name (`Write`, `Edit`, `Bash`); script not executable (`chmod +x .claude/hooks/*.sh`); `jq` parse failure; Stop-hook infinite loop missing the `stop_hook_active` guard.

## Notes

- Hook event names and JSON schemas can shift on minor releases — re-verify with `/hooks` after upgrades.
- Referenced by every hook note: [[block-destructive-bash]], [[protect-sensitive-files]], [[test-gate-on-stop]], [[auto-format-on-write]], [[session-start-context-injection]].
