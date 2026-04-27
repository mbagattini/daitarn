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

## Core ideas

**Scope is normed.** Each unit of work — a *step*, roughly 2–4 hours of human work — has an explicit brief, a written analysis, a set of binding decisions, and an implementation that does only what the decisions say. Anything that falls outside scope goes to a parking lot, never silently into the implementation.

**The assistant does not improvise.** A canonical sequence of skills (`/d3-analyze`, `/d3-discuss`, `/d3-implement`, `/d3-review`, `/d3-recheck`, `/d3-close`) governs the lifecycle of every step. Each skill checks preconditions on the filesystem and refuses to start if a required artifact is missing.

**Past, future, and system files are off-limits to the assistant.** They live under `.d3/`, which the assistant never reads outside of explicit skill machinery. This keeps the working context clean and prevents the assistant from drifting into past or planned work.

**Knowledge accumulates explicitly.** Each step ends with a closure proposal: what to promote into durable project knowledge, what to park in the backlog, what to drop. The pilot executes the moves manually. Over time, `specs/project/core/` and `specs/project/reference/` become the project's institutional memory.

**Two modes.** *Pilot mode* assumes the human reads, understands, and edits code. *Auto mode* (introduced in v1.1) is for projects in unfamiliar languages or stacks where the pilot cannot meaningfully edit the implementation. The flow adapts but the governance stays.

## Repository structure

```
daitarn/
├── CLAUDE.md                    # operating manual loaded by the assistant
├── .claude/commands/            # Daitarn skills (/d3-*)
├── .d3/                         # off-limits to the assistant
│   ├── system.md                # version + changelog of the system itself
│   ├── past/                    # closed steps, archived by the pilot
│   ├── future/                  # planning notes, pilot-only
│   ├── backlog.md               # parked ideas
│   └── templates/               # source templates for step documents
├── specs/
│   ├── project/
│   │   ├── core/                # always loaded by the assistant
│   │   └── reference/           # consulted only via /d3-recall
│   └── step/                    # ephemeral working set for the current step
└── src/                         # source code
```

## Getting started

1. Download the version you want use, likely the most recent one.
2. `git init` in the repository root.
3. In `CLAUDE.md`, fill in the *Project mission* section and choose the mode (`Mode: pilot` or `Mode: auto`).
4. Optionally fill the placeholders in `specs/project/core/` (conventions, glossary, governance overrides).
5. Write a `step-brief.md` in `specs/step/` for your first step, using `.d3/templates/step-brief.md` as a starting point.
6. Open Claude Code and invoke `/d3-analyze`.

From there, the assistant guides the next move at the end of every skill via a `Next:` block.

## Versions history

### v1.1 — dual-mode support

Adds support for projects where the pilot does not edit code (for example, projects written in languages or stacks the pilot is not fluent in). The governance, slicing, and knowledge-accumulation logic stay identical; only the review portion of the lifecycle changes.

**Added**
- A `Mode:` declaration in `CLAUDE.md`. Allowed values: `pilot` (default) and `auto`.
- A new skill `/d3-self-audit` for auto mode. It replaces the `/d3-review` + `/d3-recheck` pair: the assistant audits its own implementation against three explicit categories — scope creep, gaps versus decisions, technical fragility — and applies corrections in place. The skill is prompted to default to suspicion of its own work.
- A new template `.d3/templates/self-audit.md` with a dedicated section for high-level pilot feedback on observable behavior (the channel for the pilot's input in auto mode).

**Changed**
- `/d3-review` and `/d3-recheck` now refuse to run when `Mode: auto`.
- `/d3-self-audit` refuses to run when `Mode: pilot`.
- `/d3-implement`'s closing block is mode-aware: it suggests `/d3-review` in pilot mode and `/d3-self-audit` in auto mode.
- `/d3-close` preconditions are mode-aware: it expects `recheck-learnings.md` in pilot mode and `self-audit.md` in auto mode.

**Auto-mode contract**
- The pilot does not edit code.
- The pilot may still edit documents under `specs/step/` (clarifying the brief, answering open questions) and provide high-level feedback on observable behavior.
- `/d3-recheck`'s function — capturing knowledge from human review — is partially absorbed by `/d3-self-audit`'s *Things to watch* section. This is a known and accepted reduction in the knowledge-accumulation property of the system in auto mode.

### v1.0 — initial scaffolding

The first working version of the system.

**Includes**
- `CLAUDE.md` operating manual with anti-intraprendence rules and filesystem layout.
- Six flow skills: `/d3-analyze`, `/d3-discuss`, `/d3-implement`, `/d3-review`, `/d3-recheck`, `/d3-close`.
- One lookup skill: `/d3-recall` (queries `specs/project/reference/` with stated query and reason).
- Two commit skills: `/d3-commit-claude` (prefix `[claude]`) and `/d3-commit-pilot` (no prefix; pilot is the implicit author of unprefixed commits).
- Eight document templates under `.d3/templates/`, each with an inert HTML-comment header explaining its use.
- Split of project knowledge into `specs/project/core/` (always loaded) and `specs/project/reference/` (consulted on demand).
- `.d3/system.md` as a self-describing manifest with version and changelog of the system itself.
- English as the system of record (conversations may happen in any language; what is written to disk is in English).

## Design notes

A few decisions worth knowing about, because they show up everywhere in the system.

**HTML comments as inert metadata.** Document templates begin with a `<!-- ... -->` header explaining their use. The header is invisible when the document is rendered (e.g., on GitHub) but visible to text readers and to the assistant. The pilot may delete it or leave it in; either is fine.

**Commits are explicit, never autonomous.** The assistant never commits on its own. The pilot invokes `/d3-commit-claude` or `/d3-commit-pilot`. Messages are auto-generated from context. This keeps the git log a faithful audit trail of who did what, with prefix `[claude]` for the assistant and no prefix for the pilot.

**Closure proposes; the pilot executes.** The assistant never moves files between `specs/step/`, `specs/project/`, and `.d3/`. `/d3-close` produces a tabular promotion plan; the pilot performs the moves manually. This is the same principle that keeps `.d3/` off-limits — the assistant does not curate its own memory.

**Step-brief in, closure-proposal out.** Every step starts with a brief written by the pilot and ends with a closure proposal written by the assistant. Everything in between (`understanding.md`, `decisions.md`, `implementation-notes.md`, etc.) is intermediate workspace that gets distilled at close time.

## Contributing

This is a personal system that I am sharing in case it is useful. Feedback, issues, and pull requests are welcome but not actively solicited. If you fork it and adapt it to your own way of working, that is exactly the intended use.

## License

MIT License
