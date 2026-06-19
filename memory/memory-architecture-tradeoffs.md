---
title: Choosing a memory backend — and why the write path matters more than the read path
type: reference
confidence: anecdotal
date: 2026-06-19
model:
version:
tags: [memory, architecture, vector, graph]
source: DigitalApplied "Agent Memory Architectures" (digitalapplied.com/blog/agent-memory-architectures-vector-graph-episodic); Zep (arXiv:2501.13956); mem0 (arXiv:2504.19413); "Diagnosing Retrieval vs Utilization" (arXiv:2603.02473); "Markdown Is Not Memory" (stopusingmarkdownformemory.com)
---

## Takeaway

The backend determines what reasoning you can do:

| Backend | Strength | Weakness |
|---|---|---|
| **Vector store** | fast fuzzy/semantic recall, cheap, lowest ops | flat — no relationships, weak temporal; accuracy can degrade toward 0% past ~5 entities/query |
| **Knowledge graph** (Zep/Graphiti, Cognee) | multi-hop + temporal validity + auditable traces | heaviest write path; extraction errors compound |
| **Structured / relational** | deterministic exact lookup, access control | no semantic generalization — usually the *backing store* under the others |
| **Flat files** (a `MEMORY.md`) | stable instructions/persona, git-versionable | not searchable evolving memory — "a glorified sticky note" |
| **Hybrid** (vector + graph + episodic buffer) | best recall + reasoning | highest cost; routing/eviction tuning is where deployments quietly fail |

But the bigger differentiator is the **write path**, not the read path: *verbatim* vs *LLM-extracted* vs *agent-self-edited* vs *temporally-versioned*. Everyone can "embed + cosine search."

## When it applies

Picking storage once you've decided you need memory ([[memory-vs-context-vs-rag]]). Start vector (cheapest that works); add a graph when relationships/time matter; go hybrid for anything in production beyond a quarter.

## Why

Write-time extraction (mem0, Zep) → cheap, fast, token-light reads, but ingest cost and a place to silently drop facts. Store-raw / verbatim (e.g. MemPalace) → lossless, deterministic, private, but no compression. A controlled study found **retrieval method dominates accuracy** — raw chunks with no extraction matched or beat LLM extraction — so spend the compute budget on retrieval quality, not fancy write-time extraction. (Counterpoint: extraction shrinks the read-time token footprint, which matters when reads are high-volume and latency-sensitive.)

## Notes

- A single `MEMORY.md` is the flat-file form — see [[memory-md-session-handoff]] (good for persona/state, not large evolving memory). Caching repeated context is not a backend — [[prompt-caching]].
- Temporal/contradiction handling lives here too: [[memory-conflict-and-forgetting]]. Vendor benchmark numbers are contested — [[evaluating-agent-memory]].
