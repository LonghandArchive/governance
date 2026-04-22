# Architecture

This document describes the architecture of The Longhand Archive. It is the authoritative reference for how components relate to one another and where responsibilities lie. Every repository's `CLAUDE.md` references this document as the source of truth for cross-cutting architectural context.

## The shape of the project

The Longhand Archive is an archival platform for UK public sector data. It separates two concerns: the capture of data from its original public sources, and the derivation of queryable, analytical, or presentational views from that captured data.

This separation is the foundational architectural commitment. Capture and derivation have different lifecycles, different failure profiles, different audiences, and different authority. Mixing them produces systems that are fragile in all of those dimensions at once. Keeping them separate — at the repository level, the code level, and the data level — is what allows each side to evolve independently.

## The seven layers

The system is organised into seven conceptual layers. Not seven services. Not seven repositories. Seven layers of responsibility, each with a defined role and defined boundaries.

### 1. Collectors

Collectors capture data from public sources. Each collector owns one source. It handles the specifics of that source — authentication, parsing, rate limiting, lifecycle tracking, asset retrieval — and produces a local archive as its output.

Collectors are independent. A collector does not know about the platform, the database, or any consumer of its output. It produces to the archive contract and stops there.

Each collector is its own repository under the naming pattern `{source}-collector`. The first and currently only collector is `civilservicejobs-collector`.

### 2. The archive contract

The archive contract is the versioned specification of what collectors produce and what consumers can rely on finding. It defines the directory layout, file formats, field schemas, invariants, and provenance metadata that constitute a conforming archive.

The contract is the only interface through which a consumer reads a collector's output. Consumers do not reach into collector internals. Collectors do not adjust output to accommodate consumer preferences. Changes to what either side depends on are changes to the contract.

