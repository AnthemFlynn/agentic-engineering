---
title: Force vertical slices so every step is independently runnable
type: pattern
confidence: proven
date: 2026-06-18
model:
version:
tags: [claude-code, prompting, workflow]
source: claude-code-pro-playbook.md (Pattern 6)
---

## Takeaway

Claude defaults to horizontal phases (all DB, then all API, then all UI) — you see nothing working until the end. Instead, instruct it to build **vertical slices**: each slice crosses every layer, is independently demoable, and ends at a review checkpoint.

## When it applies

Multi-layer features (DB → service → API → UI). The bigger the feature, the more a horizontal plan delays the first working, reviewable output.

## Why

A vertical slice produces runnable, testable behavior early, so you catch wrong direction after slice 1 instead of after the whole build. The forced checkpoint ("stop and let me review before slice 2") keeps each increment small enough to redirect cheaply.

## Example

```
Implement user notifications as vertical slices.

Slice 1: "User sees unread notification count in the header"
- DB: notifications table (id, user_id, type, read_at, created_at)
- Service: getUnreadCount(userId)
- API: GET /api/notifications/count
- Frontend: NotificationBadge using the endpoint
- Test: integration test for the full slice
After Slice 1 passes, STOP for review before Slice 2.
```

## Notes

- Pairs with [[plan-command-as-spec]] (spec the slices first) and a [[test-gate-on-stop]] hook (each slice must pass before proceeding).
