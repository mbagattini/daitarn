# Daitarn

A governance system for working on software projects with Claude Code.

Daitarn sits between *vibe coding* (no governance, full speed, no learning) and *spec-driven design* (heavy upfront discussion). It is built around the idea that the human pilot retains control of scope, decisions, and the rhythm of work, while the assistant executes within explicit bounds and the project accumulates durable knowledge over time.

The name comes from the anime *Daitarn 3* — specifically from the relationship between the mecha and its pilot, where neither is useful without the other.

## Who this is for

You are likely to find Daitarn useful if:

- You want to use Claude Code on real software projects without losing track of what is happening and why.
- You value learning the codebase as much as producing it. Daitarn deliberately trades speed for knowledge.
- You have tried fully autonomous AI coding and found it produces too much, too fast, in directions you did not authorize.
- You have tried heavy spec-driven approaches and found the upfront ceremony exhausting.
- You work on existing codebases (brownfield) and want to add Claude Code without it sprawling all over the place.

## Core ideas

**Scope is normed.** Each unit of work — a *step*, roughly 2–4 hours of human work — has an explicit brief, a written analysis, a set of binding decisions, and an implementation that does only what the decisions say. Anything that falls outside scope goes to a parking lot, never silently into the implementation.

**The assistant does not improvise.** A canonical sequence of slash commands governs the lifecycle of every step. Each command checks preconditions on the filesystem and refuses to start if a required artifact is missing.

**Past, future, and system files are off-limits to the assistant.** They live under `.d3/`, which the assistant never reads outside of explicit command machinery. This keeps the working context clean and prevents drift into past or planned work.

**Knowledge accumulates explicitly.** Each step ends with a closure proposal: what to promote into durable project knowledge, what to park in the backlog, what to drop. The pilot executes the moves manually. Over time, `specs/project/core/` and `specs/project/reference/` become the project's institutional memory.

**Source roots and read-only paths are declarative.** A small file tells the assistant where the source code lives (one or many directories) and which paths are read-only. This makes Daitarn work for greenfield projects, multi-project solutions, and existing codebases without code changes to the system.

**Two modes.** *Pilot mode* assumes the human reads, understands, and edits code. *Auto mode* is for projects in unfamiliar languages or stacks where the pilot cannot meaningfully edit the implementation. The flow adapts but the governance stays.

## Repository structure

```
daitarn/
├── CLAUDE.md                    # operating manual loaded by the assistant
├── .claude/commands/            # Daitarn slash commands (/d3-*)
├── .d3/                         # off-limits to the assistant
│   ├── system.md                # version + changelog of the system itself
│   ├── past/                    # closed steps, archived by the pilot
│   ├── future/                  # planning notes, pilot-only
│   ├── backlog.md               # parked ideas
│   └── templates/               # source templates for documents
├── specs/
│   ├── project/
│   │   ├── core/                # always loaded by the assistant
│   │   │   ├── source-roots.md  # declared source paths (incl. test tag)
│   │   │   ├── boundaries.md    # read-only paths (gitignore syntax)
│   │   │   ├── map.md           # high-level codebase map
│   │   │   ├── conventions.md   # code and naming conventions
│   │   │   ├── glossary.md      # domain glossary
│   │   │   └── governance.md    # project-specific governance overrides
│   │   └── reference/           # consulted only via /d3-recall
│   └── step/                    # ephemeral working set for the current step
└── <source roots>               # source code; default is src/, configurable
```

## Getting started

### Greenfield project

1. Download the version you want use, likely the most recent one.
2. `git init` in the repository root.
3. In `CLAUDE.md`, fill in the *Project mission* section and choose the mode (`Mode: pilot` or `Mode: auto`).
4. Optionally fill the placeholders in `specs/project/core/` (conventions, glossary, governance overrides). They can also stay empty and grow over time.
5. Write a `step-brief.md` in `specs/step/` for your first step, using `.d3/templates/step-brief.md` as a starting point.
6. Open Claude Code and invoke `/d3-analyze`.

The assistant guides the next move at the end of every command via a `Next:` block.

