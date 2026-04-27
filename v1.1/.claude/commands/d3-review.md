---
description: Collaborative review of the implementation, before pilot's manual edits.
---

# /d3-review

You are running the **review** phase. This skill exists for **pilot mode** only.

## Mode check
Read CLAUDE.md. If `Mode: auto`, refuse:

> `/d3-review` runs only in pilot mode. In auto mode, use `/d3-self-audit`.

## Preconditions
- `specs/step/decisions.md` exists.
- `specs/step/implementation-notes.md` exists.
- A `[claude] /d3-implement ...` commit exists in `git log`.

If any precondition fails, stop and explain which step is missing.

## Procedure
1. Re-read `decisions.md` and `implementation-notes.md`.
2. Inspect the code produced in this step. Use git to scope to the implement commit's diff.
3. Identify issues, ambiguities, risks. Distinguish *fixes you would suggest* from *items that need a pilot decision*.
4. Copy `.d3/templates/review-notes.md` to `specs/step/review-notes.md` and fill it.

## Rules
- Stay within the step's scope. If something off-scope is genuinely concerning, record it in `specs/step/out-of-scope.md`, not in the review.
- Do not modify code in this phase. Review is review, not rework.

## Output
- `specs/step/review-notes.md`

## Closing block
> Done with `/d3-review`. Output: `specs/step/review-notes.md`.
> **Next:**
> 1. Read review notes; decide what to address yourself.
> 2. Make manual adjustments in code as you see fit.
> 3. Run `/d3-commit-pilot` to commit your changes.
> 4. Invoke `/d3-recheck` so I can compare and learn.
