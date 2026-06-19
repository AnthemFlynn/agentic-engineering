---
title: Block writes to sensitive files with a PreToolUse path guard
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, hooks, security]
source: claude-code-pro-playbook.md (Pattern 2, Hook 3)
---

## Takeaway

A PreToolUse hook on `Write|Edit` that inspects `file_path` and `exit 2`s if it matches a protected pattern (`.env*`, `*.pem`, `*.key`). Stops Claude from "simplifying" or wiping secrets before the write hits disk.

## When it applies

Any repo with secret/config files Claude should never edit programmatically. Complements `permissions.deny` (which hides files from *reads*) by guarding *writes*.

## Why

Claude sometimes decides to tidy `.env` by removing "unused" keys. A path guard makes that write fail mechanically, regardless of intent.

## Example

```bash
#!/bin/bash   # .claude/hooks/protect-files.sh
INPUT=$(cat); FILE_PATH=$(echo "$INPUT" | jq -r '.tool_input.file_path // empty')
PROTECTED=(".env" ".env.local" ".env.production" ".env.staging" "*.pem" "*.key")
for p in "${PROTECTED[@]}"; do
  if [[ "$FILE_PATH" == *"$p"* ]]; then
    echo "Blocked: $FILE_PATH is protected. Edit manually." >&2; exit 2
  fi
done
exit 0
```

## Notes

- Pair with `permissions.deny: ["Read(./.env)", ...]` in [[committed-settings-json-baseline]] to cover both read and write.
- Sibling guard for commands: [[block-destructive-bash]].
