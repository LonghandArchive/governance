# 0010 — The project builds for its own purpose

Status: Accepted
Date: 2026-04-20

## Context

The Longhand Archive is a public-interest project. Its architecture, brand, and editorial posture are calibrated to that purpose: independent, non-endorsed, observational, free to use, with data and documentation under open licences. These properties are what make the project credible as a public resource.

The risk addressed by this decision is drift. Without an explicit rule, the project can accumulate features, infrastructure, and design decisions that serve an external interest rather than its stated purpose. Each individual accommodation will seem reasonable in isolation. The cumulative effect would compromise the project's independence, complicate its licensing position, and produce a codebase whose purpose is ambiguous even to its author.

External interests include — but are not limited to — an employer's priorities, a commercial product built by the author or others, a specific consumer's needs, or a partnership that would constrain the project's editorial or architectural independence.

## Decision

The project builds for its own purpose and does not accommodate the needs of any specific external consumer or interest.

**Purpose-driven work only.** Every feature, data capture, design decision, and infrastructure choice is justified by the project's own goals: archiving UK public sector data, deriving intelligence from that archive, and documenting how the system is built. Work whose primary justification is to serve an external interest is declined on that basis.

**External consumers use public interfaces.** When the project offers public interfaces — a website, a public API, published datasets — any external consumer may use them on the same terms as any other. No consumer receives privileged access, bespoke features, or architectural accommodations. The project does not design its interfaces around the requirements of a specific consumer.

**No organisational entanglement.** The project does not share its name, brand, codebase, infrastructure, or GitHub organisation with any external product, service, or venture. If a separate project builds on what The Longhand Archive publishes, it does so as an independent entity using public interfaces — not as an extension of this project.

**Independence is structural, not nominal.** The separation is enforced through architecture (collectors unaware of consumers, archive contract as the only interface, public API treating all consumers equally) and through governance (this ADR, the brand posture in ADR 0005, the contribution posture). It is not maintained by good intentions alone.

## Consequences

Proposed work is tested against this rule. A feature whose primary justification is "this would also help [external interest]" is declined. A reasonable variant of the work that serves the project on its own terms is acceptable; the external framing is not.

This rule is cross-cutting. It applies to the platform (no features designed for a specific consumer's needs), to collectors (no data captured to serve an external use case), to governance (no principles or patterns designed around external considerations), and to public-facing content (no framing that suggests the project is a route into something else).

The rule does not prevent external parties from using what the project publishes. The public API, when it exists, is designed to be useful to anyone. The distinction is between building something useful that others can consume and building something to serve a specific other's needs.

If this rule needs revisiting, the reconsideration is captured as a new ADR that supersedes this one. Until that happens, this ADR is the current rule.
