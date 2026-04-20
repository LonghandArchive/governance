# 0007 — Personal data is redacted at the projection boundary

Status: Accepted
Date: 2026-04-20

## Context

The archive retains full, unredacted captures of public sector sources, including personal data that appeared in the original publication — hiring manager names, contact email addresses, direct phone numbers. Such personal data was originally published with a specific and time-limited purpose, typically the acceptance of applications. Once that purpose expires, a permanent public archive that continues to display the personal data indefinitely is on weak ground under UK GDPR, even though the original publication was lawful.

The Open Government Licence does not cover personal data, and UK GDPR applies to the project as a controller once it republishes the data in a new form.

The project has chosen a strategy that preserves archival integrity without re-publishing personal data: the raw archive is retained in full; personal data is redacted when the archive is projected into any queryable or publicly visible form.

## Decision

Personal data is redacted at the boundary between the archive and any derived view of it. The archive itself retains the unredacted record as the authoritative source. No surface that reaches the public — database projection, website, API, export — carries the personal data.

The redaction is applied by the projection or sync layer, not by the collector. Collectors produce complete, faithful captures; consumers are responsible for minimising what reaches the public.

The scope of redaction is defined at the projection layer and documented in the consuming repository. It includes, at minimum: named individuals in contact roles, direct personal email addresses, direct personal telephone numbers, and any other personal identifiers that the source publication included as points of contact.

A lightweight takedown process is maintained even in the absence of a legal obligation. A contact address is published on the public site's about page, and specific removal requests are honoured within a stated timeframe.

## Consequences

The archive remains the authoritative record and retains research value. Derived views are safer to publish and easier to defend under data protection obligations.

Every feature that touches job text, attachment text, or any other field that could contain personal data is tested against this rule before becoming public. Re-exposing redacted data through a new feature — a search endpoint that surfaces raw text, an export format that bypasses the projection — is a breach of this ADR and not merely a bug.

This ADR is cross-cutting because the principle applies to every future collector and every future projection, not only to the Civil Service Jobs collector and the current platform.
