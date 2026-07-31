# 🧠 Architecture Decisions

This document indexes the Architecture Decision Records for
**AZ-EAP-001: Secure Azure Hub-Spoke Connectivity**.

Architecture decisions are recorded separately so that each decision can be
reviewed, revised, superseded, or deprecated without obscuring the complete
pattern.

## Decision Status Definitions

| Status | Meaning |
|---|---|
| Proposed | The decision is under review and has not been accepted |
| Accepted | The decision is approved as the current pattern direction |
| Superseded | A newer ADR replaces the decision |
| Deprecated | The decision should not be used for new implementations |
| Rejected | The option was evaluated but not selected |

## Decision Register

| ADR | Decision | Status | Primary requirements |
|---|---|---|---|
| [ADR-001](decision-records/ADR-001-use-hub-spoke-baseline.md) | Use hub-spoke as the baseline network topology | Proposed | CR-001, CR-002, CR-006, CR-008 |
| [ADR-002](decision-records/ADR-002-centralize-selected-traffic-inspection.md) | Centralize selected traffic inspection | Proposed | CR-003, CR-004, SR-001, SR-005 |
| [ADR-003](decision-records/ADR-003-use-private-endpoints-selectively.md) | Use private endpoints selectively | Proposed | SR-002, SR-003, DNS-003 |
| [ADR-004](decision-records/ADR-004-centralize-private-dns-resolution.md) | Centralize private DNS resolution and governance | Proposed | DNS-001, DNS-002, DNS-003, DNS-004 |
| [ADR-005](decision-records/ADR-005-separate-production-and-non-production.md) | Separate production and non-production subscriptions and networks | Proposed | BR-002, RR-003, GR-001 |

## Decision Principles

The ADRs follow these principles:

- Requirements are defined before Azure products and SKUs
- Decisions must identify credible alternatives
- Centralization must provide measurable security, governance, or operational value
- Network controls complement identity, application, endpoint, and data controls
- Decisions must disclose cost, reliability, performance, and operational consequences
- Exceptions must be documented and reviewable
- Exact service SKUs remain outside the scope of this decision stage

## Decision Review

The ADRs remain **Proposed** until they have been reviewed together with:

- The context diagram
- The logical architecture diagram
- Traffic-flow documentation
- DNS resolution paths
- Security and reliability analysis
- Operational ownership
- Cost and capacity considerations

Acceptance of an ADR means it is the current direction of this reference
pattern. It does not automatically approve the decision for every production
environment.
