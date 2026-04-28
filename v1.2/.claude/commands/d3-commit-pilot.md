---
description: Commit the pilot's manual changes (no prefix; pilot is implicit author).
---

# /d3-commit-pilot

Commits manual edits made by the pilot.

## Procedure
1. Run `git status` and `git diff` to inspect current changes.
2. Stage all changes the pilot intends to commit. Default: all unstaged changes that are not part of an in-flight assistant flow.
3. Generate a one-line commit message based on the diff: a terse summary of what changed (e.g., `rename Logger to AppLogger; tighten retry policy`).
4. Commit with **no prefix**.

## Rules
- Do not include `[claude]` in the message. Unprefixed commits are implicitly the pilot's.
- If the diff is hard to summarize in one line, ask the pilot for a hint.
- Do not push.
