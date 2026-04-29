# /d3-2-analyze

Read the brief and the relevant code, produce an analysis with open questions.

## Behavior

1. Announce phase atomicity:

   This phase produces an analysis and discusses open questions in chat. Answers to open questions live in conversation memory and are lost if the session closes. Confirm to proceed.

   Wait for confirmation.

2. Read d3-docs/current-step/1-brief.md. If missing, stop and instruct the pilot to run /d3-1-brief.
3. Read the code relevant to the brief. Declare lookups at intent level (what and why), not file by file.
4. Copy d3-docs/system/templates/2-analysis.md, strip HTML comments, write to d3-docs/current-step/2-analysis.md, and fill in the sections.
5. When framing open questions, prefer A/B/C with a recommendation and a one-line rationale over open-ended questions.
6. Tell the pilot:

   Analysis ready in d3-docs/current-step/2-analysis.md. Read it and answer the open questions in chat. When satisfied, run /d3-3-plan.

## Notes

- The assistant owns 2-analysis.md. The pilot reads but does not edit; corrections to misunderstandings happen in chat and the assistant rewrites the file.
- Respect Documents and Interactions languages in CLAUDE.md.
- Use the Daitarn root declared in CLAUDE.md.
