# Agentic Engineering

![Knowledge base](https://img.shields.io/badge/knowledge%20base-agentic%20engineering-6E40C9)
![Format](https://img.shields.io/badge/format-atomic%20%C2%B7%20wiki--linked-0969DA)
![Content](https://img.shields.io/badge/content-markdown-000000)
[![License: CC BY 4.0](https://img.shields.io/badge/license-CC%20BY%204.0-lightgrey)](LICENSE)

> A curated, source-cited knowledge base of patterns, tips, and hard-won lessons for **building and operating AI agents** — harness design, prompting, evals, orchestration, model economics, and the tooling around them.

Each entry is one focused **atomic note** with [structured frontmatter](TEMPLATE.md) and `[[wiki-links]]` between related ideas, filed under the topic it belongs to. Browse by area below, or follow the links between notes.

## Areas

| Area | What lives here |
|------|-----------------|
| [harness-design/](harness-design/) | Action spaces, tool/function definitions, observation & result formatting, error surfaces — how an agent perceives and acts. |
| [prompting/](prompting/) | Prompt & context engineering: system prompts, context-window management, compaction, instruction design. |
| [evals/](evals/) | Eval-driven development, rubrics, graders, LLM-as-judge, regression testing, datasets. |
| [orchestration/](orchestration/) | Multi-agent topologies, autonomous loops, fan-out/pipeline, DAGs, handoffs, worktrees. |
| [models/](models/) | Model selection, routing by task complexity, cost control, prompt caching, token budgeting. |
| [tooling/](tooling/) | Tool-specific knowledge by category — [harnesses](tooling/harnesses/) (Claude Code, OpenCode, Codex, Antigravity), [plugins](tooling/plugins/), CLIs, MCP servers, skills, and hooks. |
| [patterns/](patterns/) | Cross-cutting reusable patterns that don't belong to a single topic above. |

## How it's organized

- **Atomic notes** — one idea per file, so each is independently citable and linkable.
- **Topic-first** — filed by subject, not by form. Whether a note is a pattern, tip, or reference is captured in frontmatter, not by folder.
- **Wiki-linked** — related notes connect via `[[note-slug]]`, so you can follow a thread across areas. Each area's `README.md` indexes its notes.

## Sources & provenance

These notes are **distilled and synthesized** from public documentation and the practitioner community — e.g. Anthropic's Claude Code docs, publicly shared workflows, and community projects. Every note's `source:` frontmatter cites where its claims come from, and `confidence:` flags how well-established each claim is (`proven` / `anecdotal` / `hypothesis`).

This is an **independent, unofficial** knowledge base, not affiliated with any vendor. Agentic tooling moves fast: notes carry `version:`/`date:` fields, but **verify version-sensitive details against primary sources** before relying on them.

## Adding an entry

1. Pick the area it belongs to (or propose a new one — add the directory and a `README.md` describing its scope).
2. Copy [`TEMPLATE.md`](TEMPLATE.md), fill in the frontmatter, write the entry.
3. Name the file `kebab-case-of-the-takeaway.md`.
4. Link related notes inline with `[[note-slug]]` wiki-links, and add the note under the `## Notes` heading of its area README.

New contributors: see [CONTRIBUTING.md](CONTRIBUTING.md) for the full workflow, and [CLAUDE.md](CLAUDE.md) for the authoring conventions in detail.

## License

Licensed under [Creative Commons Attribution 4.0 International](LICENSE) (CC BY 4.0). You're free to share and adapt with attribution. Individual notes cite their upstream `source:` in frontmatter — those original works remain under their own terms; please preserve that credit when reusing.
