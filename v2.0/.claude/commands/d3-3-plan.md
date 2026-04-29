# /d3-3-plan

Discuss the approach in chat and write the agreed plan.

## Behavior

1. Announce phase atomicity:

   This phase converges on an approach via chat discussion and writes a plan at the end. If the session closes mid-discussion, the plan is lost; the previous artifacts (1-brief, 2-analysis) remain.

   Wait for confirmation.

2. Read d3-docs/current-step/1-brief.md and d3-docs/current-step/2-analysis.md. If either is missing, stop and instruct the pilot.
3. Consult d3-docs/reference/journal.md, declaring the lookup, to surface any precedents relevant to the decisions ahead.
4. Propose an approach in chat. Where decisions are required, frame them as A/B/C with a recommendation and a one-line rationale. One decision at a time, not bundled.
5. Iterate with the pilot until convergence.
6. When the pilot signals agreement, copy d3-docs/system/templates/3-plan.md, strip HTML comments, write to d3-docs/current-step/3-plan.md, and fill in the sections.
7. Tell the pilot:

   Plan ready in d3-docs/current-step/3-plan.md. Review it. If it stands, run /d3-4-build.

## Notes

- The assistant owns 3-plan.md. The pilot does not edit directly; for changes, reopen the discussion in chat and the assistant rewrites.
- The pilot may answer "D, none of the above" to any A/B/C and propose an alternative.
- Respect Documents and Interactions languages in CLAUDE.md.
- Use the Daitarn root declared in CLAUDE.md.
