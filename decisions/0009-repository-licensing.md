# 0009 — Repository licensing: CC BY 4.0 for documentation, deferred for code

Status: Accepted
Date: 2026-04-20

## Context

Repositories in The Longhand Archive fall into two kinds. Documentation repositories — governance, archive-contract, the organisation profile — contain prose, specifications, and decision records. Code repositories — collectors and the platform — contain executable software.

These two kinds of content have different natural licensing families. Creative Commons licences are designed for written and creative work; open source software licences (MIT, Apache, GPL, AGPL) are designed for code. Using the wrong family produces awkward terms and unclear permissions.

Some repositories are currently private and will only need a licence when they are made public. The right time to decide a code repository's licence is when it is being prepared for publication, not in advance.

## Decision

Documentation repositories use Creative Commons Attribution 4.0 International (CC BY 4.0). This applies to all repositories whose content is primarily prose, specification, or decision-record material, including `governance`, `archive-contract`, and `.github`. The licence is added as a `LICENSE` file at the repository root.

Code repositories do not have a default licence. The licence for a code repository is chosen at the point the repository is made public, informed by its role in the project and by the state of any commercial considerations at that time. Until a code repository is public, it remains under default copyright and does not require a `LICENSE` file.

When a code repository is made public, the licence decision is captured as an ADR in that repository.

## Consequences

Documentation created in this organisation is reusable with attribution by default. Adoption of patterns, quotation of ADRs, and reuse of architectural framing are all permitted, which supports the project's public learning-log posture.

Code licensing decisions are deferred to a point where context is richer. The alternative — choosing code licences in advance — forces a decision before the information needed to make it well is available.

The two licence families are not mixed within a repository. A documentation repository does not contain open-source-licensed code; a code repository does not contain CC-licensed documentation. When a code repository contains substantive documentation, that documentation is covered by the code repository's licence unless separately noted.
