---
title: Multi-agent quality comes from context focus, not parallelism
type: tip
confidence: anecdotal
date: 2026-06-18
model:
version:
tags: [multi-agent, context]
source: claude-code-staff-engineer-patterns.md (Pattern 1, production note); claude-code-field-guide-may2026.md (section 6)
---

## Takeaway

The reason to split work across agents is **context focus per agent**, not throughput. A single agent typically degrades once it passes ~80–90% context-window utilization; teams keep each teammate around ~40%, enabling sharper reasoning in a narrower domain.

## When it applies

Whenever you're deciding *whether* to fan work out. If the task fits comfortably in one focused context, one agent is better. Reach for multiple agents when a single context would be forced past the degradation zone or be polluted by unrelated material.

## Why

Reasoning quality falls as the window fills with loosely-relevant tokens. Narrower scope per agent keeps the relevant signal dense. This reframes "more agents" as a context-management decision, not a speed decision.

## Why subagents, specifically

The under-appreciated value of subagents is **isolation, not parallelism**. Delegated research, exploration, or verification keeps its verbose output — file searches, failed approaches, log dumps — in the subagent's own window; only the summary returns. Three patterns that consistently pay off: *research isolation*, *writer/reviewer* split, and *test/implementation* split.

But subagents aren't free — spawning one to "rename a variable" is pure overhead. Use them only for work that is genuinely independent, isolated, or would pollute the main session if run inline.

## Notes

- The single-session counterpart (clear/compact one window) is [[manage-context-as-finite-resource]]; the overhead-vs-isolation tradeoff across primitives is [[skills-subagents-agent-teams-spectrum]].
- The ~40% / ~80–90% figures are production anecdotes, not benchmarked constants — treat as direction, not thresholds.
- Implication for [[agent-teams-bidirectional-multi-agent]]: scope each teammate so it never needs the whole repo in context.
- Related lever: [[model-mixing-per-agent-role]] (right-size the model per scoped role).
