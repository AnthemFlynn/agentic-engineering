---
title: Mix models by role — cheap for high-frequency coordination, expensive for rare deep work
type: pattern
confidence: anecdotal
date: 2026-06-18
model:
version:
tags: [cost, multi-agent, routing]
source: claude-code-staff-engineer-patterns.md (Patterns 4–5); Anthropic "Code with Claude" case studies
---

## Takeaway

Assign different models to different agents in the same team. Invert the naive expectation: put the **cheap** model on the high-frequency coordination/routing work and the **expensive** model on the low-frequency, high-stakes deep work.

## When it applies

Any multi-agent setup with a dispatcher + specialists. The coordinator reads diffs and routes — Haiku is fine. A security specialist on auth/payments — Opus is worth it. Pattern-recognizable work (perf: N+1, unbounded loops) — Sonnet.

## Why

Coordination fires constantly and needs little reasoning; deep analysis fires rarely and a miss is expensive. Spending the token budget where reasoning matters is what gives "frontier quality at a fraction of the cost." The *Spiral* pattern (Haiku specialist + Opus lead) reports frontier-level quality at ~1/5 the cost.

## Example

Set `model:` in each subagent's frontmatter:

```markdown
# .claude/agents/review-coordinator.md → model: haiku   (reads diffs, routes, synthesizes; no analysis)
# .claude/agents/security-analyst.md   → model: opus    (adversarial; misses are expensive)
# .claude/agents/performance-analyst.md→ model: sonnet  (pattern-recognizable issues)
```

## Notes

- Cost check: a 200–500 line PR review on Sonnet ≈ $0.02–0.05; ~10 PRs/day ≈ $30–50/mo. Reserve Opus for scheduled deep audits, not every push.
- Cost numbers are model/date-sensitive (verify current pricing) — see [[claude-api]] for live rates.
- Pairs with [[context-focus-beats-parallelism]]; lives in the AGENT layer of [[enforcement-layer-cake]].
