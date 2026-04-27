---
description: After the pilot's manual edits, identify diffs and capture rationale.
---

# /d3-recheck

You are running the **recheck** phase. This skill exists for **pilot mode** only.

## Mode check
Read CLAUDE.md. If `Mode: auto`, refuse:

> `/d3-recheck` runs only in pilot mode. In auto mode, use `/d3-self-audit`.

## Preconditions
- `specs/step/implementation-notes.md` exists.
- At least one commit (typically the pilot's, unprefixed) exists after the most recent `[claude] /d3-implement` commit.

If preconditions fail, explain and stop.

## Procedure
1. From git, compute the diff between the last `[claude]` commit of this step and current HEAD. Restrict to files relevant to this step.
2. Summarize the diff in plain terms — what changed, in which files, with what effect.
3. For each non-trivial change, ask the pilot: *"why this change?"* — concretely and concisely. Trivial changes (whitespace, simple renames) do not need rationale questions.
4. Capture the pilot's answers as you receive them.
5. Copy `.d3/templates/recheck-learnings.md` to `specs/step/recheck-learnings.md` and fill it.

## Rules
- Do not assume rationale. Ask. The point of this phase is to extract knowledge that only the pilot has.
- Lessons should be generalizable beyond this step.
- Do not modify code.

## Output
- `specs/step/recheck-learnings.md`

## Closing block
> Done with `/d3-recheck`. Output: `specs/step/recheck-learnings.md`.
> **Next:**
> 1. Run `/d3-commit-claude` to checkpoint the learnings.
> 2. If this step is complete, invoke `/d3-close`.
> 3. If more work remains, decide the next phase (typically another `/d3-implement` increment).
