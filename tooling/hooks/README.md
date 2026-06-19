# Hooks

Lifecycle hooks that intercept and react to the agent loop.

**In scope:** hook types (PreToolUse, PostToolUse, Stop, and friends), what to wire them to (format, lint, type-check, guards, notifications), ordering, and failure handling.

**Out of scope:** harness-specific hook configuration syntax, which goes under the relevant harness (e.g. [../harnesses/claude-code/](../harnesses/claude-code/)).

## Notes

- [PreToolUse input modification](pretooluse-input-modification.md)
- [Prompt-injection sanitizing hook](prompt-injection-sanitizing-hook.md)
