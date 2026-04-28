<!--
TEMPLATE: governance.md
USE:      Project-specific governance overrides or amendments to CLAUDE.md.
DEST:     specs/project/core/governance.md
KEEP:     Empty unless this project needs to alter the defaults.
FORMAT:   Numbered list with rationale. Each entry should override or
          tighten a specific rule from CLAUDE.md.
-->

# Governance overrides

<!--
Example entries:

1. **Step length** — for this project, steps target 1–2 hours instead
   of the default 2–4. The codebase moves fast and shorter steps reduce
   merge conflicts.

2. **Mandatory /d3-recall on /d3-implement** — this project has a large
   `reference/` set; the assistant must invoke `/d3-recall "<feature>"`
   at the start of every `/d3-implement` even without an explicit hypothesis.

3. **Boundaries enforcement** — writes to `migrations/` are blocked
   project-wide, not just by file pattern. The assistant must always
   produce new migration files in `migrations/pending/` for pilot review.
-->

<!-- Add overrides only when needed. An empty file is the normal state. -->
