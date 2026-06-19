---
title: Store less — more memory measurably makes agents worse
type: pattern
confidence: proven
date: 2026-06-19
model:
version:
tags: [memory, anti-pattern, retrieval]
source: "The Forgetting Problem" (tianpan.co/blog/2026-04-12-the-forgetting-problem-when-agent-memory-becomes-a-liability); mem0 "State of AI Agent Memory 2026" (mem0.ai/blog/state-of-ai-agent-memory-2026)
---

## Takeaway

"Store everything" is the master memory anti-pattern. Recall quality is bounded not by what you *can* store but by how well you can **suppress everything irrelevant** — every junk entry competes in top-*k* and crowds out the right one. Reported results: "add-all" agents scored **13% vs 39%** (medical reasoning) and **32% vs 51%** (autonomous driving) against *selective* memory. More memory was net-negative.

## When it applies

Every memory *write* decision. Quality-gate writes; never persist raw transcripts wholesale, and never persist a model-invented statement as memory unless a tool result or trusted source backs it.

## Why

An agent that remembers everything recalls badly. Worse, bad memories compound: a stored hallucination becomes retrieved context that spuriously corroborates itself — a self-poisoning quality-collapse spiral ("training on your own outputs"). Unbounded growth also dilutes attention and runs up latency and token cost.

## Example

- Gate each write with an importance/reflection score instead of appending all; selective addition bought ~10 accuracy points over naive growth in practitioner tests.
- Separate an automatic, exhaustive **event log** from a deliberately curated **semantic** store — conflating them produces noisy retrieval.
- Pin only facts that must *always* be true (always-visible memory costs tokens every turn) — retrieve everything else.

## Notes

- Exact percentages are directional — memory benchmarks are immature and vendor-contested; see [[evaluating-agent-memory]].
- The attention-dilution mechanism is [[manage-context-as-finite-resource]]. Keeping the store clean over time is [[memory-conflict-and-forgetting]]. The "never persist invented facts" rule is also an anti-poisoning control: [[memory-poisoning-and-governance]].
