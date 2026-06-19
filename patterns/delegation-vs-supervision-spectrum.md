---
title: Decide per task: fully delegate, supervise closely, or don't delegate
type: pattern
confidence: proven
date: 2026-06-18
model:
version:
tags: [workflow, review, judgment]
source: claude-code-field-guide-may2026.md (sections 5 & meta)
---

## Takeaway

The best practitioners are deliberate about *where each task falls* on a supervision spectrum — they don't apply one trust level to everything. Anthropic's 2026 developer report: devs use AI in ~60% of work but fully delegate only 0–20% of tasks.

## When it applies

Before handing any task to an agent. Sort it into one of three buckets up front; the bucket sets how much you review.

## Why

AI-generated code often "works" superficially while hiding subtle bugs, and the cost of a miss scales with the domain. Calibrating supervision to stakes — rather than trusting or distrusting uniformly — is what separates high-leverage use from either over-checking or shipping silent defects.

## Example

- **Fully delegate (low supervision):** test generation, boilerplate, migrations, docs, formatting, dependency audits, repetitive cross-file refactors.
- **Supervise closely:** auth flows, payment code, data mutations, security-sensitive paths, load-bearing architectural decisions.
- **Don't delegate:** system security settings, environment credentials, production deploys without a human checkpoint.

For the "supervise closely" bucket, tests are the only reliable validation — superficial success isn't proof; pair them with manual review.

## Notes

- Verification mechanisms for the middle bucket: [[rubric-as-self-verification]], [[writer-reviewer-loop]]. Hard guardrails for the bottom: [[enforcement-layer-cake]], [[committed-settings-json-baseline]].
- The takeaway behind it: treat the agent as a programmable platform (rules + hooks + skills + isolation + tools), and prompts become almost incidental.
