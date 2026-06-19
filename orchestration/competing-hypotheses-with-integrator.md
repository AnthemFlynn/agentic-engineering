---
title: Debug with parallel hypothesis agents and an unbiased integrator
type: pattern
confidence: anecdotal
date: 2026-06-18
model:
version:
tags: [multi-agent, debugging]
source: claude-code-staff-engineer-patterns.md (Pattern 1, debugging use case)
---

## Takeaway

For a bug with several plausible root causes, assign one investigator per hypothesis, have each write findings to its own file, then have a separate **integrator** read all findings and synthesize the likely cause — only after every investigation is done.

## When it applies

Ambiguous bugs where pursuing one theory first risks anchoring (e.g. "is the timeout a connection-pool leak or a webhook retry loop?"). Not worth the overhead for bugs with an obvious single cause.

## Why

Investigators run in parallel without seeing each other's work, so no shared anchoring. The integrator never pursued any single path, so it synthesizes without the sunk-cost bias of the engineer who chased one theory.

## Example

```
investigator-A: hypothesis = connection-pool exhaustion.
  Investigate src/db/pool.ts + callers; write findings to .claude/debug/hypothesis-a.md
investigator-B: hypothesis = Stripe webhook retry loop.
  Investigate src/webhooks/stripe.ts; write findings to .claude/debug/hypothesis-b.md
integrator: do not start until BOTH files exist. Read both, synthesize root cause, propose fix.
```

## Notes

- The file-handoff + "don't start until both exist" gate is the coordination mechanism — no direct messaging required.
- A concrete instance of [[agent-teams-bidirectional-multi-agent]] exploiting [[context-focus-beats-parallelism]].
