# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

A curated knowledge base for **Agentic Engineering** — shared knowledge, tips, tricks, hacks, patterns, and hard-won lessons about building and operating AI agents.

This is a **content repository**, not an application. Entries are reference material meant to be read by humans and by future agents. There is no build, no test suite, and no runtime — so do not invent `build`/`lint`/`test` commands or CI steps. If tooling is added later (e.g. a markdown linter or a generated index), document the actual commands here at that point.

## Structure

- **`README.md`** — human-facing index. Lists the areas and explains how to add an entry. Keep its area table in sync when areas are added or removed.
- **`CLAUDE.md`** (this file) — authoring conventions for agents.
- **`TEMPLATE.md`** — the canonical entry skeleton. Copy it to start a new entry.
- **One directory per area**, each with a `README.md` defining its scope (in-scope / out-of-scope). Current areas: `harness-design/`, `prompting/`, `evals/`, `orchestration/`, `models/`, `tooling/`, `patterns/`.
- **Entries** are individual Markdown files inside an area, named `kebab-case-of-the-takeaway.md`.

Organization is **topic-first**: an entry is filed by the subject it concerns, not by its form. Whether something is a deep pattern or a quick hack is captured in frontmatter (`type:`), not by directory.

## Entry format

Every entry opens with YAML frontmatter (see `TEMPLATE.md` for the skeleton):

```yaml
---
title: Short, specific title — the takeaway as a phrase
type: pattern          # pattern | tip | hack | reference | playbook | gotcha
confidence: anecdotal  # proven | anecdotal | hypothesis
date: 2026-06-18       # absolute ISO date written — never relative
updated:               # absolute ISO date of last substantive revision (optional)
model:                 # e.g. claude-opus-4-8 — only if model-specific
version:               # SDK/tool/harness version, if behavior is version-sensitive
tags: []               # e.g. [evals, cost]
source:                # doc URL, experiment, or observed behavior the claim rests on
---
```

The body follows the template's sections: **Takeaway → When it applies → Why → Example → Notes.**

## Authoring conventions

- **One concept per file.** Many small focused entries beat a few sprawling ones. A reader should grasp exactly one idea per file.
- **Lead with the takeaway.** State the practice first, justify it second. The reader should know what to do before they know why.
- **Show, don't just tell.** Include concrete, runnable artifacts — prompts, configs, snippets, command lines — over abstract description.
- **Cite the source.** Name where a claim comes from (a doc, a model's observed behavior, an experiment, a tool version). Agentic tooling moves fast; unattributed claims age badly.
- **Use absolute dates.** Convert "last week" to an ISO date. Set `date:` on creation; bump `updated:` on substantive edits.
- **Mark version sensitivity.** Anything tied to a specific model, SDK, or Claude Code release sets `model:`/`version:` so a future reader knows whether it still holds.
- **Be honest about confidence.** `proven` = repeatedly validated; `anecdotal` = worked in a real case or two; `hypothesis` = untested idea. Label it accurately — the base earns trust by labeling uncertainty.
- **Link related notes** inline with `[[note-slug]]` wiki-links, where the slug is the target filename without `.md` (e.g. `[[external-grader-loop]]`). Slugs are location-independent — link by slug regardless of folder. A `[[slug]]` that doesn't resolve yet is fine: it marks a note worth writing. Use relative-path Markdown links only for navigation between READMEs.
- **Index notes in their area README.** When you add a note, add a bullet linking it under the `## Notes` heading of that folder's `README.md`.

## Working in this repo

- Before adding an entry, check whether an existing one covers the topic — extend it rather than creating a near-duplicate.
- Treat outdated or disproven entries as bugs: correct or remove them; don't let stale advice sit next to current advice.
- To add a new area: create the directory with a scope `README.md`, then add a row to the area table in the top-level `README.md`.
- Vendor-neutral techniques go in their concept area; put something in `tooling/` only when it's genuinely tied to a specific tool.
- Within `tooling/`, **harness-specific material lives under its harness** (e.g. all Claude-Code-specific hooks, skills, subagents, commands, and settings go in `tooling/harnesses/claude-code/`). The category folders `tooling/{hooks,skills,clis,mcps}/` are reserved for *genuinely universal / cross-harness* material. When unsure, treat it as harness-specific.
