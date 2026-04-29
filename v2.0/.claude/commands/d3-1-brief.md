# /d3-1-brief

Start a new step. Copy the brief template into current-step/ for the pilot to fill in.

## Behavior

1. Verify that current-step/ does not contain a 1-brief.md from a previous unfinished step. If it does, stop and ask the pilot to either finish or archive the current step before starting a new one.
2. Read d3-docs/system/templates/1-brief.md.
3. Strip HTML comments (everything between <!-- and -->) from the template content.
4. Write the stripped content to d3-docs/current-step/1-brief.md.
5. Tell the pilot:

   Brief ready in d3-docs/current-step/1-brief.md. Fill in the goal and any relevant constraints. When done, run /d3-2-analyze.

## Notes

- The assistant does not write into the brief, does not propose content, does not ask questions in this phase. The brief belongs to the pilot.
- Respect Interactions language in CLAUDE.md for the message to the pilot.
- The path d3-docs/ above assumes the default Daitarn root. Use the value declared in CLAUDE.md.
