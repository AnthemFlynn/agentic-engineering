---
title: Block destructive shell commands with a PreToolUse guard (exit 2)
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, hooks, security]
source: claude-code-pro-playbook.md (Pattern 2, Hook 2)
---

## Takeaway

A PreToolUse hook on `Bash` that pattern-matches dangerous commands and `exit 2`s to block them. Claude receives the block reason and routes around it (e.g. drafts a safer command instead).

## When it applies

Any session that can run shell. Maintain a blocklist of irreversible operations: `rm -rf /`, `rm -rf *`, `git push --force`/`-f`, `DROP TABLE`/`DROP DATABASE`, `chmod -R 777`, `truncate`.

## Why

`exit 2` is a hard stop the prompt can't override. When a dev asks Claude to "clean up the dist directory" and it drafts `rm -rf ./dist/*`, the hook blocks and Claude retries with `find ./dist -type f -delete`.

## Example

```bash
#!/bin/bash   # .claude/hooks/guard-bash.sh
INPUT=$(cat); COMMAND=$(echo "$INPUT" | jq -r '.tool_input.command // empty')
BLOCKED=("rm -rf /" "rm -rf \*" "git push --force" "git push -f" "DROP TABLE" "DROP DATABASE" "chmod -R 777" "truncate")
for p in "${BLOCKED[@]}"; do
  if echo "$COMMAND" | grep -qi "$p"; then echo "Blocked: matches '$p'" >&2; exit 2; fi
done
exit 0
```

Wire on `"matcher": "Bash"`. Remember `chmod +x .claude/hooks/*.sh`.

## Notes

- Grep blocklists over-trigger and miss obfuscations — a backstop, not the boundary. The real boundary in autonomous runs is [[allowed-tools-hard-contract]].
- To *rewrite* rather than block, see [[pretooluse-input-modification]]. Part of [[committed-settings-json-baseline]].
