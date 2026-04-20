# 0001 — New repositories require three tests

Status: Accepted
Date: 2026-04-20

## Context

The Longhand Archive is organised as a set of repositories under a single GitHub organisation. The pressure to create new repositories — for components, for documentation, for speculative future work — will recur. Without a principle for when a new repository is justified, the decision is made reactively each time, and the organisation tends to accumulate either too many repositories (fragmenting work that belongs together) or too few (concealing components that should evolve independently).

## Decision

A new repository is created only when three tests are met, not one or two.

**Independent evolution.** The component can meaningfully change without the other repositories changing. If a change in one forces a synchronous change in another in the same commit, they are coupled and belong together.

**Independent deployment or distribution.** The component runs on its own schedule, or is consumed by something other than the repository it sits next to.

**A distinct audience or consumer.** The component is opened, read, or used by someone different from the adjacent repositories — a different contributor, a different client system, a different researcher.

When all three tests pass, the repository is created. When any test fails, the component lives inside an existing repository until the triggers are genuinely met.

## Consequences

The default is consolidation. Components remain inside existing repositories unless separation is demonstrably earned. Extracting later, when the triggers fire, is treated as a normal evolution rather than as a cost to avoid.

Repositories are not created for speculative future work. An empty repository anticipating a future component is worse than no repository at all, because it signals commitment without progress.

The three tests also apply to extracting components from existing repositories. Splitting is evaluated against the same criteria as creating from scratch.
