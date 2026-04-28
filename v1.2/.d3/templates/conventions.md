<!--
TEMPLATE: conventions.md
USE:      Code and naming conventions for the project. Always loaded.
DEST:     specs/project/core/conventions.md
KEEP:     Brief. This file is in context on every interaction.
FORMAT:   No single right format. Below are three styles. Pick what fits
          each section, mix freely. Delete the styles you don't use.
-->

# Conventions

<!--
STYLE A — keyed bullets (good for small, atomic rules).
Example:

## Code style
- **Indentation:** 4 spaces, no tabs.
- **Line length:** 100 cols soft limit.
- **Brace style:** opening brace on same line.
- **Language version:** C# 12 / .NET 8.
- **Formatter:** dotnet format, run on save.
-->

## Code style
- **Indentation:** 
- **Line length:** 
- **Brace style:** 
- **Language version:** 
- **Formatter:** 

<!--
STYLE B — table (good when each rule has the same columns).
Example:

## Naming

| Element | Convention | Example |
|---|---|---|
| Class | PascalCase | `OrderProcessor` |
| Method | PascalCase | `ComputeTotal` |
| Local variable | camelCase | `pendingOrders` |
| Constant | SCREAMING_SNAKE | `MAX_RETRIES` |
| File | matches type name | `OrderProcessor.cs` |
-->

## Naming

| Element | Convention | Example |
|---|---|---|
|  |  |  |

<!--
STYLE C — short prose paragraphs (good for things that need rationale,
not just rules). Example:

## File and folder organization
Each bounded context lives under `src/<Context>/`. Within a context,
domain types go in `Domain/`, application services in `Application/`,
infrastructure in `Infrastructure/`. Tests mirror this structure under
`tests/<Context>/`. Cross-context shared types live in
`src/Shared/` and must remain dependency-free.
-->

## File and folder organization
<!-- One short paragraph. -->
