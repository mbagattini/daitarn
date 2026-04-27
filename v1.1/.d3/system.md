<!--
PURPOSE: Self-describing manifest of the Daitarn governance system.
ACCESS: Off-limits during normal flow (lives under .d3/).
        Available to the pilot, and to future meta-analysis sessions
        if/when introduced.
USE:    Track system version, structure, and evolution. When you change
        the system (add a skill, rename a folder, alter a rule), append
        an entry to the changelog below.
-->

# Daitarn System

## Version

1.1 — dual-mode support (pilot / auto).

## Purpose of this file

Daitarn evolves. This file lets a future self (or a future meta-analysis
session) reconstruct what the system was at any point and why it changed.
CLAUDE.md describes the *current* state; this file describes the *history*.

## Snapshot at v1.0

**Structure**
- `CLAUDE.md` — operating manual (always loaded by the assistant).
- `.d3/` — pilot territory, off-limits to the assistant. Holds `past/`, `future/`, `backlog.md`, `templates/`, and this file.
- `specs/project/core/` — durable project knowledge, always loaded.
- `specs/project/reference/` — durable project knowledge, consulted via `/d3-recall`.
- `specs/step/` — ephemeral working set for the current step.
- `src/` — source code.

**Flow skills**: `/d3-analyze`, `/d3-discuss`, `/d3-implement`, `/d3-review`, `/d3-recheck`, `/d3-close`.
**Lookup skill**: `/d3-recall`.
**Commit skills**: `/d3-commit-claude`, `/d3-commit-pilot`.

**Step lifecycle**
1. Pilot drops a `step-brief.md` into `specs/step/`.
2. Flow runs through analyze → discuss → implement → review → (pilot edits) → recheck → close.
3. `/d3-close` proposes a promotion plan; the pilot executes the moves manually.
4. `specs/step/` is emptied; archived contents go to `.d3/past/step-<N>/`.

## Evolution log

Append entries newest-first as the system changes.

### 1.1 — dual-mode support
- Introduced `Mode:` declaration in CLAUDE.md (`pilot` | `auto`).
- Added `/d3-self-audit` skill and `self-audit.md` template for auto mode (replaces the review/recheck pair).
- `/d3-review` and `/d3-recheck` now refuse to run in auto mode.
- `/d3-self-audit` refuses to run in pilot mode.
- `/d3-implement` closing block is mode-aware.
- `/d3-close` preconditions are mode-aware: pilot expects `recheck-learnings.md`, auto expects `self-audit.md`.
- Auto mode contract: the pilot does not edit code; the pilot may edit documents under `specs/step/` and provide high-level feedback on observable behavior.

### 1.0 — initial scaffolding
- Established CLAUDE.md, six flow skills, one lookup, two commit skills.
- `.d3/` set as off-limits with the single exception of skill-machinery template reads.
- Project knowledge split into `core/` (auto-loaded) and `reference/` (consulted via `/d3-recall`).
- Closure produces a tabular promotion plan; the pilot executes promotions manually.
- Commits are explicit only, never autonomous; assistant uses `[claude]` prefix.
