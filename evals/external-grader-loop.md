---
title: Grade output with a fresh instance to remove authorship bias
type: pattern
confidence: anecdotal
date: 2026-06-18
model:
version:
tags: [claude-code, rubric, grading]
source: claude-code-staff-engineer-patterns.md (Pattern 3); Anthropic Outcomes (Managed Agents beta)
---

## Takeaway

Score an agent's output with a **separate instance** that reads it cold against a written rubric — it isn't influenced by the reasoning or trajectory that produced the output. Loop: draft → grade → retry on the weakest dimension → escalate to human after N attempts.

## When it applies

Outputs with a definable quality bar (PR reviews, generated docs, analyses) where the producer tends to over-rate its own work. Overkill for trivial or already-verified outputs.

## Why

A grader sharing the author's context inherits the author's blind spots. A fresh read ("score this as if you didn't write it; be adversarial") catches reviews that flagged issues but gave no fix, or missed an entire dimension. Anthropic's internal Outcomes benchmark reports ~10.1% quality improvement with no model change.

## Example

Three passes in one session:

```
Pass 1: Review the diff → write to .claude/review-draft.md
Pass 2: Fresh read. Load rubric (.claude/rubrics/pr-review.md). Score the draft
        adversarially. Write grade JSON (pass, weakest_dimension, retry_instruction).
Pass 3: If pass=false, rewrite targeting weakest_dimension, re-grade. Max 3 attempts,
        else output best version + flag REVIEW_NEEDS_HUMAN_ESCALATION.
```

Rubric scores each dimension 1–5 (specificity, actionability, false-positive rate, coverage); pass requires all ≥3.

## Notes

- Distinct from [[rubric-as-self-verification]]: that's the *author* self-checking before declaring done; this is an *independent* grader after the fact. They compose.
- Force machine-readable grades with a [[structured-output-contract]].
- PROCEDURE/PIPELINE layers of [[enforcement-layer-cake]].
