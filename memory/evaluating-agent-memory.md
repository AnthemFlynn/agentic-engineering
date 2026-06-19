---
title: Evaluating agent memory — the benchmarks are immature, so validate on your own data
type: reference
confidence: anecdotal
date: 2026-06-19
model:
version:
tags: [memory, evals, benchmarks]
source: LongMemEval (arXiv:2410.10813); LoCoMo (snap-research.github.io/locomo); MemBench (arXiv:2506.21605); Convomem (arXiv:2511.10523); Zep↔mem0 LoCoMo dispute (blog.getzep.com)
---

## Takeaway

Memory is a measurable bottleneck — commercial assistants drop **~30% in accuracy** when forced to recall across sustained multi-session interactions (LongMemEval). But the leading benchmarks have documented validity problems and vendor numbers are openly contested, so treat any published figure as **directional** and validate on your own data with the metric you actually care about.

## When it applies

Choosing, building, or claiming a memory system — especially when comparing vendors, whose numbers often aren't comparable (different splits; *retrieval Recall@K* vs *end-to-end QA accuracy* are not the same metric).

## Why

- **LoCoMo** has documented inaccurate gold answers and only ~10 conversations — statistically underpowered.
- **LongMemEval** sources filler conversations from *other* benchmarks, creating a stylistic tell that lets systems shortcut genuine retrieval.
- **MemBench** adds a useful **capacity** axis: how performance degrades as the store grows.
- The Zep↔mem0 LoCoMo dispute (84% → 58.44% → 75.14% across rebuttals) shows the numbers are a marketing battleground.
- **Convomem**'s finding that "the first ~150 conversations don't need RAG" is itself a critique — naive full-context can beat retrieval at small scale, so many benchmarks don't isolate *when* memory actually helps.

## Example

Build a small eval set from your own traffic. Measure the ability you need (multi-session reasoning, temporal updates, abstention) and the outcome you care about (task success, not just Recall@K). Score with a fresh-context grader — see [[external-grader-loop]].

## Notes

- The "more memory = worse" result lives in [[selective-memory-beats-total-recall]]; capacity degradation as the store grows ties back to [[memory-architecture-tradeoffs]].
