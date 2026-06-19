---
title: A codebase-explorer subagent that researches without polluting main context
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, subagents, context]
source: claude-code-pro-playbook.md (Pattern 4)
---

## Takeaway

Delegate exploration of an unfamiliar module to a subagent whose only job is to investigate and return a structured summary. The grep output, dead-ends, and file reads stay in the subagent's context; only the distilled summary returns to your main session.

## When it applies

Before implementing against a system you don't yet understand. Restrict the agent to read/search tools and explicitly forbid it from writing code — investigation only.

## Why

Exploration is the biggest source of main-context pollution. Isolating it preserves your working context for the actual implementation — a direct application of [[context-focus-beats-parallelism]].

## Example

```markdown
# .claude/agents/codebase-explorer.md
---
name: codebase-explorer
description: Understand how a module/system works before implementing. Investigation only — do NOT write code.
tools: Read, Grep, Glob, Bash
model: sonnet
---
You explore, understand, and summarize. You do NOT write production code.
Return: 1) how it works now (2–3 paragraphs) 2) key files + roles 3) patterns to follow
4) gotchas / what NOT to do 5) open questions you couldn't answer from code alone.
```

Invoke: *"Use codebase-explorer to research how our notification system works — how it sends email today, the template system, where preferences live, retry behavior."*

## Notes

- Sibling reviewer subagent: [[subagent-code-reviewer]]. Model choice per role: [[model-mixing-per-agent-role]].
