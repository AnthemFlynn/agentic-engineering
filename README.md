# Agentic Engineering

A curated knowledge base of patterns, tips, tricks, hacks, and hard-won lessons for building and operating AI agents.

Each entry is a single focused Markdown file with [structured frontmatter](TEMPLATE.md), filed under the topic it belongs to.

## Areas

| Area | What lives here |
|------|-----------------|
| [harness-design/](harness-design/) | Action spaces, tool/function definitions, observation & result formatting, error surfaces — how an agent perceives and acts. |
| [prompting/](prompting/) | Prompt & context engineering: system prompts, context-window management, compaction, instruction design. |
| [evals/](evals/) | Eval-driven development, rubrics, graders, LLM-as-judge, regression testing, datasets. |
| [orchestration/](orchestration/) | Multi-agent topologies, autonomous loops, fan-out/pipeline, DAGs, handoffs, worktrees. |
| [models/](models/) | Model selection, routing by task complexity, cost control, prompt caching, token budgeting. |
| [tooling/](tooling/) | Claude Code (skills, subagents, hooks, MCP, slash commands) and other agent harnesses/CLIs. |
| [patterns/](patterns/) | Cross-cutting reusable patterns that don't belong to a single topic above. |

## Adding an entry

1. Pick the area it belongs to (or propose a new one — add the directory and a `README.md` describing its scope).
2. Copy [`TEMPLATE.md`](TEMPLATE.md), fill in the frontmatter, write the entry.
3. Name the file `kebab-case-of-the-takeaway.md`.
4. Link related entries inline.

See [CLAUDE.md](CLAUDE.md) for the authoring conventions in full.
