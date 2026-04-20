# 0008 — ADR location: repository-level and organisation-level

Status: Accepted
Date: 2026-04-20

## Context

Architecture Decision Records serve two distinct purposes. Some decisions are specific to a single codebase — a schema choice, an internal layering rule, a library decision. Others apply across the whole project — repository naming, brand posture, compliance requirements. Mixing the two in one place obscures which decisions apply to which context.

## Decision

ADRs live in two places.

**Repository-level ADRs** live in `docs/decisions/` inside the repository they apply to. They document decisions specific to that codebase: architecture, implementation choices, internal conventions. They are read by anyone working in that repository.

**Organisation-level ADRs** live in `governance/decisions/`. They document decisions that apply across repositories: structural rules, cross-cutting principles, compliance, brand.

Each ADR records a single decision. ADRs are dated and immutable. A decision that is later reversed is recorded in a new ADR that supersedes the original. The original is marked superseded but is not edited. The history is legible at every point.

Every repository's `CLAUDE.md` references `governance/decisions` as a source of cross-cutting rules that apply to its work.

## Consequences

Every future decision has an obvious home. A reader looking for a cross-cutting rule finds it in governance; a reader looking for a repository-specific decision finds it in the repository.

Org-level decisions that turn out to be repository-specific are migrated to the appropriate repository's ADRs, with a superseding ADR in governance that records the relocation. Repository-specific decisions that turn out to be cross-cutting are migrated upward in the same way.

The numbering is independent between governance and each repository. `governance/decisions/0001` and `platform/docs/decisions/0001` are unrelated.