### Brownfield project (existing codebase)

1. Extract the v1.2 scaffold into your existing repository root. The scaffold adds `CLAUDE.md`, `.claude/`, `.d3/`, and `specs/`. It also includes a default `src/` directory — delete it if your project does not use that path.
2. Edit `specs/project/core/source-roots.md`. Replace the default `src` line with the actual source directories of your project. Mark test directories with `[test]`.
3. In `CLAUDE.md`, fill *Project mission* and choose the mode.
4. Run the onboarding commands, in order, to populate `specs/project/core/`:
   - `/d3-onboard-map` — high-level codebase map.
   - `/d3-onboard-boundaries` — propose read-only paths.
   - `/d3-onboard-conventions` — extract code and naming conventions.
   - `/d3-onboard-avoid` — populate `specs/project/reference/avoid.md` with rejected approaches and anti-patterns.
   - `/d3-onboard-finalize` — read-only consistency check across the four files.
5. After each onboarding command, the assistant writes a first draft and surfaces uncertainties in chat. The pilot fixes obvious mistakes in conversation, then opens the file in an editor to add what the assistant could not infer (private context, business reasoning, "this convention is a retaggio, don't follow it").
6. Once onboarding is complete, the project is structurally indistinguishable from a greenfield project at step N. From here, the regular flow begins: drop a `step-brief.md` and invoke `/d3-analyze`.

Onboarding can also be re-run later — for example if `conventions.md` has degraded over time and you want to re-extract from the codebase.

## Versions history

### v1.2 — onboarding, boundaries, source roots

Adds first-class support for working on existing codebases (brownfield) without altering the core flow. Also makes the source layout configurable, so projects with multiple source directories or non-`src/` layouts work natively.

**Added — declarative configuration**
- `specs/project/core/source-roots.md` — one path per line, optional `[test]` tag for test directories. Replaces the previous implicit assumption that source lives in `src/`. Default is `src` (greenfield-compatible); brownfield projects override.
- `specs/project/core/boundaries.md` — gitignore-syntax patterns for read-only paths. The assistant refuses to write to matching paths but reads them freely.
- `specs/project/core/map.md` — high-level codebase map. For brownfield, populated by `/d3-onboard-map`. For greenfield, may stay empty until the codebase is large enough to need a map.

**Added — onboarding commands** (one-time, also usable to refresh degraded core files)
- `/d3-onboard-map` — high-level structural map.
- `/d3-onboard-boundaries` — propose read-only paths from observable signals.
- `/d3-onboard-conventions` — extract code and naming conventions from samples; treats production roots and `[test]`-tagged roots distinctly.
- `/d3-onboard-avoid` — populate `avoid.md` from in-code signals plus a focused conversation with the pilot.
- `/d3-onboard-finalize` — read-only consistency check across the four files. Reports inconsistencies; does not write.

**Added — onboarding pattern**
Each onboarding command writes a first draft directly to the target file, surfaces uncertainties in chat for quick correction, and explicitly hands off to the pilot's editor for substantive additions. The handoff is the key insight: large additions that the pilot needs to make are easier in an editor than in chat, and the assistant's draft fixes the tone of the document so the pilot's additions land in the same register.

**Changed**
- `CLAUDE.md` includes the new core files in *Project-level references (always loaded)* and updates the anti-intraprendence rules to require checking `boundaries.md` before any write inside a source root, and to disallow writes outside source roots without explicit pilot confirmation.
- `/d3-implement` validates write targets against `source-roots.md` and `boundaries.md` before writing.
- All `core/` files now have proper templates in `.d3/templates/` with inert format examples (keyed bullets / table / prose) — previously only the placeholder lived in `core/` directly.
- Terminology cleanup throughout: "skill" → "slash command" / "command", since Daitarn uses Claude Code slash commands (explicit pilot invocation), not Claude Code skills (autonomous, descriptor-triggered tools — a different mechanism).

### v1.1 — dual-mode support

