# Daitarn

Version: 2.0
Released: 2026-04-29

## Changelog

### 2.0 (2026-04-29)

Major restructure. No migration path from 1.x — v2.0 is a fresh scaffold.

Structure
- All Daitarn content lives under a single configurable root, declared in CLAUDE.md as Daitarn root.
- Folders: system/ (off-limits), reference/ (always-loaded perimeter and conventions, on-demand journal), current-step/ (working set, one step at a time).
- core/ folder removed; its content is now in reference/.
- Reference files reduced from six (source-roots, boundaries, map, conventions, glossary, governance) to two (perimeter, conventions). Map collapsed into perimeter as inline notes; glossary and governance dropped.
- Past four reference files (decisions, avoid, patterns, lessons) merged into a single journal.md, append-only, no tags.

Commands
- Flow reduced from seven phases to five, numbered in command names: /d3-1-brief, /d3-2-analyze, /d3-3-plan, /d3-4-build, /d3-5-close.
- /d3-discuss merged into /d3-2-analyze and /d3-3-plan with cleaner phase boundaries.
- /d3-review and /d3-recheck removed as named phases. In pilot mode, /d3-5-close diffs the pilot's interventions against the build commit.
- /d3-self-audit absorbed into /d3-5-close as the auto-mode behavior.
- Onboarding collapsed from five commands to one: /d3-onboard, which auto-detects greenfield vs brownfield and produces perimeter and conventions in a single guided session.
- /d3-recall removed; perimeter and conventions are always loaded, journal is consulted on-demand by the assistant before decisions.
- Two commit commands merged into /d3-commit. /d3-4-build commits automatically at phase end with the same logic.

Output files
- Each phase produces one file in current-step/, named after the phase: 1-brief.md, 2-analysis.md, 3-plan.md, 4-build.md, 5-closure.md.
- Step folder renamed from step/ to current-step/ for clarity against system/past/.

Conventions
- Language settings introduced in CLAUDE.md: Documents, Interactions, Commits, each defaulting to en (ISO 639-1).
- File style tightened: no tables, no bold (except short field labels), no backticks (except real ambiguity), bullets over prose, skip empty sections.
- HTML comments are author-time only and stripped on copy from system/templates/ to current-step/. Blockquotes carry production-time notes.
- /d3-2-analyze, /d3-3-plan and /d3-onboard announce phase atomicity at start.
- Decision proposals follow A/B/C with explicit recommendation and one-line rationale, no open-ended questions when avoidable.

Backlog carried into 2.x
- /d3-help contextual command.
- Migration procedure between 2.x versions.
- Growth management for journal.md.

### 1.x

Archived. v2.0 does not migrate from 1.x.
