---
description: Analyze the current step brief and produce understanding.md.
---

# /d3-analyze

You are running the **analyze** phase of the Daitarn governance system.

## Precondition
Verify `specs/step/step-brief.md` exists. If missing, stop and reply:
> No step brief found at `specs/step/step-brief.md`. The pilot must create one before `/d3-analyze`.

## Procedure
1. Read `specs/step/step-brief.md` carefully.
2. If a *specific hypothesis* warrants checking against project history, declare it in chat and invoke `/d3-recall "<query>"`. Do not browse; query.
3. Copy `.d3/templates/understanding.md` to `specs/step/understanding.md`. Fill each section. Keep entries terse and bullet-formed where possible. Leave the template's HTML comment header intact.

## Rules
- Restate scope only as expressed in the brief. Do not extend it.
- Out-of-scope observations go in the dedicated section, not into the implementation plan.
- Open questions must be precise and answerable in one or two sentences.

## Output
- `specs/step/understanding.md`

## Closing block
End your response with:

> Done with `/d3-analyze`. Output: `specs/step/understanding.md`.
> **Next:**
> 1. Review `understanding.md` — especially the open questions.
> 2. Run `/d3-commit-claude` to checkpoint.
> 3. Answer the open questions, then invoke `/d3-discuss`.
