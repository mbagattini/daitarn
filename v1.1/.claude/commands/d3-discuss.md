---
description: Resolve open questions and produce binding decisions for the step.
---

# /d3-discuss

You are running the **discuss** phase.

## Preconditions
- `specs/step/step-brief.md` exists.
- `specs/step/understanding.md` exists.

If either is missing, stop and tell the pilot which file is needed and which skill produces it.

## Procedure
1. Read `step-brief.md` and `understanding.md`.
2. Engage with the pilot to address open questions and finalize approach. The conversation may happen in any language; the documents you produce are in English.
3. You may propose alternatives **only inside the declared scope** (e.g., a different library that achieves the same goal). Anything that broadens scope goes to `out-of-scope.md`, not into the discussion.
4. You may invoke `/d3-recall "<query>"` if a hypothesis warrants checking. Declare query and reason first.
5. When the pilot signals readiness, copy `.d3/templates/decisions.md` to `specs/step/decisions.md` and fill it. If anything surfaced as out-of-scope, copy `.d3/templates/out-of-scope.md` to `specs/step/out-of-scope.md` and record it.

## Rules
- Decisions must be directly executable, not topics for further debate.
- Each decision: what + brief why. No essays.
- Do not write decisions that imply work outside the resolved scope.

## Outputs
- `specs/step/decisions.md` (always)
- `specs/step/out-of-scope.md` (if anything was parked)

## Closing block
> Done with `/d3-discuss`. Outputs: `decisions.md` [, `out-of-scope.md`].
> **Next:**
> 1. Review `decisions.md`.
> 2. Run `/d3-commit-claude` to checkpoint.
> 3. When ready, invoke `/d3-implement`.
