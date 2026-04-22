# 0010 — Commercial venture separation

Status: Accepted
Date: 2026-04-20

## Context

The Longhand Archive is a public-interest project. Its architecture, brand, and editorial posture are calibrated to that purpose: independent, non-endorsed, observational, free to use, with data and documentation under open licences. These properties are what make the project credible as a public resource.

A separate commercial venture is anticipated — a product, likely aimed at individuals applying to the civil service or similar audiences, that would make use of related capabilities but serve a commercial purpose. The commercial venture is not yet defined in detail. Its eventual existence is known; its shape is not.

The risk addressed by this decision is drift. Without an explicit rule, the public project will accumulate features, infrastructure, and design decisions that anticipate or accommodate the commercial venture. Each individual accommodation will seem reasonable in isolation. The cumulative effect would compromise the public project's independence, complicate its licensing position, and produce a codebase whose purpose is ambiguous even to its author.

## Decision

The public project and any commercial venture are architecturally, organisationally, and operationally separate.

**Separate organisation.** The commercial venture does not live under `longhandarchive` on GitHub. When it comes into existence, it takes its own GitHub organisation with its own name. No commercial venture repositories sit alongside the public project's repositories.

**Separate brand.** The commercial venture does not use The Longhand Archive name, domain, visual identity, or social handles. It presents to users as its own product.

**Separate codebase.** The commercial venture does not share code with the public project. No shared libraries, no shared deployment pipelines, no shared configuration. If a pattern needs to exist in both, it is re-implemented, not extracted.

**Separate infrastructure.** The commercial venture does not share databases, VPS instances, object storage, or any other running infrastructure with the public project. Data flows between them — for example, the commercial venture consuming the public API — happen over the same public interfaces any other external consumer would use.

**Separate legal entity, if incorporated.** If the commercial venture is incorporated, it is a separate entity from the author's personal undertaking of the public project. Contracts, obligations, and liabilities of one do not attach to the other.

The public project does not build features, hold data, or accept constraints whose primary purpose is to serve an anticipated commercial venture. Capabilities that are genuinely useful to both — a stable public API, for example — are built for the public project's own purpose first; their availability to the commercial venture is incidental, not designed-in.

## Consequences

Proposed work in the public project is tested against this rule. A feature, a data capture, a design decision, or an infrastructure choice whose primary justification is "this would also help the commercial venture" is declined on that basis. A reasonable variant of the work that serves the public project on its own terms is acceptable; the commercial framing is not.

The rule applies symmetrically. The commercial venture, when it exists, will not be architected with expectations of access to the public project's infrastructure, codebase, or brand. It will consume public interfaces as an external party would.

This rule is cross-cutting. It applies to the platform (no features specific to commercial users, no account types anticipating commercial monetisation), to collectors (no data captured specifically to serve commercial use cases), to governance (no principles or patterns designed around commercial considerations), and to public-facing content (no framing that suggests the public project is a route into a commercial offer).

If at some future point the separation rule needs revisiting — for example, if operating the commercial venture as a genuinely distinct entity proves impractical — the reconsideration is captured as a new ADR that supersedes this one. Until that happens, this ADR is the rule.

This decision does not prevent the author from being publicly associated with both projects. The non-endorsement framing in ADR 0005 already requires the public project to identify the author as an individual undertaking the work in a personal capacity. The same individual can also pursue a separate commercial venture without compromising either project, provided the separation described here is maintained.
