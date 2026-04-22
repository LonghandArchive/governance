# 0010 — The project builds for its own purpose

Status: Accepted
Date: 2026-04-20

## Context

The Longhand Archive is a public-interest project. Its architecture, brand, and editorial posture are calibrated to that purpose: independent, non-endorsed, observational, free to use, with data and documentation under open licences. These properties are what make the project credible as a public resource.

The risk is drift. Without an explicit rule, the project accumulates features, infrastructure, and design decisions that serve an external interest rather than its stated purpose. Each accommodation seems reasonable in isolation. The cumulative effect compromises independence, complicates licensing, and produces a codebase whose purpose is ambiguous even to its author.

## Decision

The project builds for its own purpose. Every feature, data capture, and design decision is justified by what the project exists to do: archive UK public sector data, derive intelligence from that archive, and document how the system is built. Work whose primary justification is to serve something outside that purpose is declined.

This applies regardless of the source of the external interest — an employer's priorities, another product, a specific consumer's requirements, a partnership that would constrain the project's independence. The test is the same: does this serve the project's own goals, or does it serve someone else's?

External consumers use public interfaces on the same terms as anyone else. No consumer gets privileged access, bespoke features, or architectural accommodations. The project does not share its name, brand, codebase, infrastructure, or GitHub organisation with any external product or service. These are not aspirational boundaries — they are enforced through the architecture: collectors unaware of consumers, the archive contract as the only interface, and this ADR as the standing rule.

## Consequences

Proposed work is tested against this rule. A feature whose primary justification is "this would also help [external interest]" is declined. A reasonable variant that serves the project on its own terms is acceptable; the external framing is not.

The rule applies to the platform, to collectors, to governance, and to public-facing content. No framing that suggests the project is a route into something else.

The rule does not prevent external parties from using what the project publishes. A stable public API, when it exists, is designed to be useful to anyone. The distinction is between building something useful that others happen to consume and building something to serve a specific other's needs.
