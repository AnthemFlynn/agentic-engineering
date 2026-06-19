---
title: Force schema-shaped JSON output so pipelines parse without string-scraping
type: pattern
confidence: proven
date: 2026-06-18
model:
version:
tags: [claude-code, output, ci]
source: claude-code-staff-engineer-patterns.md (Patterns 4 & 9)
---

## Takeaway

When an agent's output feeds a downstream step, specify an exact JSON schema and demand "output ONLY valid JSON matching this schema." Combine with `--output-format json` in headless runs so the contract is machine-readable end to end.

## When it applies

Any agent output consumed by code rather than a human: CI gates, grade objects, issue lists, routing decisions. Skip it when the consumer is a person reading prose.

## Why

Free-form prose forces brittle string parsing downstream. A declared schema makes `jq '.result'` (or any parser) reliable, and makes the agent's "done/not-done" decision a boolean the pipeline can branch on.

## Example

```
Review this PR diff. Output ONLY valid JSON matching:
{ "summary": string,
  "issues": [{"file": string, "line": number,
              "severity": "critical|high|medium|low",
              "description": string, "fix": string}],
  "pass": boolean,
  "recommendation": "approve|request_changes|needs_discussion" }
```

```bash
claude -p "$PROMPT" --bare --output-format json --max-turns 8 > review.json
jq -r '.result' review.json
```

## Notes

- The machine-readable backbone of [[external-grader-loop]] and CI gating in [[headless-mode-ci-primitive]].
- Keep the schema small and flat; deeply nested schemas raise malformed-output risk.