Adds support for projects where the pilot does not edit code (for example, projects written in languages or stacks the pilot is not fluent in). The governance, slicing, and knowledge-accumulation logic stay identical; only the review portion of the lifecycle changes.

**Added**
- A `Mode:` declaration in `CLAUDE.md`. Allowed values: `pilot` (default) and `auto`.
- A new slash command `/d3-self-audit` for auto mode. It replaces the `/d3-review` + `/d3-recheck` pair: the assistant audits its own implementation against three explicit categories — scope creep, gaps versus decisions, technical fragility — and applies corrections in place. The prompt defaults to suspicion of its own work.
- A new template `.d3/templates/self-audit.md` with a dedicated section for high-level pilot feedback on observable behavior.

**Changed**
- `/d3-review` and `/d3-recheck` refuse to run when `Mode: auto`.
- `/d3-self-audit` refuses to run when `Mode: pilot`.
- `/d3-implement`'s closing block is mode-aware: it suggests `/d3-review` in pilot mode and `/d3-self-audit` in auto mode.
- `/d3-close` preconditions are mode-aware: it expects `recheck-learnings.md` in pilot mode and `self-audit.md` in auto mode.

**Auto-mode contract**
- The pilot does not edit code.
- The pilot may still edit documents under `specs/step/` (clarifying the brief, answering open questions) and provide high-level feedback on observable behavior.
- The knowledge-capture function of `/d3-recheck` is partially absorbed by `/d3-self-audit`'s *Things to watch* section. This is a known and accepted reduction in the knowledge-accumulation property of the system in auto mode.

### v1.0 — initial scaffolding

The first working version of the system.

**Includes**
- `CLAUDE.md` operating manual with anti-intraprendence rules and filesystem layout.
- Six flow commands: `/d3-analyze`, `/d3-discuss`, `/d3-implement`, `/d3-review`, `/d3-recheck`, `/d3-close`.
- One lookup command: `/d3-recall` (queries `specs/project/reference/` with stated query and reason).
- Two commit commands: `/d3-commit-claude` (prefix `[claude]`) and `/d3-commit-pilot` (no prefix; pilot is the implicit author of unprefixed commits).
- Eight document templates under `.d3/templates/`, each with an inert HTML-comment header explaining its use.
- Split of project knowledge into `specs/project/core/` (always loaded) and `specs/project/reference/` (consulted on demand).
- `.d3/system.md` as a self-describing manifest with version and changelog of the system itself.
- English as the system of record (conversations may happen in any language; what is written to disk is in English).

## Design notes

A few decisions worth knowing about, because they show up everywhere in the system.

**HTML comments as inert metadata.** Document templates begin with a `<!-- ... -->` header explaining their use. The header is invisible when the document is rendered (e.g., on GitHub) but visible to text readers and to the assistant. The pilot may delete it or leave it in; either is fine.

**Commits are explicit, never autonomous.** The assistant never commits on its own. The pilot invokes `/d3-commit-claude` or `/d3-commit-pilot`. Messages are auto-generated from context. This keeps the git log a faithful audit trail of who did what, with prefix `[claude]` for the assistant and no prefix for the pilot.

**Closure proposes; the pilot executes.** The assistant never moves files between `specs/step/`, `specs/project/`, and `.d3/`. `/d3-close` produces a tabular promotion plan; the pilot performs the moves manually. This is the same principle that keeps `.d3/` off-limits — the assistant does not curate its own memory.

**Step-brief in, closure-proposal out.** Every step starts with a brief written by the pilot and ends with a closure proposal written by the assistant. Everything in between is intermediate workspace that gets distilled at close time.

**Onboarding writes drafts, the pilot integrates in editor.** For onboarding commands, the assistant produces a first draft and ends in the editor handoff. Quick corrections happen in chat; substantive additions happen in the editor. This pattern recognizes that the two modalities have different sweet spots and uses each for what it does best.

## Contributing

This is a personal system that I am sharing in case it is useful. Feedback, issues, and pull requests are welcome but not actively solicited. If you fork it and adapt it to your own way of working, that is exactly the intended use.

## License

MIT License.
