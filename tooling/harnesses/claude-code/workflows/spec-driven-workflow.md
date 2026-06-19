---
title: Plan before Claude touches a file — the spec-driven workflow
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, planning, workflow]
source: claude-code-field-guide-may2026.md (section 3)
---

## Takeaway

The most expensive mistake in Claude Code is letting it code before you've agreed on *what* to build — 200 lines solving the wrong problem costs more than the seconds it saved. Enter plan mode (`/plan` or `Shift+Tab`) for anything architectural, multi-file, or ambiguous: Claude explores and proposes without touching code; you review and redirect; then execute.

## When it applies

Architectural, multi-file, or ambiguous work. Skip for one-line mechanical edits where the cost of a wrong edit is trivial.

## Why

The pause costs ~nothing; wrong edits cost a debugging session. Reviewing a spec while it's cheap to change beats discovering the wrong direction after code hits disk.

## Example

The five-stage pipeline teams report working well:

1. **Brainstorm** — describe the goal; let Claude ask about scope and constraints.
2. **Spec** — Claude writes `docs/specs/<date>-<feature>.md`; challenge and change it while it's cheap.
3. **Plan** — Claude converts the spec into an ordered task list with exact file paths and per-task verification commands.
4. **Review the plan** — last chance before disk: right order? anything missing?
5. **Execute** — Claude dispatches a subagent per task, each implementing, testing, and committing.

Build tasks as vertical slices (DB + service + UI together), not horizontal phases, for end-to-end feedback from task one.

## Notes

- The spec artifact discipline: [[plan-command-as-spec]]. Slicing: [[vertical-slice-prompt]]. Per-task isolation: [[context-focus-beats-parallelism]], [[worktrees-parallel-features]]. Choosing the execution tier: [[skills-subagents-agent-teams-spectrum]].
