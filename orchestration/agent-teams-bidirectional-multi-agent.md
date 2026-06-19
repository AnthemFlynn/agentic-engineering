---
title: Agent teams give teammates direct, bidirectional communication
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.32+ (experimental)
tags: [claude-code, multi-agent]
source: claude-code-staff-engineer-patterns.md (Pattern 1); code.claude.com/docs/en/agent-teams
---

## Takeaway

Agent teams differ from subagents: teammates message **each other directly** (a security agent can talk to the backend agent without routing through the lead), each runs in its own context window and git worktree, and each is individually addressable.

## When it applies

Use when teammates can operate independently on bounded, separable work — per-directory ownership, competing investigations. Do NOT use for sequential tasks, same-file edits, simple bugs, or work with many interdependencies: coordination overhead and token cost outweigh the gain.

## Why

Independent contexts let each teammate stay narrowly scoped. The quality win comes from [[context-focus-beats-parallelism]], not from running things at the same time.

## Example

Enable (experimental):

```json
// .claude/settings.json
{ "env": { "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1" } }
```

Spawn in natural language: give each teammate a bounded directory it owns, and give the lead a decompose-and-assign job ("don't let them touch each other's directories"). Cycle teammates with `Shift+Down`; in tmux/iTerm2 they open as split panes.

## Notes

- Experimental as of May 2026 — verify with `claude --version` and check release notes.
- Concrete topology: [[competing-hypotheses-with-integrator]].
- Sits in the AGENT layer of the [[enforcement-layer-cake]].
