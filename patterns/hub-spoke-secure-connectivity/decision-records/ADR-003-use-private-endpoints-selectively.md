# ADR-003: Use Private Endpoints Selectively

- **Status:** Proposed
- **Date:** 2026-07-31
- **Pattern:** AZ-EAP-001
- **Depends on:** ADR-001 and ADR-004

## Context

Azure Private Endpoints can provide private IP-based connectivity from a
virtual network to supported Azure services.

Private endpoints can reduce public network exposure, but they also introduce:

- Private DNS dependencies
- Additional network interfaces and IP consumption
- Lifecycle and ownership considerations
- Service-specific behavior
- Cross-subscription and cross-team coordination
- Monitoring and troubleshooting complexity

The pattern must avoid two extremes:

1. Exposing services publicly without justified controls.
2. Mandating private endpoints for every supported service without evaluating
   security, operational, cost, and technical requirements.

## Decision Drivers

- Minimize unnecessary public exposure
- Support private service access
- Preserve reliable DNS resolution
- Avoid uncontrolled complexity
- Maintain service ownership clarity
- Support workload-specific risk decisions
- Prevent automatic assumptions that private connectivity alone provides authorization

## Requirements Addressed

- DNS-001
- DNS-003
- SR-002
- SR-003
- SR-007
- OR-003
- PR-001
- CO-001

## Options Considered

### Option 1: Require Private Endpoints for Every Supported Service

**Advantages**

- Consistent private network access model
- Reduced reliance on public endpoints
- Strong alignment with restrictive network policies

**Disadvantages**

- Adds DNS and lifecycle complexity
- May provide limited benefit for some workloads
- Increases IP address and resource consumption
- Can complicate multi-region and cross-network access
- Requires service-specific implementation knowledge
- May increase operational support costs

### Option 2: Use Private Endpoints Selectively

Private endpoints are adopted when justified by data sensitivity, exposure
policy, regulatory requirements, threat analysis, or integration needs.

**Advantages**

- Aligns control strength with risk
- Avoids unnecessary complexity
- Supports workload-specific decisions
- Allows clear exception documentation
- Encourages explicit DNS and lifecycle planning

**Disadvantages**

- Requires assessment for each service or workload
- Produces a mixed connectivity model
- Governance must detect unjustified public exposure
- Documentation must clearly identify approved access paths

### Option 3: Use Public Endpoints with Service-Level Restrictions

Services retain public endpoints but use identity, firewall rules, service
endpoints, network ACLs, or application controls as applicable.

**Advantages**

- Simpler DNS behavior
- Fewer private network dependencies
- Potentially simpler cross-region access
- Lower private endpoint resource overhead

**Disadvantages**

- Publicly addressable service endpoint remains present
- Network restrictions may be service-specific
- Misconfiguration can increase exposure
- May not meet restrictive security or compliance requirements

## Decision

Use private endpoints **selectively**, based on documented criteria.

A private endpoint should be strongly considered when one or more of these
conditions apply:

- Public network access is prohibited by policy
- The service processes sensitive or regulated data
- Access must originate from approved private networks
- The threat model identifies public endpoint exposure as unacceptable
- Corporate or hybrid clients require private access
- Service-level public restrictions are insufficient
- The operational team can support the required DNS and lifecycle model

The decision must also evaluate:

- DNS-zone ownership
- Private endpoint ownership
- Subnet and IP capacity
- Cross-region access
- Failover behavior
- Monitoring
- Decommissioning
- Public-network-access configuration
- Service-specific limitations

## Rationale

A private endpoint is a connectivity mechanism, not a universal substitute for
identity, authorization, encryption, application security, or data protection.

Selective adoption ensures the pattern gains the security benefits of private
connectivity where they are material while retaining manageable operations.

## Consequences

### Positive Consequences

- Sensitive services can avoid unnecessary public exposure
- Private access paths become explicit
- Governance can evaluate public and private service access
- Workload teams must document DNS and lifecycle dependencies

### Negative Consequences

- A mixed connectivity model requires clear documentation
- DNS failures can make services unavailable
- Private endpoint records and connections require lifecycle management
- Cross-network access may require additional routing and DNS work
- Troubleshooting requires network and service expertise

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Incorrect DNS resolves the public endpoint | Medium | High | Central DNS standards and resolution testing |
| Public access remains enabled unintentionally | Medium | High | Policy, configuration review, and exposure monitoring |
| Private endpoint is deleted before DNS cleanup | Medium | Medium | Controlled decommissioning process |
| IP address exhaustion occurs | Low | High | Capacity planning and dedicated endpoint subnets where justified |
| Cross-region failover does not update access correctly | Medium | High | Document and test regional recovery behavior |

## Validation

- Resolve service names from approved Azure networks
- Resolve service names from approved corporate networks
- Confirm the resolved private IP address
- Validate permitted and denied access
- Confirm public-network-access policy
- Test private endpoint connection approval
- Test DNS record lifecycle
- Test service and regional failover behavior where applicable

## References

- Microsoft Azure Private Endpoint overview
- Microsoft Azure Private Endpoint DNS integration scenarios
- Microsoft Azure Architecture Center private-link hub-spoke guidance
