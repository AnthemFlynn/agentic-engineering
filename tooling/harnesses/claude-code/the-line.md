---
title: "The Line" — where you stop using Claude Code and start building on it
type: reference
confidence: proven
date: 2026-06-18
model:
version:
tags: [claude-code, agent-sdk, architecture, mental-model]
source: claude-code-mastery-v3_2.html ("The Line")
---

## Takeaway

There's an altitude boundary in agent work. Above it, a human drives Claude Code in a terminal and the question is "how do I prompt this?" Below it, your *application* drives the agent loop and the question becomes "how do I design this?" — your agents are services, your MCP servers are APIs, your prompt cache is a cost center, your audit logs are compliance artifacts.

## When it applies

Use it as a decision marker. If a human is still driving, you're above the line — invest in CLAUDE.md, hooks, subagents, workflows. If your application drives the loop, you're below it — you need the Agent SDK ([[agent-sdk-budgeted-run]]), budget caps, durable execution, governance, and security that doesn't depend on prompt instructions.

## Why

The two altitudes have different failure modes and different tools. Conflating them — prompting your way through what is really a systems-design problem, or over-engineering a terminal session — is the common mistake the boundary names.

## Notes

- Everything tagged "runtime" lives below the line: [[agent-sdk-budgeted-run]], [[mcp-server-intent-grouped-design]], [[prompt-caching]], [[durable-execution-checkpoints]], [[governance-audit-shadow-mcp]]. The layered controls that span both sides: [[enforcement-layer-cake]].
