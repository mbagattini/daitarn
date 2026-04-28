---
description: One-time onboarding pass — propose read-only paths in gitignore syntax.
---

# /d3-onboard-boundaries

You are running the **boundaries** pass of onboarding.

## Precondition
- Read `specs/project/core/source-roots.md`. At least one listed root must exist and contain code. If none do, refuse:

  > `/d3-onboard-boundaries` requires at least one populated source root. For greenfield, populate `boundaries.md` manually if needed.

## Soft guard
If `specs/project/core/boundaries.md` already has non-placeholder patterns, warn:

> `boundaries.md` already has patterns. Proceeding will overwrite. Git protects the previous version. Continue?

## Signals to look for
Propose paths as read-only when you observe:
- Folder names suggesting legacy or external origin: `legacy/`, `vendor/`, `third_party/`, `external/`.
- Folder names suggesting generation: `generated/`, `gen/`, `auto/`, `*.g.*` file patterns.
- File headers stating "DO NOT EDIT" or "AUTO-GENERATED".
- Build tooling outputs that happen to be tracked: `dist/`, `build/`, `obj/`, `bin/` (rare but possible).
- Migration files where existing migrations should be immutable (typical pattern: `migrations/*.sql` with new ones added but old ones never modified).
- CI/infrastructure config that is typically owned by a different role (`.github/workflows/`, `.gitlab-ci.yml`, etc.) — propose, but mark as low confidence.

Do not propose generic exclusions like `node_modules/` or `.git/` — those are not part of the source roots and don't need entries here.

## Procedure
1. Read `source-roots.md`. Scan within and around the listed roots for the signals above.
2. Copy `.d3/templates/boundaries.md` to `specs/project/core/boundaries.md`.
3. Fill it with proposed patterns. Each pattern with a brief comment line above it explaining why.
4. In chat, list each proposal with confidence: high (clear signal in code) or low (guess, needs pilot judgment).
5. Explicitly note things you considered but did NOT include, with reason.

## Rules
- gitignore syntax. Nothing else.
- Comments above each pattern, not after.
- One concept per pattern. Don't combine unrelated paths.
- An empty `boundaries.md` (after this pass) is a valid outcome if nothing in the codebase warrants it.

## Output
- `specs/project/core/boundaries.md`

## Closing block
> Done with `/d3-onboard-boundaries`. Output: `specs/project/core/boundaries.md`.
> **Next:**
> 1. Review my proposals in chat — especially the low-confidence ones. Tell me which to keep, adjust, or drop.
> 2. Open the file in your editor to add patterns I couldn't infer (paths whose read-only status comes from team conventions, not from the code itself).
> 3. Run `/d3-commit-pilot` when satisfied.
> 4. Suggested next pass: `/d3-onboard-conventions`.
