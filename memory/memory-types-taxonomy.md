---
title: The memory map — working vs long-term, episodic/semantic/procedural, parametric vs external
type: reference
confidence: proven
date: 2026-06-19
model:
version:
tags: [memory, taxonomy, architecture]
source: CoALA — Cognitive Architectures for Language Agents (arXiv:2309.02427); Wu et al. "From Human Memory to AI Memory" (arXiv:2504.15965); RAG (Lewis et al., arXiv:2005.11401)
---

## Takeaway

Two orthogonal cuts organize the whole space:

1. **Locality** — *working / short-term* (whatever is in the context window right now: ephemeral, token-limited, the only memory the model directly reasons over) vs *long-term* (external, persisted, retrieved on demand).
2. **Cognitive type** of long-term memory (from CoALA): **episodic** (events/experiences), **semantic** (facts/knowledge), **procedural** (skills/how-to).

A third cut crosses both: **parametric** (knowledge baked into weights — fast, opaque, hard to edit) vs **non-parametric / external** (in retrievable stores — inspectable, citable, updatable). Memory *type* is largely independent of storage *backend*.

## When it applies

Whenever you decide what an agent should remember. Pick the type per use case first, then the backend — the type dictates the write/retrieve pattern.

## Why

Each type wants a different mechanism: episodic → append-only log + scored retrieval; semantic → curated, deduplicated store; procedural → mostly your code and the model's weights. CoALA's load-bearing warning: writing to **procedural** memory (an agent editing its own decision logic) is *significantly riskier* than writing episodic or semantic memory — treat self-modifying procedures with extreme caution.

## Example

- semantic: "the user is vegetarian" · episodic: "last Tuesday I booked the user an aisle seat" · procedural: the agent's tool-use loop.
- parametric: the model knowing Paris is France's capital with no retrieval — updated only by fine-tuning/model-editing (slow, opaque). non-parametric: that same fact in a vector DB — updated by *writing*.

## Notes

- Comes after the [[memory-vs-context-vs-rag]] decision; backend choice is [[memory-architecture-tradeoffs]]. Procedural memory the agent edits itself is [[procedural-memory-self-rewriting]] — gate it per [[self-editing-is-the-riskiest-write]].
- Terminology flag: the non-weight side is variously called "non-parametric" / "textual" / "contextual" across surveys — "non-parametric" is the safest shared term. The distinction originates in the 2020 RAG paper.
