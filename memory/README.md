# Memory

Agent memory systems — how an agent persists and recalls knowledge beyond a single context window.

**In scope:** long-term / cross-session memory, retrieval and recall, memory architectures (vector stores, knowledge graphs, memory-palace schemes), what to remember and when to forget, and benchmarking memory quality.

**Out of scope:** single-session context-window management (→ [prompting/](../prompting/), e.g. compaction and `/clear`); Claude-Code-specific session-state handoff (→ [tooling/harnesses/claude-code/](../tooling/harnesses/claude-code/)).

## Notes

- [Memory, context management, and RAG are three different problems](memory-vs-context-vs-rag.md)
- [The memory map — types taxonomy](memory-types-taxonomy.md)
- [Store less: more memory makes agents worse](selective-memory-beats-total-recall.md)
- [Retrieval scoring (recency × importance × relevance) + hybrid + rerank](retrieval-scoring-recency-importance-relevance.md)
- [Backend tradeoffs (vector / graph / structured / files / hybrid)](memory-architecture-tradeoffs.md)
- [Reconcile at write time and forget on purpose](memory-conflict-and-forgetting.md)
- [Poisoning & governance — memory as an attack surface](memory-poisoning-and-governance.md)
- [Evaluating agent memory](evaluating-agent-memory.md)
- [Procedural memory — agents that rewrite their own instructions & skills](procedural-memory-self-rewriting.md)
- [Self-editing is the riskiest write — gate it with evals](self-editing-is-the-riskiest-write.md)

## Repos to watch

External memory systems worth following:

- [MemPalace/mempalace](https://github.com/MemPalace/mempalace) — local-first, verbatim (zero-LLM) memory with structured indexing; recall-benchmark-focused.
- [letta-ai/letta](https://github.com/letta-ai/letta) — MemGPT successor; OS-style hierarchical memory the agent self-edits via tools.
- [mem0ai/mem0](https://github.com/mem0ai/mem0) — drop-in memory layer; LLM fact-extraction over a hybrid vector/graph store.
- [getzep/graphiti](https://github.com/getzep/graphiti) — temporal (bi-temporal) knowledge-graph memory engine behind Zep.
