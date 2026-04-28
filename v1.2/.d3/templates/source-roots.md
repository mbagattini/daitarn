<!--
TEMPLATE: source-roots.md
USE:      List of paths the assistant treats as project source.
DEST:     specs/project/core/source-roots.md
SYNTAX:   One path per line. Optional `[test]` tag at end of line marks
          a path as containing test code. `#` for comments. No globs.
RULE:     The assistant explores, samples, and writes code only inside
          paths listed here. Paths tagged [test] are treated separately
          where it matters (notably onboarding sampling and implementation
          writes). All paths are relative to the repo root.
-->

# Source roots

<!--
GREENFIELD DEFAULT (single root):

src

GREENFIELD WITH SEPARATE TESTS:

src
tests [test]

BROWNFIELD MULTI-ROOT (.NET solution example):

Platforms
Revorg.SBO.ServiceLayer
Revorg.SBO.ServiceLayer.Tests              [test]
Revorg.SBO.WarehouseExtender.Core
Revorg.SBO.WarehouseExtender.Core.Tests    [test]
Revorg.SBO.WarehouseExtender.UI
Revorg.SBO.WarehouseExtender.Utilities

BROWNFIELD MONOREPO EXAMPLE:

services/api
services/worker
packages/shared
apps/web
apps/web/__tests__                         [test]
-->

src
