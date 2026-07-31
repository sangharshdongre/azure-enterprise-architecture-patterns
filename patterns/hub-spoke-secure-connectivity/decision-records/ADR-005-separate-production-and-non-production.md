# ADR-005: Separate Production and Non-Production Subscriptions and Networks

- **Status:** Proposed
- **Date:** 2026-07-31
- **Pattern:** AZ-EAP-001
- **Depends on:** ADR-001

## Context

The fictional organization operates production and non-production workloads
with different:

- Availability expectations
- Change controls
- Access requirements
- Data classifications
- Support responsibilities
- Cost-management objectives
- Risk tolerances

The architecture must prevent non-production failures, changes, identities,
and network policies from directly affecting production workloads.

## Decision Drivers

- Reduce production blast radius
- Enforce environment-specific governance
- Separate operational access
- Provide clear cost visibility
- Support distinct change-management processes
- Prevent accidental transitive connectivity
- Support environment-specific policy and monitoring

## Requirements Addressed

- BR-002
- CR-003
- RR-003
- GR-001
- SR-005
- OR-003
- CO-001

## Options Considered

### Option 1: Separate Subscriptions and Spoke Networks

Production and non-production workloads use distinct subscriptions and
virtual networks.

**Advantages**

- Clear governance and ownership boundaries
- Smaller failure and change blast radius
- Separate policy and access assignments
- Improved cost reporting
- Easier environment-specific monitoring
- Reduced risk of accidental network overlap

**Disadvantages**

- More subscriptions and network objects to manage
- Requires standardized automation
- Shared-service access must be deliberately configured
- Cross-environment testing paths need controlled exceptions

### Option 2: Shared Subscription with Separate Virtual Networks

Production and non-production use different networks but share a subscription.

**Advantages**

- Fewer subscriptions
- Potentially simpler initial administration
- Network separation remains possible

**Disadvantages**

- Policy, role, quota, and cost boundaries are weaker
- Subscription-level changes can affect both environments
- Access-control assignments become more complex
- Resource organization can become difficult at scale

### Option 3: Shared Subscription and Shared Virtual Network

Environment separation relies primarily on subnets and resource groups.

**Advantages**

- Lowest initial administrative overhead
- Simple for very small environments

**Disadvantages**

- Weak failure and governance boundaries
- Higher risk of accidental connectivity
- Shared quotas and policies
- Complex least-privilege administration
- Poor fit for enterprise production workloads

## Decision

Separate production and non-production workloads using:

- Distinct Azure subscriptions
- Distinct spoke virtual networks
- Distinct access-control assignments
- Environment-specific policy and monitoring
- Denied inter-environment communication by default
- Approved, documented exceptions for required integration or testing

Shared hub services may support both environments only when:

- The shared dependency is explicitly accepted
- Access is segmented
- Capacity is validated
- Failure impact is understood
- Operational ownership is documented

Separate hubs may be required where security, regulation, availability, or
organizational boundaries justify stronger isolation.

## Rationale

Subscription and network separation provides clearer governance, ownership,
cost, access, and failure boundaries than resource-group or subnet separation
alone.

It also supports repeatable workload onboarding and environment-specific
change controls.

## Consequences

### Positive Consequences

- Production has stronger isolation from non-production changes
- Governance and access can differ by environment
- Costs are easier to attribute
- Routing and firewall rules can be reviewed by environment
- Environment decommissioning is simpler

### Negative Consequences

- More subscriptions and networks must be managed
- Automation becomes essential
- Shared services require explicit access design
- Testing production-like integrations may require approved temporary paths
- IP address planning must cover separate environments

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Shared hub creates a common failure dependency | Medium | High | Validate availability and consider separate hubs where required |
| Non-production gains unintended production access | Medium | High | Deny by default, validate routes, and review firewall policy |
| Subscription sprawl becomes difficult to manage | Medium | Medium | Standardized vending, naming, tagging, and lifecycle controls |
| Duplicated services increase costs | Medium | Medium | Centralize only justified shared services |
| Testing requires unsafe production connectivity | Medium | High | Use controlled test data, approved interfaces, and temporary exceptions |

## Validation

- Confirm subscriptions and networks are distinct
- Verify production and non-production address spaces do not overlap
- Test that cross-environment traffic is denied by default
- Review role assignments and policy scope
- Verify environment-specific diagnostics
- Confirm cost attribution
- Test approved exception expiration and removal
