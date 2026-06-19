---
title: Multi-agent quality comes from context focus, not parallelism
type: tip
confidence: anecdotal
date: 2026-06-18
model:
version:
tags: [multi-agent, context]
source: claude-code-staff-engineer-patterns.md (Pattern 1, production note)
---

## Takeaway

The reason to split work across agents is **context focus per agent**, not throughput. A single agent typically degrades once it passes ~80–90% context-window utilization; teams keep each teammate around ~40%, enabling sharper reasoning in a narrower domain.

## When it applies

Whenever you're deciding *whether* to fan work out. If the task fits comfortably in one focused context, one agent is better. Reach for multiple agents when a single context would be forced past the degradation zone or be polluted by unrelated material.

## Why

Reasoning quality falls as the window fills with loosely-relevant tokens. Narrower scope per agent keeps the relevant signal dense. This reframes "more agents" as a context-management decision, not a speed decision.

## Notes

- The ~40% / ~80–90% figures are production anecdotes, not benchmarked constants — treat as direction, not thresholds.
- Implication for [[agent-teams-bidirectional-multi-agent]]: scope each teammate so it never needs the whole repo in context.
- Related lever: [[model-mixing-per-agent-role]] (right-size the model per scoped role).
