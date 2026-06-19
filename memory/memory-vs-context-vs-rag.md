---
title: Memory, context management, and RAG are three different problems
type: pattern
confidence: proven
date: 2026-06-19
model:
version:
tags: [memory, context, rag, architecture]
source: Anthropic "Effective context engineering" (anthropic.com/engineering/effective-context-engineering-for-ai-agents); Atlan "AI Memory System vs RAG" (atlan.com/know/ai-memory-system-vs-rag); mem0 "RAG vs AI Memory" (mem0.ai/blog/rag-vs-ai-memory)
---

## Takeaway

Don't conflate them. A quick litmus test:

- **Same answer for everyone → RAG.** Read-only retrieval over a static corpus; relevance is a property of the *content*.
- **Different answer per user, evolving over time → agent memory.** Has a *write path the agent itself uses*; relevance is a property of the *user*.
- **Fits in this session → just context management.** Compaction, clearing, trimming.

The distinguishing feature of memory is the write path — the agent decides what to store and reconciles updates when facts change.

## When it applies

Whenever you're tempted to "add memory." Very often the real need is context management or RAG, and a memory subsystem is over-engineering that adds a persistence layer and a poisoning surface for no benefit.

## Why

Memory costs you a write path, persistence, reconciliation, and an attack surface. RAG answers "what does this document say?"; memory answers "what does this user need?" Reaching for a memory store to solve a context-window problem buys complexity, not capability.

## Example

Work the ladder top-down, cheapest first:

1. **Context window** — tool-result clearing, compaction, structured note-taking. Done if state fits the session.
2. **RAG** — knowledge that's the same for everyone, single-turn-ish, kept fresh by re-indexing.
3. **Memory** — per-user state that must survive a session reset and evolve.

The 2026 production default is **all three at once**: RAG for universal knowledge + memory for personalization + context management for the live task.

## Notes

- The context layer in depth: [[manage-context-as-finite-resource]]. A file-based, session-scoped form of memory: [[memory-md-session-handoff]]. Note that [[prompt-caching]] makes repeated context *cheap to transport* but is **not** memory — it doesn't organize, reconcile, or forget.
- Once you've decided you need memory, pick the type ([[memory-types-taxonomy]]) then the backend ([[memory-architecture-tradeoffs]]).
