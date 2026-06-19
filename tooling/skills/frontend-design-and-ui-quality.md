---
title: frontend-design + Vercel UI — creative direction and a quality gate
type: reference
confidence: anecdotal
date: 2026-06-18
model:
version:
tags: [skill, frontend, design, ui]
source: claude-code-mastery-v3_2.html (S2)
---

## Takeaway

Two complementary UI skills: Anthropic's **frontend-design** commits the agent to a bold aesthetic direction (typography, palette, composition) *before* writing UI code — preventing the generic Inter-font/purple-gradient default. Vercel's **UI quality** skill is the gate after: audits code against 100+ rules (WCAG 2.1, semantic HTML, focus states, touch targets, keyboard nav).

## When it applies

Any frontend work. Use frontend-design as the creative-direction step up front; use the Vercel skill as the quality gate before shipping. They're cross-harness skills, hence filed here rather than under a harness.

## Example

```bash
npx skills add anthropics/claude-code --skill frontend-design
/frontend-design            # describe what to build → commits to a direction

npx skills add vercel/claude-code-skills
/ui-review                  # audit current UI against 100+ rules
```

## Notes

- "Creative direction skill" + "quality-gate skill" is the same two-phase shape as design-then-verify; the gate is a packaged [[rubric-as-self-verification]] for UI.
