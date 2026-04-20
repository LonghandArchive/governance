# Governance

This repository contains cross-cutting decisions and operating principles for The Longhand Archive.

Repositories in this organisation make their own architectural and implementation decisions in their own `docs/decisions/` directories. The records here document decisions that apply across repositories — naming conventions, structural rules, brand posture, compliance requirements, and other principles that shape how the project operates as a whole.

## Structure

- `principles.md` — a short statement of how the project operates.
- `decisions/` — Architecture Decision Records for cross-cutting decisions, numbered sequentially.

## How to read an ADR

Each ADR records a single decision: the context that made it necessary, the decision itself, and the consequences that follow. ADRs are dated and immutable. A decision that is later reversed is recorded in a new ADR that supersedes the original; the original is marked superseded but is not edited. The history is always legible.

## How to add an ADR

A new ADR is added when a cross-cutting decision is made that affects multiple repositories or the project as a whole. The next available number is used. The ADR is committed in the same change as any corresponding updates to affected repositories.

Decisions that apply to a single repository belong in that repository's own `docs/decisions/` directory, not here.
