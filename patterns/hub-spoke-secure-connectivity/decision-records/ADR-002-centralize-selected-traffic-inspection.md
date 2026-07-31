# ADR-002: Centralize Selected Traffic Inspection

- **Status:** Proposed
- **Date:** 2026-07-31
- **Pattern:** AZ-EAP-001
- **Depends on:** ADR-001

## Context

The organization requires consistent network security controls without
forcing every traffic flow through a centralized inspection service
regardless of risk, latency, cost, or technical suitability.

Traffic categories include:

- Workload-to-internet
- Internet-to-application
- Corporate-to-Azure
- Azure-to-corporate
- Spoke-to-spoke
- Workload-to-Azure-PaaS
- Management and administrative traffic

The architecture must distinguish traffic that requires centralized
inspection from traffic that can be controlled using other mechanisms.

## Decision Drivers

- Enforce approved internet egress policy
- Control communication between trust boundaries
- Centralize security-relevant logging
- Avoid unnecessary latency and transit
- Prevent inspection services from becoming an unjustified bottleneck
- Apply layered security controls
- Support documented exceptions

## Requirements Addressed

- CR-003
- CR-004
- CR-005
- SR-001
- SR-005
- SR-006
- PR-001
- PR-004
- CO-005

## Options Considered

### Option 1: Inspect All Traffic Centrally

All possible inbound, outbound, inter-spoke, hybrid, and service traffic is
forced through a centralized firewall.

**Advantages**

- Consistent central policy location
- Broad centralized visibility
- Simplified conceptual security narrative

**Disadvantages**

- Creates latency and throughput dependencies
- Increases firewall processing and data costs
- Can produce asymmetric-routing problems
- May inspect traffic that is already adequately controlled elsewhere
- Expands the blast radius of firewall failures or configuration errors
- Can complicate private endpoint and platform-service traffic

### Option 2: Centralize Selected Traffic Inspection

Central inspection is applied based on traffic category, risk, policy, and
technical feasibility.

**Advantages**

- Focuses inspection on higher-value traffic paths
- Reduces unnecessary transit
- Supports risk-based control selection
- Allows workload-specific ingress designs
- Reduces avoidable cost and performance impact

**Disadvantages**

- Requires clearer traffic classification
- Policy is distributed across multiple control types
- Documentation and governance are more demanding
- Exceptions require disciplined review

### Option 3: Workload-Owned Inspection Only

Each workload team deploys and operates its own network inspection controls.

**Advantages**

- Workload autonomy
- Workload-specific policy
- Reduced central service dependency

**Disadvantages**

- Inconsistent implementation
- Duplicated services and cost
- Fragmented logging and monitoring
- Difficult enterprise governance
- Higher operational burden for application teams

## Decision

Use **centralized inspection selectively**, based on documented traffic
categories.

The baseline intent is:

| Traffic category | Baseline treatment |
|---|---|
| Workload-to-internet | Centralized egress control and inspection |
| Azure-to-corporate | Controlled through approved hybrid paths and security policy |
| Corporate-to-Azure | Controlled through approved hybrid paths and destination controls |
| Spoke-to-spoke | Denied by default; inspected when explicitly permitted and required |
| Internet-to-application | Use an approved workload-appropriate ingress service |
| Workload-to-private-endpoint | Evaluate direct routing, DNS, NSGs, service controls, and inspection requirements |
| Administrative access | Use approved privileged access methods and identity controls |

The final architecture will not assume that every packet must traverse one
central firewall.

## Rationale

Risk-based inspection better balances:

- Security
- Operational complexity
- Latency
- Availability
- Service limits
- Cost

Central inspection is valuable for controlled egress and selected trust-boundary
traffic, but forcing all traffic through it can create unnecessary dependencies
and obscure workload-specific requirements.

## Consequences

### Positive Consequences

- Higher-risk traffic receives consistent centralized controls
- Unnecessary transit can be avoided
- Firewall capacity can be planned against defined traffic categories
- Exceptions become explicit and reviewable
- Network inspection is treated as part of layered security

### Negative Consequences

- The architecture requires detailed traffic-flow documentation
- Multiple control planes may enforce different aspects of policy
- Workload onboarding must classify traffic correctly
- Monitoring must correlate firewall, platform, NSG, and application logs

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Traffic bypasses required inspection | Medium | High | Route validation, policy controls, and continuous monitoring |
| Central firewall becomes a bottleneck | Medium | High | Capacity planning, performance testing, and scaling review |
| Asymmetric routing disrupts connections | Medium | High | Document flow symmetry and validate effective routes |
| Policy is inconsistent across control types | Medium | Medium | Define ownership and policy-authority hierarchy |
| Logging costs grow unexpectedly | Medium | Medium | Filter, retain, and route logs based on security requirements |

## Validation

- Effective-route inspection
- Approved and denied flow testing
- Firewall log verification
- Latency and throughput testing
- Failure and maintenance testing
- Route-symmetry validation
- Exception-review process testing

## References

- Microsoft Azure Architecture Center: Hub-spoke network topology
- Microsoft Azure Firewall hub-spoke guidance
