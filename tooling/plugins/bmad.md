---
title: BMAD — a spec-driven design plugin for the pre-implementation phase
type: reference
confidence: anecdotal
date: 2026-06-18
model:
version:
tags: [plugin, bmad, workflow, spec-driven]
source: claude-code-mastery-v3_2.html (S4)
---

## Takeaway

BMAD (Brain Mapping and Agentic Development) is a spec-driven plugin that forces requirements clarity *before* implementation: structured brainstorming, contradiction-finding in the spec, and validation that flags when implementation drifts from the agreed design.

## When it applies

The design phase of a feature — product design, user flows, edge-case hunting, adversarial spec review — where catching contradictions on paper is far cheaper than in code. Distinct from execution-focused plugins.

## Example

```bash
npx skills add bmad-method/bmad-claude-code
/brainstorm     # generate user flows you didn't know you needed
/doc-sharding   # break a PRD into vertical implementation slices
/validate       # check implementation against the spec
/adversarial    # find security & edge-case gaps in the design
```

## Notes

- Complements [[superpowers]]: BMAD owns design → spec → validation plan; Superpowers owns spec → tasks → subagent execution. Together they cover the SDLC with gates at each stage.
- Operationalizes [[spec-driven-workflow]] (the brainstorm → spec → plan stages) and [[vertical-slice-prompt]] (doc-sharding into slices).
