---
title: When Claude repeats a mistake, diagnose the root cause into CLAUDE.md
type: pattern
confidence: proven
date: 2026-06-18
model:
version:
tags: [claude-code, claude-md, debugging]
source: claude-code-pro-playbook.md (Pattern 10)
---

## Takeaway

When Claude keeps making the same mistake, stop correcting the symptom in-session — those corrections don't persist. Instead run a diagnostic prompt that makes Claude name the rule, explain why it keeps missing it, and propose the exact CLAUDE.md text to prevent it permanently.

## When it applies

Any recurring error you've corrected 2–3+ times in a session. If it's a one-off, just fix it; this is for patterns that signal missing or ambiguous persistent context.

## Why

In-session corrections live only in that conversation. Forcing Claude to articulate the rule surfaces *why* it's failing (missing context vs. ambiguous instruction vs. conflicting rule), and the proposed CLAUDE.md addition turns a transient fix into a durable one.

## Example

```
Stop. Don't fix the code yet.
I've corrected you on [issue] three times. Before continuing:
1. Explain in your own words the rule you're supposed to follow.
2. Explain why you keep getting it wrong (missing context? ambiguous? conflicting rule?).
3. Propose the exact text to add to CLAUDE.md to prevent this — include the WHY.
After I approve the addition, then fix the code.
```

Typical output: *"Always import utilities from @company/core, not @company/utils. @company/utils was deprecated in v3.2. See docs/migration-v3.md."* You approve, it's committed, done permanently.

## Notes

- The escalation path for [[claude-md-living-document]]'s correction loop when a simple add doesn't stick.
