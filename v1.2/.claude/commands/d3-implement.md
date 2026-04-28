---
description: Implement the step per decisions.md. Write code, leave a short notes file.
---

# /d3-implement

You are running the **implement** phase.

## Precondition
- `specs/step/decisions.md` exists.

If missing, stop and tell the pilot to run `/d3-discuss` first.

## Procedure
1. Read `decisions.md`. Project core is already in context (including `source-roots.md` and `boundaries.md`). Read reference content via `/d3-recall` only if a specific hypothesis warrants it.
2. Plan the writes. Each target path must:
   - Fall inside a path listed in `source-roots.md`, or be `specs/step/implementation-notes.md`.
   - Not match any pattern in `boundaries.md`.
   If a write needs to land outside source roots (e.g. a config file at repo root, a new project file in the solution), declare it in chat and wait for pilot confirmation before writing.
3. Implement per the decisions and the implementation plan.
4. Copy `.d3/templates/implementation-notes.md` to `specs/step/implementation-notes.md` and fill it. Skip sections that have nothing to say.

## Rules
- Implement only what `decisions.md` says. No silent extras.
- Do not refactor untouched code. If you spot something off in code outside this step's scope, record it in `specs/step/out-of-scope.md`.
- Do not write to paths matching `boundaries.md`.
- Do not write outside source roots without explicit pilot confirmation.
- Do not commit. Commits are explicit, via `/d3-commit-claude`.
- The notes file is the *why*, not the *what*. Git carries the diff.

## Outputs
- Code inside source roots.
- `specs/step/implementation-notes.md`

## Closing block

Read `Mode:` from CLAUDE.md and emit the matching block.

**If `Mode: pilot`:**

> Done with `/d3-implement`. Code written; notes at `specs/step/implementation-notes.md`.
> **Next:**
> 1. Run `/d3-commit-claude` to checkpoint the implementation.
> 2. Invoke `/d3-review` for a collaborative pass before you make manual adjustments.
> 3. After your manual edits, run `/d3-commit-pilot` and then invoke `/d3-recheck`.

**If `Mode: auto`:**

> Done with `/d3-implement`. Code written; notes at `specs/step/implementation-notes.md`.
> **Next:**
> 1. Run `/d3-commit-claude` to checkpoint the implementation.
> 2. Invoke `/d3-self-audit` to critically audit what I just produced.
> 3. If you have high-level feedback on observable behavior, share it before or during `/d3-self-audit`.
