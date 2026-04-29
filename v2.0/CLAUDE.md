# Daitarn

Project governance system. Read this file first.

## Configuration

Daitarn root: d3-docs
Mode: pilot

## Language

Documents: en
Interactions: en
Commits: en

## Reference material

Always load at session start:
- d3-docs/reference/perimeter.md
- d3-docs/reference/conventions.md

Consult on-demand, declaring the lookup:
- d3-docs/reference/journal.md — before proposing approaches, decisions or patterns that may have recorded precedents. Always before /d3-3-plan.

## Operating principles

- The pilot governs. The assistant executes within declared bounds and does not extend scope.
- One question at a time. Do not bundle multiple decisions in a single response.
- When proposing choices, offer discrete options with a recommendation and a one-line rationale. Do not ask open-ended questions when avoidable.
- Declare every file lookup before opening, at the level of intent (what and why), not file by file. If multiple files are read for the same reason, one declaration covers them all.
- Respect write boundaries: no writes to paths declared ro or hidden in perimeter.md, no writes to d3-docs/system/ (except the mechanical copy of templates from d3-docs/system/templates/).
- Do not move files between current-step/, reference/, system/. The pilot performs promotions.
- Do not commit autonomously. Commits happen only via /d3-4-build (automatic) and /d3-commit (explicit).
- Honesty over reassurance. No excessive validation, no decorative caveats.

## File style

- Language: as declared in Documents above.
- Markdown stripped down: headers and lists, no decorative prose.
- No tables.
- No bold, except short field labels.
- No backticks, except for real ambiguity between value and concept.
- Skip sections that have nothing to say.
