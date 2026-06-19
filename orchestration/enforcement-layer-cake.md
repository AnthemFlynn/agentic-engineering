---
title: Stack five layers, each enforcing what the layer below can't guarantee
type: reference
confidence: proven
date: 2026-06-18
model:
version:
tags: [claude-code, architecture, security]
source: claude-code-staff-engineer-patterns.md (architecture mental model)
---

## Takeaway

Production-grade consistency comes from layering controls, where each higher layer is a *hard* guarantee for what the softer layer beneath can only suggest:

```
ENFORCEMENT (cannot be bypassed)
├── --allowedTools          hard tool whitelist in headless runs
├── PreToolUse hooks        exit 2 = blocked; rewrite stdin = redirected
└── permissions.deny        files invisible to Claude
BEHAVIORAL (advisory, ~70–80% reliable)
├── CLAUDE.md root          ~60 lines of invariants
├── @imported docs          conditional, loads on relevance
└── MEMORY.md               session-state handoff
PROCEDURE (invoked on demand)
├── Skills                  reusable workflows
├── Slash commands          explicit invocation
└── Rubrics                 quality gates
AGENT (orchestration)
├── Subagents               isolated workers
├── Agent teams             bidirectional, multi-context
└── Model mixing            Haiku/Sonnet/Opus per role
PIPELINE (no human in loop)
├── Headless mode           claude -p with --bare + --allowedTools
├── GitHub Actions          anthropics/claude-code-action@v1
└── Grading loops           draft → grade → retry → escalate
```

## When it applies

When you need reliability, not just a good session. Anything advisory (CLAUDE.md) will be violated ~20–30% of the time; back every must-hold invariant with an enforcement-layer control.

## Why

Behavioral guidance is probabilistic. The enforcement layer is mechanical: a tool not in `--allowedTools` literally cannot fire; a `permissions.deny` file is invisible. Teams that get consistency build the lower layers, not just the top two.

## Notes

- Per-layer entries: [[allowed-tools-hard-contract]], [[pretooluse-input-modification]], [[compound-claude-md-dynamic-import]], [[memory-md-session-handoff]], [[external-grader-loop]], [[agent-teams-bidirectional-multi-agent]], [[model-mixing-per-agent-role]], [[headless-mode-ci-primitive]].