The contract lives in its own repository: [`archive-contract`](https://github.com/longhandarchive/archive-contract).

### 3. The sync / projection layer

The sync layer reads from collector archives and projects the data into the platform's queryable form — currently Postgres. It is the bridge between the authoritative archive and the derived database.

The sync layer is one-directional. It reads from archives and writes to the database. It never writes back to archives. It never exposes database state to collectors.

The sync layer applies compliance transformations — most notably, personal data redaction per [`decisions/0007`](decisions/0007-personal-data-redacted-at-projection-boundary.md) — at the boundary between archive and projection. The raw archive retains complete data; the projection only receives the minimised version.

The sync layer is part of the platform repository.

### 4. The data layer

The data layer defines the domain models, queries, and database access patterns that the rest of the platform uses to interact with stored data. It is the single place where the shape of a job, an event, an asset, or a user is defined in code.

The data layer includes the database schema itself. The platform uses a single Postgres instance with two logically separate schemas: `archive` for the projection of collector data, and `accounts` for authoritative user data. Foreign keys do not cross the schema boundary. See [`platform/docs/decisions/0001`](https://github.com/longhandarchive/platform/blob/main/docs/decisions/0001-two-schema-database-model.md).

The data layer is consumed by the sync layer (which writes to `archive`) and by the application layer (which reads from `archive` and reads from and writes to `accounts`).

The data layer is part of the platform repository.

### 5. The application layer

The application layer handles HTTP requests, routing, view logic, template rendering, JSON endpoints, authentication when it exists, rate limiting, and attribution envelopes. It depends on the data layer for access to stored data and knows nothing about how that data arrived.

The application layer serves both HTML (for the public site) and JSON (for internal API calls, and eventually for a public API when that becomes warranted). These are aspects of the same application, not separate systems. They share models, authentication, and attribution handling.

The application layer is part of the platform repository.

### 6. The presentation layer

The presentation layer is the HTML, CSS, and client-side JavaScript that runs in the browser. It is the user interface.

For the current phase, the presentation layer is not architecturally separate from the application layer. It consists of server-rendered templates, stylesheets, and any client-side code required for specific interactive components. The specific rendering approach — pure server-side, progressive enhancement, or hybrid — is an open decision flagged in the phase-one brief.

The presentation layer becomes architecturally separate only if a distinct client emerges — a native mobile application, for example — that consumes the application layer's JSON endpoints rather than its HTML. No such client is planned for phase one.

### 7. The public API

The public API is a documented, versioned, stable JSON interface exposed to external consumers — researchers, journalists, other public-sector data projects. It is distinct from the internal JSON endpoints the web front end uses, though it may be built from the same underlying code.

The public API does not exist yet. It will be introduced when external consumers earn its existence — that is, when there is evidence of demand for programmatic access and when the cost of formalising a stable interface is justified by that demand. Until then, the application layer's JSON endpoints are internal and subject to change without notice.

When the public API is introduced, the three-test rule in [`decisions/0001`](decisions/0001-new-repositories-require-three-tests.md) applies to the question of whether it earns its own repository or remains inside the platform.

## Repositories and layers

The mapping between repositories and layers is intentional and should be preserved.

- [`civilservicejobs-collector`](https://github.com/longhandarchive/civilservicejobs-collector) — the first collector. Future collectors occupy their own repositories.
- [`archive-contract`](https://github.com/longhandarchive/archive-contract) — the contract between collectors and consumers. Shared specification.
- [`platform`](https://github.com/longhandarchive/platform) — the sync layer, the data layer, the application layer, and the presentation layer. One repository, internally layered.
- [`governance`](https://github.com/longhandarchive/governance) — cross-cutting decisions and principles. No code; documentation only.
- [`.github`](https://github.com/longhandarchive/.github) — organisation profile and shared configuration. Public.

Code that belongs to a specific layer lives in the repository that owns that layer. Code that would cross layers — for example, a utility that both a collector and the sync layer need — is a signal that a shared library may eventually be needed, but is not extracted until at least two concrete cases demonstrate the need.

## Authority and derivation

The authority hierarchy is explicit.

The original public source is the ultimate authority for the data. It is what the project is preserving.

The collector's archive is the authoritative local representation of the source. It is the thing that must not be lost, and the thing from which everything else is derived.

The platform's Postgres database is a derived projection of the archive. It is rebuildable. If the database is destroyed, it is restored by re-projecting from the archive, not by recovering from backup.

The website, the API, and any future derived views are projections of the database. They are rebuildable from the code that produces them, given the database.

This hierarchy is not merely conceptual. It is operational. Backup strategy, recovery procedures, and change management are calibrated to the level of authority each component holds. The archive is backed up with the discipline of primary data; the database with the discipline of derived data; the website with the discipline of deployment artefacts.

User data in the `accounts` schema sits outside this hierarchy. It is authoritative in its own right — not derived from anything else — and is backed up with the discipline its authority requires. This is one of the reasons the `archive` and `accounts` schemas are kept separate.

## What this architecture does not specify

Three classes of decisions are deliberately left to the repositories that make them.

**Implementation choices within a layer.** The specific database migration tool, the web framework, the templating engine, the testing approach — these are decided by the repository that owns the layer and recorded in that repository's ADRs where they are material.

**The internal structure of a layer.** The directory layout of the platform's application code, the module boundaries within the sync layer, the pattern for organising views — these are implementation concerns, not architectural ones.

**The technology of future layers.** If and when the public API, a mobile client, or a new collector is introduced, the technology used for it is decided at that point, informed by what has been learned by then.

This document captures what must be true across repositories. Everything else is the repositories' own concern.

## Evolution

The architecture will change. New collectors will be added. The platform will grow features that stress its current shape. The public API will eventually be introduced. Future versions of the archive contract will supersede the current one.

This document is versioned with the `governance` repository. Material changes to the architecture are made deliberately, captured in ADRs in [`decisions/`](decisions/), and reflected here. The document is the current description of the architecture; the ADRs are the record of how it got here.
