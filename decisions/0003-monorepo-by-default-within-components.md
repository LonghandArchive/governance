# 0003 — Monorepo by default within components

Status: Accepted
Date: 2026-04-20

## Context

Within a single component — the platform application, for example — there is a recurring temptation to separate concerns into distinct repositories. The web front end, the JSON endpoints, the database schema, the sync layer, the shared models: each can be framed as an independently meaningful thing that warrants its own home.

For a project of this size, with a single contributor, that temptation produces overhead disproportionate to the benefit. Coordinating changes across multiple repositories costs more than it saves when every change is cross-cutting.

## Decision

Within a single deployable component, all code lives in a single repository. The internal structure of the repository reflects architectural layers — sync, data access, application, presentation — through directories, not repositories.

A component is split into separate repositories only when the criteria in ADR 0001 are met: independent evolution, independent deployment or distribution, and a distinct consumer. Internal layering does not meet these criteria.

The specific application of this rule to the platform repository: the database schema, the sync layer, the web application, the internal JSON endpoints, and the presentation layer all live in `platform`. They are layered inside the repository, not separated across repositories.

## Consequences

Cross-cutting changes are made in a single commit. Schema migrations, the application code that depends on them, and the tests that exercise them are versioned together. Version skew between components of a single application is impossible by construction.

The cost of extracting a layer into its own repository rises as the repository grows. This is an acceptable trade — the trigger for extraction is the three-test rule, not a desire to avoid future refactoring cost.

This ADR is repository-level in its targets but organisation-level in its principle. Component-level ADRs in specific repositories may reference this principle when they apply it.
