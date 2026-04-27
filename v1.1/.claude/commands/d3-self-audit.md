---
description: Auto-mode replacement for review + recheck. Audit the implementation critically.
---

# /d3-self-audit

You are running the **self-audit** phase. This skill exists for **auto mode**, where the pilot does not edit code.

## Mode check
Read CLAUDE.md. If `Mode: pilot`, refuse:

> `/d3-self-audit` runs only in auto mode. In pilot mode, use `/d3-review` then `/d3-recheck`.

## Preconditions
- `Mode: auto` is set in CLAUDE.md.
- `specs/step/decisions.md` exists.
- `specs/step/implementation-notes.md` exists.
- A `[claude] /d3-implement ...` commit exists in `git log`.

## Mindset
You are looking for problems, not confirming work. Default to suspicion of your own implementation. If you find nothing, you probably did not look hard enough.

## Procedure
1. Re-read `decisions.md` and `implementation-notes.md`.
2. Inspect the diff of the most recent `[claude] /d3-implement` commit.
3. Audit against three explicit categories:
   - **Scope creep** — did I do anything not asked for in `decisions.md`?
   - **Gaps** — did I skip anything `decisions.md` required?
   - **Fragility** — under what conditions does this break? Edge cases, error paths, assumed inputs.
4. For each finding, decide: correct now, or note as *thing to watch*.
5. Apply corrections directly to the code. These corrections are part of this skill's output, not a separate `/d3-implement` invocation.
6. If the pilot has provided high-level feedback (e.g. "this doesn't do what I expected"), treat it as an additional finding and address it explicitly.
7. Copy `.d3/templates/self-audit.md` to `specs/step/self-audit.md` and fill it.

## Rules
- Findings must be concrete: location + nature of the issue. Not "the code could be cleaner."
- A self-audit that finds nothing is a red flag. Re-examine.
- Do not expand scope under the guise of an audit. Out-of-scope concerns go to `specs/step/out-of-scope.md`.
- If corrections are non-trivial, run them as part of this skill but record them in the self-audit output, then commit via `/d3-commit-claude`.

## Output
- Code corrections under `src/` (if any).
- `specs/step/self-audit.md`

## Closing block
> Done with `/d3-self-audit`. Output: `specs/step/self-audit.md`.
> **Next:**
> 1. Run `/d3-commit-claude` to checkpoint the audit and any corrections.
> 2. Review the *Things to watch* section. If something needs another pass, give feedback and re-invoke `/d3-implement`, then `/d3-self-audit` again.
> 3. When satisfied, invoke `/d3-close`.
