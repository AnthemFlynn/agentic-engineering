---
title: Back up working context with PreCompact, re-inject with PostCompact
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, hooks, context, compaction]
source: claude-code-mastery-v3_2.html (Level 1, P4)
---

## Takeaway

When context fills and auto-compacts, working memory is compressed and some is lost. **PreCompact** fires first — write a backup before compression. **PostCompact** fires after — re-inject context (e.g. "re-read MEMORY.md") that compaction may have dropped. Run the backup `async: true` so it never blocks execution.

## When it applies

Long sessions that will hit auto-compaction. Also shape *what* survives via a CLAUDE.md "compaction policy" section (current task, files modified, errors+resolutions, decisions) — Claude uses it to prioritize its compaction summary.

## Why

Compaction is lossy. A PreCompact backup preserves the full pre-compression transcript; PostCompact nudges the model to reload durable state it may have lost. The CLAUDE.md policy steers the summary toward what matters.

## Example

```json
{
  "hooks": {
    "PreCompact": [{"hooks": [{"type": "command", "async": true,
      "command": "cp ~/.claude/projects/$(basename $PWD)/$CLAUDE_SESSION_ID.jsonl ~/.claude/backups/session-$(date +%s).jsonl 2>/dev/null || true"}]}],
    "PostCompact": [{"hooks": [{"type": "command",
      "command": "echo '{\"additionalContext\":\"Context just compacted. Re-read .claude/MEMORY.md if you need task context that may have been lost.\"}'"}]}]
  }
}
```

## Notes

- Backups belong in [[async-hooks]] (never block on them). Durable cross-session state still lives in [[memory-md-session-handoff]]; proactive compaction discipline is [[manage-context-as-finite-resource]].
