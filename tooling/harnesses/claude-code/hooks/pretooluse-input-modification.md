---
title: PreToolUse hooks can silently rewrite Claude's tool input
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.0.10+
tags: [claude-code, hooks, security]
source: claude-code-staff-engineer-patterns.md (Pattern 2)
---

## Takeaway

A PreToolUse hook receives the tool call as JSON on stdin and returns (possibly modified) JSON on stdout. Claude sees the modified version as if it drafted it — transparent enforcement it can't reason around. (Distinct from `exit 2`, which *blocks* the call.)

## When it applies

When you want to *redirect* rather than reject: make a risky action safe instead of failing it. If you'd rather hard-stop, use `exit 2` (block) or [[allowed-tools-hard-contract]] (whitelist) instead.

## Why

The model can talk its way around advisory rules in CLAUDE.md but cannot perceive a stdin→stdout rewrite. It executes the safe variant, sees success, and never learns a redirect happened — so the guarantee holds regardless of prompt.

## Example

Redirect any `git push origin main` to the current branch (`.claude/hooks/safe-push.sh`):

```bash
INPUT=$(cat); COMMAND=$(echo "$INPUT" | jq -r '.tool_input.command // empty')
if echo "$COMMAND" | grep -qE 'git push.*(origin main|origin master)'; then
  BR=$(git branch --show-current)
  SAFE=$(echo "$COMMAND" | sed "s/origin main/origin $BR/g;s/origin master/origin $BR/g")
  echo "$INPUT" | jq --arg cmd "$SAFE" '.tool_input.command = $cmd'; exit 0
fi
echo "$INPUT"; exit 0
```

Other documented uses: inject `--dry-run` on `db:migrate` unless `--execute` is present; strip `--no-verify` from `git commit` so hooks always run.

## Notes

- This repo's own `block-no-verify` hook is the *blocking* sibling of the strip-`--no-verify` use case here (it rejects rather than rewrites). It also false-positives on compound commands that merely contain `git commit` alongside other tokens — a reminder that grep-based matchers over-trigger.
- Wire with `"matcher": "Bash"`, `"type": "command"`. ENFORCEMENT layer of [[enforcement-layer-cake]].
- For untrusted *content* (not commands), see [[prompt-injection-sanitizing-hook]].
