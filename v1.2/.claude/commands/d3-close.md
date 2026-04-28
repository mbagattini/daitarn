---
description: Distill the step and propose what to promote, archive, or drop.
---

# /d3-close

You are running the **close** phase.

## Preconditions
- `specs/step/decisions.md` exists.
- `specs/step/implementation-notes.md` exists.
- *Mode: pilot* → typically `specs/step/recheck-learnings.md` also exists.
- *Mode: auto* → `specs/step/self-audit.md` exists.

If decisions or implementation notes are missing, stop and explain. If the mode-specific file is missing, point to the command that produces itb (`/d3-recheck` or `/d3-self-audit`).

## Procedure
1. Read every file under `specs/step/`.
2. Copy `.d3/templates/closure-proposal.md` to `specs/step/closure-proposal.md` and fill it:
   - Distillation in four sections: decided / built / open / learned.
   - Promotion plan as a table — for each item that emerged in this step, propose a destination: `specs/project/core/<file>.md`, `specs/project/reference/<file>.md`, `.d3/backlog.md`, or `drop`.
3. Be conservative. Only promote what is genuinely durable. When in doubt, propose `reference` over `core`, and `backlog` over `reference`.

## Rules
- You **propose**, the pilot **executes**. Do not move files. Do not write into `specs/project/core/`, `specs/project/reference/`, or anything under `.d3/`.
- For each row in the promotion plan, the rationale must be one short sentence.

## Output
- `specs/step/closure-proposal.md`

## Closing block
> Done with `/d3-close`. Proposal: `specs/step/closure-proposal.md`.
> **Next:**
> 1. Review the promotion plan.
> 2. Apply the moves manually:
>    - Promote items into `specs/project/core/` or `specs/project/reference/`.
>    - Add backlog items to `.d3/backlog.md`.
>    - Archive `specs/step/` contents into `.d3/past/step-<N>/`.
>    - Empty `specs/step/`.
> 3. Run `/d3-commit-pilot` to commit the closure moves.
> 4. When ready, drop the next `step-brief.md` into `specs/step/` and invoke `/d3-analyze`.
