# /d3-4-build

Execute the plan, log progress, commit at the end.

## Behavior

1. Read d3-docs/current-step/3-plan.md. If missing, stop and instruct the pilot.
2. Copy d3-docs/system/templates/4-build.md, strip HTML comments, write to d3-docs/current-step/4-build.md.
3. Execute the plan steps in order. For each step:
   - Before writing inside any path, verify d3-docs/reference/perimeter.md. Refuse paths declared ro or hidden.
   - Before writing outside source roots and outside d3-docs/current-step/, ask the pilot for explicit confirmation.
   - Append a one-line entry to d3-docs/current-step/4-build.md describing what was done. Record deviations from the plan with a short reason.
4. After the last step, commit all changes with the same logic as /d3-commit (commit message in the language declared in Commits in CLAUDE.md, prefixed [claude]).
5. Tell the pilot:

   Build complete and committed. See d3-docs/current-step/4-build.md. When verified, run /d3-5-close.

## Notes

- The assistant owns 4-build.md and the code written during this phase.
- In pilot mode the pilot may intervene in chat to request corrections; the assistant updates code and the build log.
- In auto mode the pilot does not touch code; review happens at /d3-5-close.
- Respect Documents, Interactions and Commits languages in CLAUDE.md.
- Use the Daitarn root declared in CLAUDE.md.
