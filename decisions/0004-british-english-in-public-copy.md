# 0004 — British English in public copy

Status: Accepted
Date: 2026-04-20

## Context

The Longhand Archive is a UK-focused project about UK public sector data. The audience is predominantly British — civil servants, UK journalists, UK researchers, UK policy professionals. The project's voice is the author's own, which is British English.

Tooling defaults, dependency documentation, and AI-assisted drafting tend toward American English. Without a stated rule, public copy drifts toward inconsistency over time.

## Decision

All user-facing and publicly visible copy uses British English spelling and conventions. This includes:

- The public website's prose, labels, and error messages.
- README files in all repositories.
- ADRs, principles, and other content in `governance`.
- Public API documentation, when it exists.
- Social media copy written on behalf of the project.

Technical terms that are standardised in American English in their original context — variable names, library names, protocol terms — are not altered. `organization` as a JSON field name in an external standard remains `organization`. `organisation` as a word in English prose is spelt with an `s`.

## Consequences

The convention is consistent across every surface a reader encounters. New repositories, new documentation, and AI-assisted drafts are checked against this rule before being committed to the main branch.

This ADR applies to public copy. Internal code comments, commit messages, and working notes are not constrained by it, though consistency is preferred.
