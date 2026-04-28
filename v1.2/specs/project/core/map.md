<!--
TEMPLATE: map.md
USE:      High-level map of the codebase. Always loaded.
DEST:     specs/project/core/map.md
KEEP:     High-level. Names and one-line purposes. No deep architecture.
WHEN:     For brownfield projects, populated by /d3-onboard-map.
          For greenfield, may stay empty until the codebase is large
          enough to need a map (no fixed threshold).
FORMAT:   Mix tree + table. Tree for shape, table for purposes.
-->

# Map

<!--
EXAMPLE — tree of top-level areas:

```
src/
├── Api/                # HTTP entry points, controllers, DTOs
├── Application/        # use cases, orchestration, transactions
├── Domain/             # entities, value objects, domain services
├── Infrastructure/     # persistence, external services, messaging
└── Shared/             # cross-cutting types (must stay dependency-free)
```
-->

## Shape

```
<paste a 1-2 level tree here>
```

<!--
EXAMPLE — module table:

| Module | Purpose | Notes |
|---|---|---|
| `Api/Orders` | order endpoints | thin; delegates to Application |
| `Application/Orders` | order use cases | transactional; entry to Domain |
| `Domain/Orders` | order aggregate | invariants live here |
| `Infrastructure/Persistence` | EF Core + SQL Server | connection from config |
| `Infrastructure/Messaging` | RabbitMQ publishers | retry policies in Shared |
-->

## Modules

| Module | Purpose | Notes |
|---|---|---|
|  |  |  |

<!--
EXAMPLE — entry points (good to call out explicitly):

## Entry points
- `src/Api/Program.cs` — HTTP host startup.
- `src/Worker/Program.cs` — background job host.
- `tools/seed/Program.cs` — one-off seed CLI.
-->

## Entry points
- 

<!--
EXAMPLE — known dependencies between modules (only the non-obvious ones):

## Notable dependencies
- `Application/*` depends on `Domain/*` only.
- `Infrastructure/Messaging` is shared between Api and Worker hosts.
- `Shared/` has no dependencies on any other internal module.
-->

## Notable dependencies
- 
