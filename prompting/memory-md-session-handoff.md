---
title: Hand off session state through a MEMORY.md that Claude writes and reads
type: pattern
confidence: proven
date: 2026-06-18
model:
version:
tags: [claude-code, context, state]
source: claude-code-staff-engineer-patterns.md (Pattern 6)
---

## Takeaway

CLAUDE.md carries static project knowledge; it can't carry *session* state — what you decided last time, what's in-progress, what's blocked. Add a MEMORY.md that a session-end command writes and a session-start command reads, so the next session resumes without re-derivation.

## When it applies

Multi-session work spanning days or weeks (migrations, large features). Single-sitting tasks don't need it.

## Why

Without it, returning after a break costs ~15 minutes re-explaining state, Claude re-reads files, and you correct stale assumptions. With it, `/session-start` reads MEMORY.md and resumes precisely. Over a months-long project the file becomes a decision log — often more useful than git history for *why* the code looks the way it does.

## Example

`session-end` writes: last updated · completed this session · in-progress state · decisions made (include "tried X, caused Y" rejections) · blockers/open questions · exact next-session start prompt. Keep sections brief; update the existing file, don't create a new one.

`session-start`: read MEMORY.md → summarize state in 3 sentences → ask "resume in-progress work or start new?" → wait.

## Notes

- The most valuable section is *rejected approaches and why* — it prevents relitigating dead ends.
- Static facts go in [[compound-claude-md-dynamic-import]]; only volatile state goes here. BEHAVIORAL layer of [[enforcement-layer-cake]].
