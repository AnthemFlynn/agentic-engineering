---
title: Procedural memory — agents that rewrite their own instructions and skills
type: pattern
confidence: anecdotal
date: 2026-06-19
model:
version:
tags: [memory, procedural, self-improvement, prompting]
source: CoALA (arXiv:2309.02427); Voyager (arXiv:2305.16291); Reflexion (arXiv:2303.11366); GEPA (arXiv:2507.19457); LangMem prompt-optimization docs; ACE (arXiv:2510.04618)
---

## Takeaway

Procedural memory is the agent's **how-to** knowledge — its skills, instructions, and decision logic. Unlike facts (semantic) or events (episodic), it governs *behavior*. The editable, non-parametric forms an engineer controls are the **system prompt / instructions** and a **skill library**. "Self-improvement" in 2023–2026 mostly means editing these in text or code — *not* fine-tuning weights — through one loop: **act → reflect on the trace → propose an edit → adopt**.

## When it applies

When you want an agent to get better at a recurring task over time without retraining. Three flavors of the same loop:

- **Skill library** (edit code): *Voyager* grows a library of reusable executable skills, retrieved by embedding and composed.
- **Verbal reflection** (edit text, ephemeral): *Reflexion* writes a reflection on a failure that conditions the next attempt — "verbal reinforcement," not a gradient step.
- **Prompt optimization** (edit the persistent prompt): OPRO / DSPy / GEPA / LangMem / ACE rewrite the system prompt from many traces. This is procedural memory that survives across sessions.

## Why

Editing text/code is reversible, inspectable, and cheap versus fine-tuning. And a natural-language trace is a richer learning signal than a scalar reward: GEPA's reflective prompt evolution — reading full execution traces to diagnose failures — reportedly beat RL (GRPO) by up to ~20% with ~35× fewer rollouts.

## Example

```
ACT      observe success / failure / error trace
REFLECT  diagnose in natural language — what went wrong, why
PROPOSE  a new skill, a reflection note, or a prompt rewrite
ADOPT    store / append / swap in — ideally behind an eval gate
```

LangMem exposes this as prompt optimizers (`gradient` = separate critique then proposal; `metaprompt` = direct; `prompt_memory` = single pass). ACE keeps an itemized, evolving "playbook" (bullets, not monolithic rewrites) to avoid context collapse.

## Notes

- This is the riskiest memory type to let an agent write — gate it: [[self-editing-is-the-riskiest-write]].
- The **hand-edited human version** is already in this repo: a [[claude-md-living-document]] *is* curated procedural memory, and [[compound-engineering-loop]] is the manual reflect→encode loop (correction → CLAUDE.md → hook → skill). Where it sits in the map: [[memory-types-taxonomy]].
- Frontier flag: prompt-optimization-as-memory (GEPA, ACE, ReMe arXiv:2512.10696) is 2025–26 and largely pre-peer-review; the skill-library/reflection patterns (Voyager, Reflexion) are established.
