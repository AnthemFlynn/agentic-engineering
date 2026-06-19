---
title: Manage the context window as your most finite resource
type: pattern
confidence: proven
date: 2026-06-18
model:
version:
tags: [context, claude-code, sessions]
source: claude-code-field-guide-may2026.md (section 4)
---

## Takeaway

Context degradation is the primary failure mode of long agent sessions. Past ~40–60 minutes / 60K+ tokens, the agent starts making mistakes it wouldn't make fresh — confusing related function names, forgetting it already fixed something, re-reading files. Protect the window proactively instead of reacting once things break.

## When it applies

Any session that runs long or spans unrelated tasks. The tells: repeated small errors, the agent re-reading known files, or correcting the same issue more than twice.

## Why

A context window is not a kitchen sink — every accumulated token of back-and-forth dilutes the relevant signal. Proactive resets and delegation keep the active context dense with what matters now.

## Example

In Claude Code specifically:

- `/clear` between unrelated tasks — don't carry one task's residue into the next.
- `/compact` proactively at ~70% usage, not reactively at failure.
- If you've corrected the same issue more than twice, clear and start fresh (and capture the rule — see [[diagnostic-prompt-to-claude-md]]).
- Delegate research/exploration to a subagent so investigation logs never enter the main session.

## Notes

- 2025 → 2026 shift: power users used to manage this very manually (aggressive clearing, external artifact dirs); maturing auto-compaction and plan mode now absorb much of the overhead. The principle is unchanged; the manual cost dropped.
- The single-session sibling of [[context-focus-beats-parallelism]] (which is about splitting *across* agents). Delegation mechanism: [[subagent-codebase-explorer]].
