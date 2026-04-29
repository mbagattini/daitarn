# Daitarn

A lightweight governance system for working with Claude Code.

Daitarn sits between vibe coding (no scope, no learning) and spec-driven design (heavy upfront ceremony). The pilot governs, the assistant executes within explicit bounds, and the project accumulates durable knowledge over time.

Daitarn is a learning-while-building tool. It deliberately trades speed for the pilot's grasp on what is happening in the codebase.

## How it works

Daitarn is implemented as a small set of Claude Code slash commands plus a structured folder of project knowledge. Work proceeds in steps. Each step follows a fixed five-phase flow:

1. /d3-1-brief — the pilot declares the goal of the step.
2. /d3-2-analyze — the assistant reads the brief and the code, produces an analysis with open questions.
3. /d3-3-plan — pilot and assistant converge on an approach in chat; the plan is written down.
4. /d3-4-build — the assistant implements the plan and commits.
5. /d3-5-close — review and closure, with carry-forward notes for the next step.

Two operating modes:

- pilot — the pilot reads and edits code alongside the assistant.
- auto — the pilot does not touch code (e.g. unfamiliar language); the assistant self-audits at closure.

Two non-flow commands:

- /d3-onboard — one-time bootstrap. Auto-detects greenfield vs brownfield and produces the reference files in a single guided session.
- /d3-commit — explicit commit for assistant work outside the flow.

## Folder layout

```
<project-root>/
├── CLAUDE.md              entry point: configuration, language, principles
├── .claude/commands/      slash commands
└── d3-docs/               configurable name; declared in CLAUDE.md
    ├── system/            off-limits to the assistant
    ├── reference/         project knowledge: perimeter, conventions, journal
    └── current-step/      working set for the step in progress
```

## Installation

1. Copy this scaffold into the root of your project.
2. Open CLAUDE.md and adjust:
   - Daitarn root if you want a different folder name.
   - Mode (pilot or auto).
   - Language settings (Documents, Interactions, Commits) using ISO 639-1 codes.
3. From inside Claude Code, run /d3-onboard. The assistant guides you through populating reference/perimeter.md and reference/conventions.md, adapting to whether the project is greenfield or brownfield.
4. Start your first step with /d3-1-brief.

## Versioning

This is Daitarn 2.0. There is no migration path from 1.x — 2.0 is a fresh scaffold, structurally different. See d3-docs/system/meta.md for the full changelog.

## Philosophy

Daitarn takes seriously the idea that AI should not erode the human's understanding of their own software. Knowing the codebase matters more than producing it quickly. Every design decision in the system serves that belief.
