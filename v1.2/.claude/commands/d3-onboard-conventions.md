---
description: One-time onboarding pass — extract code and naming conventions from the codebase.
---

# /d3-onboard-conventions

You are running the **conventions** pass of onboarding.

## Precondition
- Read `specs/project/core/source-roots.md`. At least one listed root must exist and contain code.

## Soft guard
If `specs/project/core/conventions.md` already has non-placeholder content, warn before overwriting.

## What to extract
Sample the codebase and infer:
- **Code style** — indentation, line length, brace placement, language version, formatter (look for `.editorconfig`, `.prettierrc`, etc.).
- **Naming** — for types, methods, variables, files, namespaces. Look at multiple examples to confirm a pattern, not just one.
- **File and folder organization** — structure of a typical module, where tests live, where shared types live.
- **Error handling** — exceptions vs. result types, where errors are caught, how they propagate.
- **Logging** — which library, where it's configured, what gets logged.
- **Testing** — framework, structure, naming, mocking style.
- **Imports / using statements** — order, grouping, aliases.

Skip what you cannot infer with confidence. A short conventions file is more useful than a long one full of guesses.

## Procedure
1. Read `source-roots.md`. Sample primarily from non-test roots for production conventions; sample from test roots only when extracting test-specific conventions (testing framework, test naming, mocking style).
2. If `boundaries.md` is populated, respect it during sampling — don't draw conventions from read-only paths, those patterns are not the project's current style.
3. Sample several files per category, not just one.
4. Copy `.d3/templates/conventions.md` to `specs/project/core/conventions.md`.
5. Fill the file. Use the format styles in the template (keyed bullets, table, prose) appropriately for each section. Mix styles freely. Keep production and test conventions in separate sections when they differ.
6. In chat, list:
   - Categories you populated with high confidence.
   - Categories where you are uncertain and the pilot should review carefully.
   - Categories you skipped because the code didn't speak clearly.

## Rules
- Cite evidence in chat ("indentation: 4 spaces — checked X.cs, Y.cs, Z.cs"). Don't cite in the file itself; the file is reference, not justification.
- Don't guess. Skipped is fine.
- Don't propose conventions that "should" exist. Only what is actually in the code.

## Output
- `specs/project/core/conventions.md`

## Closing block
> Done with `/d3-onboard-conventions`. Output: `specs/project/core/conventions.md`.
> **Next:**
> 1. Review the high-confidence sections in chat. Correct what's wrong.
> 2. Open the file in your editor to add what I skipped or couldn't infer (rationale, exceptions, "this convention is a retaggio, don't follow it for new code").
> 3. Run `/d3-commit-pilot` when satisfied.
> 4. Suggested next pass: `/d3-onboard-avoid`.
