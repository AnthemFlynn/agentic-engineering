# Plugins

Workflow plugins — packaged bundles that ship an opinionated workflow (skills + commands + hooks + agents) as one installable unit, often across multiple harnesses.

**In scope:** what a plugin is, what it bundles, how to install it, and when to reach for it. A plugin sits above a single [skill](../skills/) — it's a coordinated *set* of primitives encoding a whole practice.

**Out of scope:** an individual skill (→ [../skills/](../skills/)); a harness itself (→ [../harnesses/](../harnesses/)); a single MCP server (→ [../mcps/](../mcps/)).

## Notes

- [Superpowers — TDD-enforced SDLC plugin](superpowers.md)
- [BMAD — spec-driven design plugin](bmad.md)

## Repos to watch

External plugins / agentic frameworks worth following:

- [obra/superpowers](https://github.com/obra/superpowers) — agentic skills framework & SDLC methodology (cross-harness).
- [affaan-m/ECC](https://github.com/affaan-m/ECC) — "Everything Claude Code": a cross-harness agent-harness optimization system (skills, instincts, memory, security) for Claude Code, Codex, OpenCode, Cursor.
