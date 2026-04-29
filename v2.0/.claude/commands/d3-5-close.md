# /d3-5-close

Verify the step, write closure, propose carry-forward and promotions.

## Behavior

1. Read d3-docs/current-step/1-brief.md, 3-plan.md, 4-build.md. If any are missing, stop and instruct the pilot.
2. Read d3-docs/reference/perimeter.md and d3-docs/reference/conventions.md (if not already loaded). Consult d3-docs/reference/journal.md if relevant, declaring the lookup.
3. Branch by Mode (declared in CLAUDE.md):

   Auto mode:
   - Re-read the code written during /d3-4-build.
   - Self-audit: check coherence with 3-plan.md, with conventions.md, with journal precedents.
   - Record findings as "things to watch" in the closure file.

   Pilot mode:
   - Diff the working tree against the build commit (the commit produced by /d3-4-build).
   - Summarize the pilot's interventions (additions, removals, edits) with reasons where not obvious from the diff. Ask in chat where context is missing.

4. Copy d3-docs/system/templates/5-closure.md, strip HTML comments, write to d3-docs/current-step/5-closure.md, and fill in the sections including:
   - Summary
   - Deviations from plan (final)
   - Self-audit findings or pilot interventions, depending on mode
   - Carry-forward items for the next step
   - Promotion proposals: for each, target file in reference/ (perimeter, conventions, journal) and proposed text

5. Tell the pilot:

   Closure ready in d3-docs/current-step/5-closure.md. You move the current-step files to d3-docs/system/past/ and apply the promotions you approve. To start a new step, run /d3-1-brief.

## Notes

- The assistant owns 5-closure.md.
- The assistant does not move files between current-step/, reference/, system/. The pilot performs the moves manually.
- The assistant does not commit at the end of /d3-5-close. Closure is documentation; if the pilot wants the closure file committed, they run /d3-commit or commit manually.
- Respect Documents and Interactions languages in CLAUDE.md.
- Use the Daitarn root declared in CLAUDE.md.
