---
title: Drive the agent loop yourself with the Agent SDK — budgeted, model-routed
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Agent SDK (@anthropic-ai/claude-agent-sdk)
tags: [claude-code, agent-sdk, cost, runtime]
source: claude-code-mastery-v3_2.html (Level 4, P1)
---

## Takeaway

The Claude Agent SDK is the same runtime that powers Claude Code, exposed as a library your application controls. `query()` returns an async iterator — each message is a step in the agent loop. Wrap it with a per-run USD ceiling, a kill switch, and model routing.

## When it applies

When your *application* drives the loop, not a human in a terminal. Route models by task: Opus for deep reasoning (architecture, complex debugging), Sonnet for standard work, Haiku for high-volume narrow tasks (classify/extract/route). The *Spiral* pattern — Haiku coordinator + Opus specialist — yields frontier quality at ~1/5 the all-Opus cost.

## Example

```ts
for await (const msg of query({ prompt, options: new ClaudeAgentOptions({
  model: selectModel(prompt),        // opus|sonnet|haiku by task regex
  systemPrompt: STATIC_SYSTEM_PROMPT, // always cached — see prompt caching
  allowedTools: ["Read","Grep","Glob","mcp__internal__get_project_status"],
  maxTurns: 20,
})})) {
  if (msg.usage) { spent += cost(msg.usage); if (spent > maxUsd) throw new Error("Budget exceeded"); }
  if (msg.type === "result") result = msg.result ?? "";  // check msg.subtype, NOT is_error
}
```

## Notes

- **Known SDK bug:** check `message.subtype` (e.g. `error_max_turns`), not `is_error` — `is_error` doesn't flag max-turns termination as an error.
- Model IDs are version-sensitive (the source predates Opus 4.8) — verify current IDs. Routing rationale: [[model-mixing-per-agent-role]]. Cache the system prompt: [[prompt-caching]]. Survive interruption: [[durable-execution-checkpoints]]. Billing note: as of June 2026 SDK usage draws a separate monthly Agent SDK credit, distinct from interactive limits. This is below [[the-line]].
