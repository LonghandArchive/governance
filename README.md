# Governance

This repository contains cross-cutting decisions, principles, and architectural context for The Longhand Archive.

Repositories in this organisation make their own architectural and implementation decisions in their own `docs/decisions/` directories. The records here document what applies across repositories — the shape of the project as a whole, the decisions that shape how every repository operates, and the principles that guide how the project is run.

## What lives here

**`architecture.md`** — the authoritative description of how The Longhand Archive is structured, including the seven architectural layers and the boundaries between them. Referenced by every repository's `CLAUDE.md` as the source of truth for cross-cutting architectural context.

**`principles.md`** — a short statement of how the project operates. The rules the project holds itself to, written for reading rather than reference.

**`decisions/`** — Architecture Decision Records for cross-cutting decisions, numbered sequentially. Each ADR records a single decision: the context that made it necessary, the decision itself, and the consequences that follow.

## How to read an ADR

ADRs are dated and immutable. A decision that is later reversed is recorded in a new ADR that supersedes the original; the original is marked superseded but is not edited. The history is always legible.

An ADR that applies across repositories lives here. An ADR that applies to a single repository lives in that repository's own `docs/decisions/` directory. See ADR 0008 for the rule.

## How to add an ADR

A new ADR is added when a cross-cutting decision is made that affects multiple repositories or the project as a whole. The next available number is used. The ADR is committed in the same change as any corresponding updates to affected repositories.

Decisions that apply to a single repository belong in that repository's own `docs/decisions/` directory, not here.

## How to change the architecture

`architecture.md` is updated when the shape of the project changes in a way that crosses repository boundaries — a new layer, a changed boundary between layers, a new relationship between components. Material changes are made deliberately, captured as ADRs in `decisions/`, and reflected in the document. The document describes the current architecture; the ADRs record how it got here.
