<!--
TEMPLATE: closure-proposal.md
USE:      Output of /d3-close.
DEST:     specs/step/closure-proposal.md
NOTE:     Distillation + promotion plan. The assistant proposes; the
          pilot decides and executes the moves manually.
-->

# Closure proposal — Step <N>

## Distillation

### What we decided and why
<!-- Binding choices that survived to close. -->

### What we built
<!-- Intent and location, not code.
     Example: "The logger lives in src/Logging/, configured at startup." -->

### What is left open
<!-- Unresolved items rolled forward. -->

### What we learned from the pilot's review
<!-- Unique knowledge from /d3-recheck. -->

## Promotion plan

| Item | Destination | Rationale |
|---|---|---|
|  | `specs/project/core/<file>.md` |  |
|  | `specs/project/reference/<file>.md` |  |
|  | `.d3/backlog.md` |  |
|  | drop |  |

## Suggested pilot actions

After your review:
1. Apply the promotion plan (manual moves into `specs/project/core/`, `specs/project/reference/`, `.d3/backlog.md`).
2. Archive `specs/step/` contents into `.d3/past/step-<N>/`.
3. Empty `specs/step/`.
4. When ready, drop the next step's `step-brief.md` into `specs/step/` and invoke `/d3-analyze`.
