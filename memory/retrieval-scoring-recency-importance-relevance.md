---
title: Score memories by recency × importance × relevance, then hybrid-retrieve and rerank
type: reference
confidence: proven
date: 2026-06-19
model:
version:
tags: [memory, retrieval, scoring]
source: Generative Agents (Park et al., UIST 2023, arXiv:2304.03442); Reciprocal Rank Fusion (Azure AI Search docs); "From BM25 to Corrective RAG" rerank benchmark (arXiv:2604.01733)
---

## Takeaway

Pure vector top-*k* is the floor, not the ceiling. The canonical episodic-memory retrieval score (Generative Agents) is a weighted sum of three normalized terms:

```
score = α_recency·recency + α_importance·importance + α_relevance·relevance
```

with all α = 1, each term min-max normalized to [0,1]:
- **recency** = exponential decay, `0.995^(hours since last retrieval)`
- **importance** = LLM-assigned poignancy, 1–10, set at write time
- **relevance** = cosine similarity between query and memory embeddings

For production precision, layer **hybrid retrieval** (BM25 + dense vector, fused with Reciprocal Rank Fusion) then a **cross-encoder reranker**.

## When it applies

Building the read path. Recency/importance weighting matters most for *episodic* memory; hybrid + rerank for any precision-sensitive recall.

## Why

Similarity alone ignores "when" and "how important," so it surfaces stale or trivial-but-similar memories. BM25 catches exact matches/codes that dense retrieval misses; RRF fuses by *rank position* (no score normalization needed); a cross-encoder reranker adds roughly **+17pp MRR@3** over unreranked hybrid.

## Example

```
RRF_score(d) = Σ over retrievers  1 / (k + rank_r(d))      # k = 60 is the standard constant
```

Complexity ladder: vector-only → hybrid (BM25 + vector + RRF) → + cross-encoder rerank. Each rung adds latency/infra for precision — match the rung to your recall SLA.

## Notes

- Scoring is independent of backend ([[memory-architecture-tradeoffs]]); the `importance` term is assigned on the write path, which is also where you gate what gets stored — see [[selective-memory-beats-total-recall]].
