---
description: Search specs/project/reference/ for content relevant to a query. Returns excerpts.
---

# /d3-recall

You are running a **lookup** against `specs/project/reference/`.

## When to use
- During any flow command, when a *specific hypothesis* warrants checking project history (a prior decision, a past avoidance, a known pattern, a recheck lesson).
- Never as exploration. Always with a query.

## Pre-invocation declaration
Before invoking, declare in chat:

> Checking `reference/` for: "<query>". Reason: <one short sentence>.

If you cannot state both a query and a reason, do not invoke.

## Procedure
1. Read the four reference files: `specs/project/reference/decisions.md`, `avoid.md`, `patterns.md`, `lessons.md`.
2. Extract entries relevant to the query. Return excerpts, not full files.
3. If nothing matches, say so plainly — "No relevant entries in `reference/` for this query." — and do not pad.

## Output
- A short message in chat with relevant excerpts and their source file. No file is written.

## Rules
- Do not enter `specs/project/reference/` for any reason other than this command.
- Quote entries verbatim with their source heading; do not paraphrase or summarize.
- After delivering excerpts, return to the flow command that was running.
