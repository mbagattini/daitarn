---
description: One-time onboarding pass — produce a high-level map of the codebase.
---

# /d3-onboard-map

You are running the **map** pass of onboarding.

## Precondition
- Read `specs/project/core/source-roots.md`. At least one listed root must exist and contain code. If none do, refuse:

  > `/d3-onboard-map` requires at least one populated source root (see `specs/project/core/source-roots.md`). For greenfield, the map will grow naturally as steps progress.

## Soft guard
If `specs/project/core/map.md` is non-placeholder (i.e. contains content beyond the template comments), warn in chat:

> `map.md` already has content. Proceeding will overwrite it. Git protects your previous version. Continue? Reply "yes" to proceed.

Do not proceed without confirmation. If the file is still in template form, no warning is needed.

## Procedure
1. Read `source-roots.md`. Note which roots are tagged `[test]`.
2. Explore each non-test source root: top-level directories, key subdirectories, build files, entry points, project files (`*.csproj`, `package.json`, `pyproject.toml`, etc.).
3. Identify modules and their apparent purposes. Stay at the level of "what is this folder for", not "how does this function work".
4. Note non-obvious dependencies between modules.
5. For test roots, note their existence and which production roots they cover, but do not document their internal structure in detail.
6. Copy `.d3/templates/map.md` to `specs/project/core/map.md` and fill it. Cover production roots in detail; test roots get a brief mention.
7. In chat, list 2–5 points where you are uncertain or had to guess. Keep it short.

## Rules
- Stay high-level. Files are noticed; functions are not.
- Do not edit code.
- Reading any path is allowed. Boundaries restrict writes only.

## Output
- `specs/project/core/map.md`

## Closing block
> Done with `/d3-onboard-map`. Output: `specs/project/core/map.md`.
> **Next:**
> 1. Open `specs/project/core/map.md` in your editor. The current content sets the tone; add anything I couldn't infer (private context, business reasoning, "this folder is misnamed for historical reasons").
> 2. Quick chat fixes: tell me directly if any module purpose is wrong and I'll rewrite that row.
> 3. Run `/d3-commit-pilot` when satisfied.
> 4. Suggested next pass: `/d3-onboard-boundaries`.
