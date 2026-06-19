---
title: Skills → Subagents → Agent Teams is a cost-vs-isolation spectrum
type: reference
confidence: proven
date: 2026-06-18
model:
version:
tags: [orchestration, subagents, skills, multi-agent]
source: claude-code-field-guide-may2026.md (section 8)
---

## Takeaway

The three reuse/isolation primitives form one spectrum. Pick the **lowest-overhead tier that still gives the isolation you need**:

```
Skills ──────────── Subagents ──────────── Agent Teams
(same context)      (isolated context)     (separate process)
low cost            parallelism            full isolation
```

## When it applies

Every "how should I structure this work" decision. The wrong choice has predictable failure modes: a CLAUDE.md that grows into a procedures doc (should be a skill), a skill doing work that pollutes context (should be a subagent), or a subagent fighting for shared files (should be a teammate in its own worktree).

## Why

Isolation and parallelism cost overhead and tokens. Moving right buys independence but pays for it; moving left is cheap but shares context. Matching the tier to the actual need avoids both bloat (too far left) and waste (too far right).

## Example

Team rollout order mirrors the spectrum's cost: **start with skills** (easiest, most portable — they work across Claude Code, Codex, and Cursor unmodified), **add hooks** when you need deterministic enforcement, **introduce subagents** when parallelism or context isolation genuinely matters.

## Notes

- Refines the AGENT layer of the [[enforcement-layer-cake]].
- Tiers in depth: skills [[create-pr-skill]], subagent isolation [[context-focus-beats-parallelism]], teams [[agent-teams-bidirectional-multi-agent]].
