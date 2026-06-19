---
title: Prompt caching — static content first, dynamic content last
type: pattern
confidence: proven
date: 2026-06-18
model:
version:
tags: [claude-code, caching, cost, runtime]
source: claude-code-mastery-v3_2.html (Level 4, P3)
---

## Takeaway

Prompt caching reuses the computed KV attention tensors for a repeated prompt prefix, cutting 40–90% of token cost on agents that resend the same system prompt across many calls. The invariant: **static content first, dynamic content last.** Any dynamic value in the system prompt breaks the cache on every call.

## When it applies

Agents that make dozens of API calls with a stable system prompt (role, architecture context, tool descriptions, few-shot examples). Minimum cache threshold is ~1,024 tokens — usually easy to exceed given that context.

## Why

Caching keys on the unchanging prefix. Put task IDs, timestamps, or user names in the system prompt and the prefix changes every call → cache miss every call. Keep the system prompt and tool definitions invariant; put the current task at the end of the user message.

## Example

```ts
const STATIC_SYSTEM = `You are a security auditor for [Company].
[Role / architecture / tool descriptions / few-shot — never change]`;  // ✅ cached after first call
query({ prompt: `Audit this file: ${filePath}\n${fileContent}`,        // ✅ dynamic in user message
        options: new ClaudeAgentOptions({ systemPrompt: STATIC_SYSTEM }) });
// ❌ BAD_SYSTEM with `task: ${taskId}` / `at: ${new Date()}` → miss every call
```

## Notes

- A core cost lever for [[agent-sdk-budgeted-run]]; complements model routing in [[model-mixing-per-agent-role]]. Cross-harness Claude API feature — also relevant to anything in `models/`. Below [[the-line]].
