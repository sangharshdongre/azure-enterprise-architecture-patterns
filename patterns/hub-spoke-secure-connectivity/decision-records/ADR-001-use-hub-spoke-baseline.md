# ADR-001: Use Hub-Spoke as the Baseline Network Topology

- **Status:** Proposed
- **Date:** 2026-07-31
- **Pattern:** AZ-EAP-001
- **Decision owners:** Repository maintainers
- **Review cycle:** Review during each major pattern revision

## Context

The fictional organization requires a repeatable Azure network foundation for
multiple production and non-production workloads.

The platform must separate shared connectivity services from application
workloads while supporting:

- Hybrid connectivity
- Centralized network governance
- Controlled routing
- Shared DNS services
- Selected traffic inspection
- Independent workload subscriptions
- Future regional expansion

A baseline topology is required before detailed routing, security, DNS, and
operational decisions can be completed.

## Decision Drivers

- Separate shared platform connectivity from workload resources
- Support multiple workload subscriptions
- Establish clear platform and workload ownership boundaries
- Enable controlled hybrid connectivity
- Support centralized shared services
- Avoid uncontrolled network transit
- Enable repeatable workload onboarding
- Preserve the option for regional expansion

## Requirements Addressed

- BR-001
- BR-003
- CR-001
- CR-002
- CR-006
- CR-008
- GR-001
- OR-005

## Options Considered

### Option 1: Customer-Managed Hub-Spoke

A centrally operated hub virtual network provides shared connectivity
services. Workload virtual networks connect as spokes.

**Advantages**

- Clear separation between shared connectivity and workload resources
- Supports multiple subscriptions and workload teams
- Allows centralized control of selected routing and security services
- Provides an understandable onboarding model
- Can be extended to multiple regional hubs
- Offers direct control over hub components and routing behavior

**Disadvantages**

- The organization must operate the hub services
- Route configuration can become complex
- Central services can create dependencies and failure impact
- Multi-region expansion requires deliberate transit design
- Incorrect peering or routing configuration can create unintended paths

### Option 2: Azure Virtual WAN Managed Hub

Azure Virtual WAN provides Microsoft-managed hub and transit capabilities.

**Advantages**

- Managed transit architecture
- Strong fit for large-scale branch and regional connectivity
- Simplified connectivity across multiple hubs in suitable scenarios
- Integrated routing capabilities
- Reduced need to build some transit components manually

**Disadvantages**

- Different cost and operating model
- Less direct control over some underlying hub behavior
- Migration from an existing customer-managed hub may require redesign
- May introduce unnecessary complexity for smaller environments
- Service and feature suitability must be validated against requirements

### Option 3: Full Mesh Virtual Network Peering

Each workload network is directly peered with other networks it needs to
reach.

**Advantages**

- Direct paths between selected networks
- Simple for a very small number of virtual networks
- No mandatory centralized transit point

**Disadvantages**

- Peering relationships grow rapidly as the environment expands
- Governance and routing become difficult to standardize
- Workload teams can become tightly coupled
- Shared hybrid connectivity becomes harder to control
- It provides a weak foundation for repeatable enterprise onboarding

### Option 4: Independent Isolated Networks

Each workload operates its own network and connectivity services.

**Advantages**

- Strong workload autonomy
- Small failure blast radius between independent environments
- Workload teams can optimize for individual needs

**Disadvantages**

- Duplicates gateways, DNS, security, and monitoring capabilities
- Increases cost and operational inconsistency
- Complicates hybrid connectivity
- Makes enterprise-wide policy enforcement more difficult
- Reduces reuse of established platform services

## Decision

Use a **customer-managed hub-spoke topology** as the baseline for
AZ-EAP-001.

The pattern will use:

- A shared connectivity subscription
- A regional hub virtual network
- Separate workload spoke virtual networks
- Virtual network peering between the hub and approved spokes
- Centralized shared connectivity services where justified
- Explicit routing and traffic-flow documentation
- Separate regional hubs when future regional requirements justify them

Azure Virtual WAN remains a credible alternative when branch scale, global
transit, managed routing, or multi-region connectivity requirements make it a
better fit.

## Rationale

Customer-managed hub-spoke provides an appropriate balance of:

- Workload isolation
- Central governance
- Shared-service reuse
- Routing control
- Operational transparency
- Incremental implementation

It supports the current fictional scenario without assuming the scale or
branch-connectivity requirements that would automatically justify Azure
Virtual WAN.

## Consequences

### Positive Consequences

- Platform services and application workloads have clear boundaries
- Workloads can be onboarded through a repeatable model
- Shared connectivity services can be governed centrally
- Production and non-production workloads can remain logically separated
- Routing and monitoring standards can be applied consistently

### Negative Consequences

- The platform team must operate the hub
- Hub failures or configuration errors can affect multiple workloads
- Route tables, peering settings, and gateway propagation require disciplined management
- Regional expansion requires a defined multi-hub strategy
- Centralization can increase organizational dependency on the platform team

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Hub failure affects multiple spokes | Medium | High | Design for required availability, monitor dependencies, and document recovery |
| Incorrect routing creates unintended traffic paths | Medium | High | Use Infrastructure as Code, route validation, and controlled changes |
| Hub becomes a performance bottleneck | Medium | High | Measure traffic, validate capacity, and avoid unnecessary transit |
| Operational ownership is unclear | Medium | Medium | Document a responsibility model and escalation paths |
| Topology becomes unsuitable at global scale | Medium | Medium | Reassess Azure Virtual WAN or multi-hub alternatives during expansion |

## Validation

The decision will be validated through:

- Context and logical architecture review
- Hub and spoke route analysis
- Approved and denied traffic-flow tests
- Hybrid connectivity tests
- Failure-domain analysis
- Capacity and latency assessment
- Operational ownership review
- Comparison with Azure Virtual WAN during regional expansion

## Exceptions

A workload may use an alternative topology when:

- It requires strict independent network ownership
- Regulatory boundaries prohibit shared connectivity
- Latency requirements make centralized transit unsuitable
- Azure Virtual WAN demonstrably better satisfies its connectivity requirements
- The exception has an owner, rationale, risk assessment, and review date

## References

- Microsoft Azure Architecture Center: Hub-spoke network topology
- Microsoft Azure Architecture Center: Hub-spoke using Azure Virtual WAN
