# 0002 — Repository naming convention

Status: Accepted
Date: 2026-04-20

## Context

Repository names are visible, stable, and hard to change cleanly once referenced externally. A consistent convention across the organisation makes the structure self-explanatory to a new reader and prevents ad-hoc naming decisions accumulating inconsistency over time.

## Decision

**Collector repositories are named by their source.** The data source is the primary identity of a collector; the role of the repository is secondary. Collector names take the form `{source}-collector`, where `{source}` is a short, lowercase identifier for the data source.

**Platform and shared repositories are named by their role.** These repositories are named for what they do within the organisation, without an organisation prefix. The organisation namespace already provides context; repeating it is redundant.

**Names do not carry the organisation prefix.** The organisation name is already visible in the URL. `longhandarchive/platform` is clearer than `longhandarchive/longhandarchive-platform`.

Examples of the pattern in use:

- `civilservicejobs-collector` — a collector, named by its source.
- `platform` — the public-facing application, named by its role.
- `archive-contract` — a shared specification, named by its role.
- `governance` — the home for cross-cutting decisions, named by its role.

## Consequences

The organisation's repository list communicates structure at a glance. A reader can distinguish collectors from platform components without explanation.

New collectors will follow the `{source}-collector` pattern without requiring a naming discussion. New role-based repositories will follow the prefix-free convention.

Repositories that pre-date this convention and do not match it are renamed when the cost of renaming is low. Once external references exist, the cost of renaming rises and the convention yields to stability.
