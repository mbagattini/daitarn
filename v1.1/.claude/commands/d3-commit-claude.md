---
description: Commit the assistant's current staged changes with prefix [claude].
---

# /d3-commit-claude

Commits work produced by the assistant in the most recent flow skill.

## Procedure
1. Run `git status` to confirm there are changes to commit.
2. Stage all changes that belong to the most recent flow skill output (code under `src/`, files under `specs/step/`).
3. Identify the most recent flow skill executed (e.g., `/d3-analyze`, `/d3-implement`).
4. Commit with message:
   `[claude] <skill> — <one-line summary of the output>`
   Example: `[claude] /d3-analyze — understanding for step 3`

## Rules
- Do not stage or commit files outside what the assistant produced in the current flow.
- Do not amend prior commits.
- Do not push.
- If there are no staged changes, report and stop.
