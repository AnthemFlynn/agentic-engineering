# Hooks

Lifecycle hooks that intercept and react to the agent loop.

**In scope:** hook types (PreToolUse, PostToolUse, Stop, and friends), what to wire them to (format, lint, type-check, guards, notifications), ordering, and failure handling.

**Out of scope:** harness-specific hook configuration syntax, which goes under the relevant harness (e.g. [../harnesses/claude-code/](../harnesses/claude-code/)).

## Notes

- [Auto-format on write (PostToolUse)](auto-format-on-write.md)
- [Block destructive bash (PreToolUse, exit 2)](block-destructive-bash.md)
- [Protect sensitive files (PreToolUse path guard)](protect-sensitive-files.md)
- [Test-gate on stop (Stop hook + loop guard)](test-gate-on-stop.md)
- [Session-start context injection](session-start-context-injection.md)
- [PreToolUse input modification](pretooluse-input-modification.md)
- [Prompt-injection sanitizing hook](prompt-injection-sanitizing-hook.md)
- [Debugging hooks when they don't fire](debugging-hooks.md)
