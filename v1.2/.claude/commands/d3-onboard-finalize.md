---
description: One-time onboarding pass — re-read all four onboarding outputs and report inconsistencies. Writes nothing.
---

# /d3-onboard-finalize

You are running the **finalize** pass of onboarding. Your job is to act as a second pair of eyes after the pilot has done their editor pass. The pilot can drift just as the assistant can; this pass is double-check, not rewrite.

## Precondition
At least one of the following must be non-empty (i.e. populated beyond the placeholder):
- `specs/project/core/map.md`
- `specs/project/core/boundaries.md`
- `specs/project/core/conventions.md`
- `specs/project/reference/avoid.md`

If all four are placeholders, refuse:

> Nothing to finalize — the four onboarding files are still placeholders. Run the onboarding passes first.

## Procedure
1. Read all four files.
2. Look for inconsistencies across them. Categories to consider:
   - **Map vs. boundaries** — does `map.md` reference modules as actively maintained, while `boundaries.md` marks them read-only? Either may be wrong.
   - **Map vs. conventions** — does `conventions.md` cite a folder structure that doesn't match `map.md`?
   - **Conventions vs. avoid** — does `avoid.md` warn against a pattern that `conventions.md` actually documents as the standard?
   - **Internal contradictions** — within a single file, do entries contradict each other?
   - **Empty echoes** — does any file reference a concept that another file should describe but doesn't?
3. Report findings in chat as a numbered list. For each:
   - Which files are involved.
   - What the inconsistency is.
   - A proposed resolution (which side is likely correct, or that the pilot must decide).
4. If you find nothing, say so plainly: "No inconsistencies found. The four files are coherent."

## Rules
- **Write nothing.** This is a check, not a fix.
- Suggested resolutions are suggestions. The pilot decides and applies them in editor.
- A finalize that finds nothing is a valid outcome — but if the four files are large and you found nothing, look again.

## Output
- A chat report. No file changes.

## Closing block
> Done with `/d3-onboard-finalize`.
> **Next:**
> 1. Review the inconsistencies (if any). Apply fixes in your editor.
> 2. Run `/d3-commit-pilot` to commit any final adjustments.
> 3. Onboarding is complete. From here, the system works exactly like a greenfield project. Drop a `step-brief.md` in `specs/step/` and invoke `/d3-analyze` for the first step.
