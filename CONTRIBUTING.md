# Contributing

Thanks for wanting to add to this knowledge base. It's a collection of **atomic, source-cited notes** on building and operating AI agents. The bar is simple: every note should be something a reader (human or agent) can act on, trust, and trace back to a source.

This guide covers the contribution workflow. For the conventions in full, see [CLAUDE.md](CLAUDE.md); for the note skeleton, see [TEMPLATE.md](TEMPLATE.md).

## What makes a good note

- **One concept per file.** If you're tempted to use "and" in the title, it's probably two notes.
- **Lead with the takeaway.** State the practice first, justify it second. A reader should know *what to do* before they know *why*.
- **Show, don't just tell.** Include a concrete, runnable artifact — a prompt, config, snippet, or command — over abstract description.
- **Cite the source.** Fill in `source:` with where the claim comes from (a doc, observed behavior, an experiment, a tool version). Unattributed claims age badly.
- **Be honest about confidence.** `proven` = repeatedly validated · `anecdotal` = worked in a real case or two · `hypothesis` = untested idea.
- **Mark version sensitivity.** Anything tied to a specific model, SDK, or release sets `model:`/`version:` so future readers know whether it still holds.
- **Use absolute dates.** Convert "last week" to an ISO date.

## Where a note goes

Organization is **topic-first** — file by subject, not by form (a tip, pattern, and reference on the same topic live together; their `type:` distinguishes them).

| If it's… | It goes in… |
|----------|-------------|
| A vendor-neutral concept (prompting, evals, orchestration, model economics, harness design) | the matching top-level area |
| A cross-cutting technique with no single home | [`patterns/`](patterns/) |
| Specific to one harness (Claude Code hooks, settings, SDK, etc.) | under that harness, e.g. [`tooling/harnesses/claude-code/`](tooling/harnesses/claude-code/) |
| An external tool | by its **primitive** — a harness → `tooling/harnesses/`, a plugin → `tooling/plugins/`, a skill → `tooling/skills/`, an MCP server → `tooling/mcps/`, a CLI → `tooling/clis/` |

When unsure whether something is harness-specific or universal, treat it as harness-specific. Don't lump distinct tool types into one "misc" bucket.

## Adding a note

1. **Branch** off `main`.
2. **Copy [`TEMPLATE.md`](TEMPLATE.md)** into the right area and fill in the frontmatter + body sections (Takeaway → When it applies → Why → Example → Notes).
3. **Name the file** `kebab-case-of-the-takeaway.md`.
4. **Link related notes** inline with `[[note-slug]]` wiki-links (slug = target filename without `.md`). Link liberally — a `[[slug]]` that doesn't resolve yet is a fine marker for a note worth writing.
5. **Index it** — add a bullet under the `## Notes` heading of the area's `README.md`.
6. **Check for duplicates first** — if a note already covers the topic, *extend it* (and add your source to its `source:`) rather than creating a near-duplicate. Treat stale or disproven notes as bugs: fix or remove them.
7. **Validate links** (below), commit, and open a PR.

### Frontmatter reference

```yaml
---
title: Short, specific title — the takeaway as a phrase
type: pattern          # pattern | tip | hack | reference | playbook | gotcha
confidence: anecdotal  # proven | anecdotal | hypothesis
date: 2026-06-18       # ISO date written — absolute, never relative
updated:               # ISO date of last substantive revision (optional)
model:                 # e.g. claude-opus-4-8 — only if model-specific
version:               # SDK / tool / harness version, if behavior is version-sensitive
tags: []               # e.g. [evals, cost]
source:                # doc URL, experiment, or observed behavior the claim rests on
---
```

## Validating links

Wiki-links are slug-based (location-independent), so moving files never breaks them — but typos do. Before opening a PR, from the repo root:

```bash
# Every [[wiki-link]] should resolve to an existing note slug
find . -name '*.md' -not -name 'README.md' -not -name 'CLAUDE.md' -not -name 'TEMPLATE.md' \
  -exec basename {} .md \; | sort -u > /tmp/slugs.txt
grep -rhoE '\[\[[a-z0-9-]+\]\]' . | sed 's/\[\[//; s/\]\]//' | sort -u > /tmp/links.txt
comm -23 /tmp/links.txt /tmp/slugs.txt    # prints only unresolved (dangling) links
```

Intentional dangling links (markers for notes not yet written) are fine; just make sure new ones are deliberate. Use plain `[[slug]]` form — not the `[[slug|alias]]` pipe syntax.

## Commits & PRs

- Conventional-commit style: `docs: …`, `feat: …`, `refactor: …`, `fix: …`.
- One coherent change per PR. Describe what you added/changed and why.

## License

By contributing, you agree your contributions are licensed under [CC BY 4.0](LICENSE), the same as the rest of the repository. Material you distill from other sources remains under its own terms — keep the `source:` credit intact.
