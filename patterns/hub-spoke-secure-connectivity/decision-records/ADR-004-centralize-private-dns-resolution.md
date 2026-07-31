# ADR-004: Centralize Private DNS Resolution and Governance

- **Status:** Proposed
- **Date:** 2026-07-31
- **Pattern:** AZ-EAP-001
- **Depends on:** ADR-001

## Context

The reference environment must resolve:

- Azure private endpoint names
- Corporate private names
- Azure-hosted internal application names
- Selected public names
- Names used across peered workload networks

DNS resolution must work consistently for Azure and approved corporate
clients.

Private endpoints make DNS especially important because clients must resolve
the service name to the intended private IP address.

## Decision Drivers

- Consistent private endpoint resolution
- Hybrid DNS support
- Clear zone ownership
- Reduced manual record management
- Support for multiple subscriptions and spokes
- Centralized governance with controlled delegation
- Observable and testable DNS paths

## Requirements Addressed

- DNS-001
- DNS-002
- DNS-003
- DNS-004
- DNS-005
- OR-003
- RR-004

## Options Considered

### Option 1: Centralized Private DNS Zones and Resolution Services

Private DNS zones and hybrid forwarding are governed through shared platform
services.

**Advantages**

- Consistent zone ownership
- Easier hybrid resolution governance
- Reduced duplication
- Standardized private endpoint integration
- Central monitoring and operational responsibility

**Disadvantages**

- Creates dependency on shared DNS services
- Platform-team changes can affect multiple workloads
- Delegation and automation require careful design
- Multi-region resilience requires deliberate planning

### Option 2: Workload-Owned DNS Zones

Each workload team owns the zones and records required by its services.

**Advantages**

- Workload autonomy
- Faster workload-specific changes
- Smaller administrative scope per team

**Disadvantages**

- Duplicate zones can create inconsistent resolution
- Hybrid integration becomes difficult
- Ownership and record lifecycle may be unclear
- Standards are harder to enforce
- Cross-workload access becomes more complex

### Option 3: Manual Corporate DNS Records

Private endpoint and Azure application records are manually created in
corporate DNS.

**Advantages**

- Uses an existing enterprise DNS platform
- Familiar operating model for traditional network teams

**Disadvantages**

- Record creation can become slow and error-prone
- Azure resource lifecycle and DNS lifecycle can diverge
- Automation is difficult
- Cloud and corporate ownership boundaries become unclear
- Manual records can remain after resources are removed

## Decision

Use a **centralized private DNS governance model** with controlled delegation.

The design will include:

- Centrally governed Azure Private DNS zones for shared private endpoint namespaces
- Documented links between zones and approved virtual networks
- Approved hybrid forwarding paths
- Automated record lifecycle where service integration supports it
- Workload delegation where ownership and isolation requirements justify it
- Monitoring and validation of critical DNS resolution paths
- A defined process for exceptions and custom internal namespaces

The detailed design will evaluate Azure DNS Private Resolver or another
approved resolution architecture without selecting an exact SKU at this stage.

## Rationale

Centralized governance reduces inconsistent private endpoint resolution and
provides a clearer model for hybrid DNS.

Controlled delegation preserves workload autonomy where required while
preventing uncontrolled duplication of common private-link zones.

## Consequences

### Positive Consequences

- Private endpoint resolution follows a consistent model
- Hybrid DNS paths can be documented centrally
- Ownership and incident response are clearer
- DNS configuration can be automated
- Duplicate-zone risks are reduced

### Negative Consequences

- DNS becomes a shared platform dependency
- Incorrect zone links can affect multiple workloads
- Central teams must support workload onboarding
- Multi-region resilience adds complexity
- Troubleshooting spans corporate and Azure DNS systems

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Shared DNS outage affects multiple workloads | Medium | High | Resilient design, monitoring, and tested recovery |
| Incorrect zone link causes resolution failure | Medium | High | Infrastructure as Code and automated validation |
| Duplicate private zones create inconsistent answers | Medium | High | Central governance and policy controls |
| Stale records remain after decommissioning | Medium | Medium | Automated lifecycle and periodic review |
| Corporate forwarding is misconfigured | Medium | High | End-to-end hybrid DNS tests and documented ownership |

## Validation

- Resolve approved private names from each spoke
- Resolve approved Azure names from corporate networks
- Resolve corporate private names from Azure workloads
- Confirm expected private endpoint IP addresses
- Test behavior when a DNS forwarding component is unavailable
- Validate record creation and deletion
- Review zone links and forwarding rules
- Verify logging and health monitoring

## References

- Microsoft Azure Private Endpoint DNS integration scenarios
- Microsoft Cloud Adoption Framework private-link DNS integration guidance
