---
title: Treat `claude -p` as a composable Unix primitive for CI
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code (headless / -p)
tags: [claude-code, ci, headless]
source: claude-code-staff-engineer-patterns.md (Pattern 4)
---

## Takeaway

`claude -p "prompt"` prints to stdout and exits — composable like any CLI tool. Four flags make it CI-ready:

```bash
claude -p "..." \
  --bare \                        # no user-config bleed → reproducible across runners
  --output-format stream-json \   # structured, loggable; each tool call is a JSON line
  --max-turns 15 \                # cap the agentic loop; prevent runaway jobs
  --allowedTools "Read,Grep,Glob" # hard tool allowlist
```

## When it applies

Automated, no-human-in-the-loop runs: PR review on push, dependency audits, scheduled checks. For interactive work the flags are unnecessary.

## Why

`--bare` is the one most teams miss: without it, CI behavior depends on whatever is in `~/.claude/` on the runner image, so results vary by machine. With it, runs are deterministic. The other three bound cost, structure the output, and constrain capability.

## Example

In GitHub Actions, use `anthropics/claude-code-action@v1` (set `model:`, `max_turns`, `prompt`); for dedup, fetch prior bot comments and instruct "only report NEW issues." In GitLab/other CI, install `@anthropic-ai/claude-code`, pipe `git diff origin/main...HEAD` into `claude -p`, capture `review.json` as an artifact.

## Notes

- Cost: a 200–500 line PR on Sonnet ≈ $0.02–0.05; pick the model per job via [[model-mixing-per-agent-role]].
- The real safety boundary is the whitelist: [[allowed-tools-hard-contract]]. Output should be a [[structured-output-contract]].
- PIPELINE layer of [[enforcement-layer-cake]].
