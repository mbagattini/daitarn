---
description: One-time onboarding pass — populate avoid.md with project anti-patterns and rejected approaches.
---

# /d3-onboard-avoid

You are running the **avoid** pass of onboarding. This is the most pilot-dependent pass: anti-patterns and rejected approaches are largely invisible in the code itself.

## Precondition
- Read `specs/project/core/source-roots.md`. At least one listed root must exist and contain code.

## Soft guard
If `specs/project/reference/avoid.md` already has entries, warn before overwriting.

## What to look for, what to ask
The pass has two parts: what you can infer, and what you must elicit.

### Inferable (low yield, but try)
Look for in-code signals:
- Comments saying "DO NOT", "FIXME — don't use this approach", "deprecated — see X instead".
- Wrapper modules whose presence implies the wrapped thing is forbidden direct usage.
- ADRs or `docs/decisions/` if they exist.

### Elicited from the pilot (the main source)
Ask the pilot a focused set of questions in chat. Examples — adapt to what the codebase suggests:
- "I see you use library X for Y. Were other libraries considered? Why was X chosen?"
- "Are there approaches the team has tried and rolled back?"
- "Any patterns you've seen in proposed contributions that should be rejected?"
- "Any tempting refactor that should NOT be done, and why?"
- "Anything an outside contributor would propose that you'd push back on?"

Ask 3–5 questions, not 20. Quality of conversation matters more than coverage.

## Procedure
1. Do the inferable scan. Note findings.
2. Ask the pilot the elicited questions in chat. Wait for answers.
3. Copy `.d3/templates/avoid.md` to `specs/project/reference/avoid.md` (the file already exists with placeholder; treat as overwrite under the soft guard).
4. Populate it with entries from both sources, using the format already defined in the existing `avoid.md` template (slug, decided in, avoid, reason, alternative).
5. If the pilot has nothing to share and the code yielded no signals, the file stays empty. That's a valid outcome.

## Rules
- Each entry must be concrete. "Avoid bad patterns" is not an entry. "Avoid raw SQL in repositories — use the repository abstraction in `Infrastructure/Persistence`" is.
- Each entry needs a *reason*. Without rationale, the entry is fragile.
- Each entry should suggest an *alternative*, when one exists.

## Output
- `specs/project/reference/avoid.md`

## Closing block
> Done with `/d3-onboard-avoid`. Output: `specs/project/reference/avoid.md`.
> **Next:**
> 1. Open the file in your editor. Add anything that didn't come up in our conversation but should be there.
> 2. Quick chat fixes: tell me directly if any entry needs reworking.
> 3. Run `/d3-commit-pilot` when satisfied.
> 4. Suggested next pass (final): `/d3-onboard-finalize`.
