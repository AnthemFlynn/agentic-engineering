---
title: Forks inherit full history; subagents start fresh — pick by context need
type: tip
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, subagents, context]
source: claude-code-mastery-v3_2.html (Level 2, primitives)
---

## Takeaway

A **subagent** starts with a clean context and returns only a summary — ideal for isolating noisy work. A **fork** inherits the full conversation history — use it when the delegated work needs all the background and starting fresh would mean re-establishing too much context.

## When it applies

Reach for a subagent when the task is self-contained and you want isolation (research, review). Reach for a fork when the task is continuous with the current thread and the background is the point — a fresh subagent would have to re-derive it.

## Why

The two trade isolation against continuity. Subagents protect the main context but lose shared history; forks keep history but carry its weight. Matching the choice to whether the work needs the backstory avoids both re-deriving context and polluting the main window.

## Notes

- Subagent isolation in depth: [[context-focus-beats-parallelism]], [[subagent-codebase-explorer]]. Both sit on the [[skills-subagents-agent-teams-spectrum]].
