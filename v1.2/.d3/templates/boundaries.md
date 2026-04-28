<!--
TEMPLATE: boundaries.md
USE:      Read-only paths. Always loaded.
DEST:     specs/project/core/boundaries.md
SYNTAX:   gitignore-style patterns. Same operators as .gitignore:
            **/      any directory
            *.ext    extension match
            !pattern negation (re-include)
            #        comment
RULE:     The assistant must not write to any path matching these
          patterns. Reading is always allowed. There is no "fragile"
          tier — a path is either read-only or normal.
-->

# Boundaries

<!--
EXAMPLE:

# Legacy code under contract; mirrors an external system.
src/legacy/**

# Generated from build scripts; manual edits will be lost.
src/generated/**
**/*.g.cs

# Existing migrations are immutable; new ones go in pending/.
migrations/*.sql
!migrations/pending/

# Vendored dependencies.
vendor/**
third_party/**

# CI configuration is owned by platform team.
.github/workflows/**
-->

# Add patterns below. An empty file means "no read-only paths".
