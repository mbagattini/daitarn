<!--
PURPOSE: Self-describing manifest of the Daitarn governance system.
ACCESS: Off-limits during normal flow (lives under .d3/).
        Available to the pilot, and to future meta-analysis sessions
        if/when introduced.
USE:    Track system version, structure, and evolution. When you change
        the system (add a command, rename a folder, alter a rule), append
        an entry to the changelog below.
-->

# Daitarn System

## Version

1.2 — onboarding, boundaries, expanded core templates.

## Purpose of this file

Daitarn evolves. This file lets a future self (or a future meta-analysis
session) reconstruct what the system was at any point and why it changed.
CLAUDE.md describes the *current* state; this file describes the *history*.

## Snapshot at v1.2

**Structure**
- `CLAUDE.md` — operating manual (always loaded by the assistant).
- `.d3/` — pilot territory, off-limits to the assistant. Holds `past/`, `future/`, `backlog.md`, `templates/`, and this file.
- `specs/project/core/` — durable project knowledge, always loaded. Includes `source-roots.md`, `conventions.md`, `glossary.md`, `governance.md`, `map.md`, `boundaries.md`.
- `specs/project/reference/` — durable project knowledge, consulted via `/d3-recall`.
- `specs/step/` — ephemeral working set for the current step.
- `<source roots>` — source code, as declared in `specs/project/core/source-roots.md`. Default is `src/`; brownfield projects override to point at actual source directories.

**Onboarding commands**: `/d3-onboard-map`, `/d3-onboard-boundaries`, `/d3-onboard-conventions`, `/d3-onboard-avoid`, `/d3-onboard-finalize`.
**Flow commands**: `/d3-analyze`, `/d3-discuss`, `/d3-implement`, `/d3-review`, `/d3-recheck`, `/d3-self-audit`, `/d3-close`.
**Lookup command**: `/d3-recall`.
**Commit commands**: `/d3-commit-claude`, `/d3-commit-pilot`.

**Modes**: `pilot` (default; pilot edits code, review + recheck) and `auto` (pilot does not edit code; self-audit replaces review/recheck).

**Step lifecycle**
1. Pilot drops a `step-brief.md` into `specs/step/`.
2. Flow runs through analyze → discuss → implement → review/self-audit → (pilot edits, pilot mode only) → recheck → close.
3. `/d3-close` proposes a promotion plan; the pilot executes the moves manually.
4. `specs/step/` is emptied; archived contents go to `.d3/past/step-<N>/`.

**Brownfield bootstrap (or core-file refresh)**
Run the onboarding commands once before the first regular step. After onboarding, the system is structurally indistinguishable from a greenfield project at step N.

## Evolution log

Append entries newest-first as the system changes.

### 1.2 — onboarding, boundaries, source roots, expanded core templates
- Added `source-roots.md` to `specs/project/core/` — declarative list of paths that contain project source. One path per line, optional `[test]` tag for test directories. Always loaded. Removes the previous implicit assumption that source lives under `src/`. Default content is `src` (greenfield-compatible); brownfield projects override it.
- Added `boundaries.md` to `specs/project/core/` (gitignore-syntax read-only paths). Always loaded. CLAUDE.md anti-intraprendence rules updated to require checking it before any write under any source root, and to disallow writes outside source roots without explicit pilot confirmation.
- Added `map.md` to `specs/project/core/` (high-level codebase map). Always loaded.
- Added five onboarding slash commands (one-time, brownfield bootstrap or core-file refresh):
  - `/d3-onboard-map`, `/d3-onboard-boundaries`, `/d3-onboard-conventions`, `/d3-onboard-avoid`, `/d3-onboard-finalize`.
  - All preconditions read `source-roots.md` instead of assuming `src/`.
  - `/d3-onboard-map` and `/d3-onboard-conventions` treat `[test]`-tagged roots distinctly from production roots.
- Onboarding pattern: each command writes a first draft directly to its target file, surfaces uncertainties in chat, and explicitly hands off to the pilot's editor for substantive additions. Finalize is a read-only consistency check across the four files.
- Soft warning on overwrite of non-placeholder content (git protects).
- All `core/` files now have proper templates under `.d3/templates/` with inert format examples (keyed bullets / table / prose).
- `/d3-implement` validates write targets against `source-roots.md` and `boundaries.md`. Writes outside source roots require pilot confirmation.
- Terminology cleanup: "skill" → "slash command" / "command" throughout, since Daitarn uses Claude Code slash commands, not Claude Code skills (which are a different mechanism for autonomous, descriptor-triggered tools).

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
