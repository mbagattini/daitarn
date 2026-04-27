<!--
This file is the operating manual of the Daitarn governance system.
The assistant reads it on every interaction. Edit with care.
The pilot may freely replace placeholder sections (mission, project context)
without altering the governance rules below.
-->

# Daitarn — Governance Manual

## Project mission
<!-- Replace with one or two sentences about what this software does. -->
TBD by the pilot.

## Mode

`Mode: pilot`
<!--
Allowed values: pilot | auto

- pilot: the pilot reads, understands, and edits code. Flow includes
         /d3-review (assistant pre-pass) and /d3-recheck (after the
         pilot's manual edits).
- auto:  the pilot does not touch code. Flow uses /d3-self-audit instead
         of review/recheck. The pilot may still edit documents under
         specs/step/ (e.g. clarifying the brief, answering questions)
         and provide high-level feedback on observable results.

Change this line to switch modes for the project.
-->

## Operating principle

The pilot governs. The assistant executes within bounds.

- Nothing implicit. If it is not in the step brief or in `specs/step/decisions.md`, it is not done.
- Scope is declared in writing before any proposal.
- Sequence is normed. Each flow skill checks preconditions on the filesystem and refuses to start if a prerequisite is missing.
- Every flow skill ends with a `Next:` block — 3–5 short suggestions guiding the pilot's next move.

## Filesystem layout

```
daitarn/
├── CLAUDE.md
├── .d3/                         # OFF-LIMITS for the assistant
│   ├── system.md
│   ├── past/
│   ├── future/
│   ├── backlog.md
│   └── templates/
├── specs/
│   ├── project/
│   │   ├── core/                # always loaded
│   │   └── reference/           # consult only via /d3-recall
│   └── step/                    # the lung of the current step
└── src/
```

## Off-limits

`.d3/` is invisible to the assistant. The assistant never reads, lists, greps, references, or commits anything under `.d3/`, in any circumstance. The single exception is the **skill machinery**: a skill's procedure may copy a template from `.d3/templates/` to `specs/step/` as part of producing its output. The assistant does not browse `.d3/` outside of these explicit, mechanical reads.

`specs/project/reference/` is not read by default. It is consulted only through `/d3-recall "<query>"`, with a stated query and a stated reason.

## Language

English is the system of record. Conversations may happen in Italian or English. Anything written to disk — files, commits, proposals, decisions — is in English. A discussion held in Italian that produces a decision is recorded in English.

## Markdown style

Operational, not narrative. Bullets over prose where possible. Do not restate context the reader already has. Skip sections that have nothing to say. No decorative caveats, no closing summaries, no apologies.

## Skill catalog

### Flow (canonical sequence)
1. `/d3-analyze` — read `step-brief.md`, produce `understanding.md`.
2. `/d3-discuss` — resolve open questions, produce `decisions.md` (and `out-of-scope.md` if needed).
3. `/d3-implement` — write code per `decisions.md`, leave `implementation-notes.md`.
4. *Mode: pilot* → `/d3-review` — collaborative review before pilot's manual edits, produce `review-notes.md`.
   *Mode: auto* → `/d3-self-audit` — assistant audits its own implementation, produce `self-audit.md`.
5. *Mode: pilot* only → `/d3-recheck` — after pilot's manual edits, capture rationale, produce `recheck-learnings.md`.
6. `/d3-close` — distill the step, propose promotion plan, produce `closure-proposal.md`.

`/d3-review` and `/d3-recheck` refuse to run when `Mode: auto`.
`/d3-self-audit` refuses to run when `Mode: pilot`.

### Lookup
- `/d3-recall "<query>"` — search `specs/project/reference/`. Returns excerpts. Invocable inside any flow skill, with prior declaration of query and reason.

### Commit
- `/d3-commit-claude` — commits assistant's current staged work; prefix `[claude]`; auto-generated message.
- `/d3-commit-pilot` — commits pilot's manual changes; no prefix; auto-generated message.

## Anti-intraprendence rules

- Do not introduce libraries, files, or patterns that were not requested.
- Do not refactor code outside the current step's scope. Off-scope concerns go to `specs/step/out-of-scope.md`.
- Do not commit on your own initiative.
- Do not move files between `specs/step/`, `specs/project/`, and `.d3/`. Closure proposes; the pilot executes.
- Do not read anything under `.d3/` (past, future, backlog, system, templates outside of skill machinery).

## Project-level references (always loaded)

Read these at the start of every interaction:
- `specs/project/core/conventions.md` — code and naming conventions.
- `specs/project/core/glossary.md` — domain glossary.
- `specs/project/core/governance.md` — project-specific governance overrides, if any.
