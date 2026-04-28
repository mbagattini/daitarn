<!--
TEMPLATE: glossary.md
USE:      Domain glossary. Always loaded.
DEST:     specs/project/core/glossary.md
KEEP:     Brief, definitional. No prose explanations.
FORMAT:   Two viable styles below. Pick one and stick with it within
          the file for consistency.
-->

# Glossary

<!--
STYLE A — bold-term bullets (most common, best when terms are short
and definitions are one line). Example:

- **Order** — a customer's request for one or more products. Becomes a Shipment once paid.
- **Shipment** — physical delivery of an Order. One-to-one with Order in v1.
- **SKU** — stock keeping unit. The atomic product identifier; not the same as a catalog ID.
- **Tenant** — an isolated customer organization. Each tenant has its own schema.
-->

## Terms

- **<term>** — <one-line definition>.

<!--
STYLE B — table (use when definitions need a second column, e.g.
abbreviations or origin). Example:

| Term | Definition | Notes |
|---|---|---|
| ETA | Estimated Time of Arrival | Always UTC in the API |
| BFF | Backend For Frontend | Per-channel, not shared |
| Hot tier | In-memory cache layer | Redis cluster, max 24h TTL |
-->
