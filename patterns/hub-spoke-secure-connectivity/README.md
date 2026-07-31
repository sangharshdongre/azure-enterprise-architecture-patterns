# 🌐 AZ-EAP-001: Secure Azure Hub-Spoke Connectivity

## Status

**Draft — definition in progress**

## Summary

This pattern defines a secure Azure hub-spoke connectivity foundation for a
fictional enterprise operating multiple production and non-production
workloads.

The design centralizes shared connectivity services while allowing workload
teams to operate separate spoke networks and subscriptions within established
security and governance boundaries.

## 🎯 Objectives

The pattern is intended to:

- Separate shared platform services from application workloads
- Support production and non-production environment isolation
- Centralize approved network traffic inspection
- Support hybrid connectivity with corporate locations
- Provide centralized private DNS resolution
- Enable private access to selected Azure platform services
- Centralize network monitoring and diagnostic data
- Establish repeatable connectivity patterns for workload teams
- Support future regional expansion without redesigning the entire platform

## ✅ Suitable When

Use this pattern as a starting point when an organization requires:

- Multiple Azure workload subscriptions
- Shared hybrid connectivity services
- Centralized network security controls
- Controlled communication between workloads
- Private connectivity to selected Azure PaaS services
- Centralized private DNS resolution
- Separation between platform and workload ownership
- A repeatable enterprise connectivity foundation

## ⚠️ Reconsider or Adapt When

This pattern should be reassessed when:

- Azure Virtual WAN better matches global transit requirements
- The environment contains only one small and isolated workload
- Regulatory requirements mandate independently operated network platforms
- Centralized inspection introduces unacceptable latency or dependency
- Workload-owned network security is an explicit operating-model requirement
- The organization lacks the operational capability to manage centralized
  network services
- A fully managed application platform removes the need for customer-managed
  network transit

## 📖 Pattern Definition

| Area | Document |
|---|---|
| Business context and stakeholders | [business-context.md](business-context.md) |
| Requirements and priorities | [requirements.md](requirements.md) |
| Assumptions, constraints, and non-goals | [assumptions-and-constraints.md](assumptions-and-constraints.md) |
| Acceptance criteria | [acceptance-criteria.md](acceptance-criteria.md) |

## 🧭 Intended Architecture Scope

The future architecture will consider:

- A centralized connectivity subscription
- One or more hub virtual networks
- Production and non-production spokes
- Hybrid connectivity through ExpressRoute or site-to-site VPN
- Centralized traffic inspection
- Private DNS resolution
- Private endpoints for selected Azure PaaS services
- Centralized diagnostics and network monitoring
- Subscription and network-level workload separation

The exact Azure services, SKUs, availability configuration, and deployment
topology will be selected during the architecture decision and design phases.

## 🚫 Current Exclusions

This stage does not include:

- Architecture diagrams
- Detailed IP address planning
- Product SKU selection
- Terraform or Bicep
- Production deployment instructions
- Organization-specific compliance mappings
- Application architecture
- Detailed threat modeling
- Operational runbooks

## 📌 Pattern Identifier

```text
Pattern ID: AZ-EAP-001
Pattern name: Secure Azure Hub-Spoke Connectivity
Status: Draft
Scenario type: Fictional enterprise reference
