---
title: Reconcile at write time and forget on purpose — don't ask the LLM to track freshness
type: pattern
confidence: proven
date: 2026-06-19
model:
version:
tags: [memory, forgetting, consistency, temporal]
source: mem0 (arXiv:2504.19413); Zep temporal KG (arXiv:2501.13956); MemoryBank / Ebbinghaus decay; "Don't Ask the LLM to Track Freshness" (arXiv:2606.01435)
---

## Takeaway

Stale and contradictory facts are the silent killers of agent memory. Three rules:

1. **Reconcile on the write path.** For each new fact, retrieve similar existing memories and emit **ADD / UPDATE / DELETE / NOOP** so contradictions never co-exist in the store.
2. **Forget on purpose.** "Passive aging is for noise; active forgetting is for facts." Tie decay to access frequency, not just age.
3. **Don't ask the LLM which version is current.** On conflict resolution, LLMs scored **18–28% vs a deterministic baseline at 78%**. Use the LLM to *extract*; use deterministic code (timestamps, `max(serial)`) to decide *current*.

## When it applies

Any evolving per-user memory. The classic failure: "user works at X" persists after it's wrong, because the user never says "I moved" — pure semantic supersession waits for a contradiction that never arrives.

## Why

Append-only stores swamp retrieval and surface contradictions; mutable stores lose history; **bi-temporal** modeling (Zep — track *valid-time* and *ingest-time*, invalidate rather than delete) keeps both, at maximum complexity. Decay (e.g. Ebbinghaus `R = e^(−t/S)`, strength +1 per retrieval) prunes stale low-value memories while frequently-used ones persist.

## Example

TTL tiers: allergies / names → ~infinite; "currently debugging X" → hours/days. Reconcile at write (ADD/UPDATE/DELETE/NOOP); pick the current fact deterministically by timestamp, not by asking the model.

## Notes

- Which backends support invalidation/temporal reasoning: [[memory-architecture-tradeoffs]]. Pairs with [[selective-memory-beats-total-recall]] — clean writes keep recall sharp.
