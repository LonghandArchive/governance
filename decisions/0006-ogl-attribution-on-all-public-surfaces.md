# 0006 — OGL attribution on all public surfaces

Status: Accepted
Date: 2026-04-20

## Context

The Longhand Archive uses data published under the Open Government Licence v3.0. The licence is permissive — commercial and non-commercial use, adaptation, redistribution, and combination with other data are all permitted. In return, the licence requires attribution: the source must be acknowledged, and the attribution statement must be visible.

The risk is not deliberate omission; it is incremental drift. A new page, a new feed, a new export format, or a new API response added without considering attribution silently breaches the licence. A standing rule prevents this.

## Decision

Every public surface that presents data derived from an OGL source carries an attribution statement. The attribution statement is the standard OGL v3.0 form unless the source specifies otherwise:

> Contains public sector information licensed under the Open Government Licence v3.0.

The statement is accompanied by a link to the licence: `https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/`.

The requirement applies to:

- The public website's footer on every page that presents archive data.
- The dedicated attribution page listing all sources, linked from the footer.
- API responses that return derived data, with attribution included in the response envelope.
- Any dataset exports, with attribution in the accompanying documentation or metadata.
- Social media posts that quote or visualise data, where the format permits.

## Consequences

New surfaces added to the project are checked against this rule before becoming public. New data sources added to the archive are added to the attribution page as part of the same change.

This ADR is cross-cutting because OGL compliance is a property of the project as a whole, not of any single repository. Implementation details — how attribution is rendered in specific UI components, how the API envelope is structured — live in the repositories that implement them.
