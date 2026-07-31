# Acceptance Criteria

These criteria define what must be demonstrated before AZ-EAP-001 can move
from **Draft** to **Reviewed** status.

## 📖 Documentation

| ID | Acceptance criterion |
|---|---|
| AC-001 | The business context, objectives, and stakeholders are documented. |
| AC-002 | Requirements are uniquely identified and prioritized. |
| AC-003 | Assumptions, constraints, and non-goals are explicitly documented. |
| AC-004 | Each architecture decision references the requirements it addresses. |
| AC-005 | Known limitations and credible alternatives are documented. |
| AC-006 | All external technical claims use authoritative references. |

## 🌐 Architecture

| ID | Acceptance criterion |
|---|---|
| AC-007 | A context diagram identifies Azure, corporate, internet, and operational boundaries. |
| AC-008 | A logical diagram identifies hub, spoke, subscription, and trust boundaries. |
| AC-009 | Important traffic flows are numbered and described. |
| AC-010 | Routing intent is documented for inbound, outbound, hybrid, inter-spoke, and private-service traffic. |
| AC-011 | DNS resolution paths are documented for Azure and corporate clients. |
| AC-012 | Platform and workload-team responsibilities are distinguishable. |

## 🔐 Security

| ID | Acceptance criterion |
|---|---|
| AC-013 | Public exposure points are explicitly identified. |
| AC-014 | Administrative access paths are documented. |
| AC-015 | Network-policy exceptions require documented approval. |
| AC-016 | Security-relevant logs and monitoring destinations are identified. |
| AC-017 | Private endpoint risks, DNS dependencies, and lifecycle considerations are documented. |
| AC-018 | Network controls are described as complementary to identity and application controls. |

## 🛡️ Reliability

| ID | Acceptance criterion |
|---|---|
| AC-019 | Critical connectivity dependencies are identified. |
| AC-020 | Potential single points of failure are identified and addressed or accepted. |
| AC-021 | Failure scenarios include expected impact, detection, and recovery action. |
| AC-022 | Availability assumptions are documented before service SKUs are selected. |
| AC-023 | Production and non-production failure domains are appropriately separated. |

## 📊 Operations

| ID | Acceptance criterion |
|---|---|
| AC-024 | Service ownership and support responsibilities are documented. |
| AC-025 | Monitoring and alerting requirements are traceable to critical dependencies. |
| AC-026 | Workload onboarding requirements are documented. |
| AC-027 | Change, exception, and decommissioning responsibilities are defined. |
| AC-028 | Operational dependencies on corporate services are identified. |

## 💰 Cost and Performance

| ID | Acceptance criterion |
|---|---|
| AC-029 | Major shared-service cost drivers are identified. |
| AC-030 | Logging and retention costs are included in the cost discussion. |
| AC-031 | Capacity-sensitive services are identified. |
| AC-032 | Latency and throughput-sensitive traffic flows are identified. |
| AC-033 | SKU selection is deferred until capacity and availability requirements are defined. |

## 🧪 Validation

| ID | Acceptance criterion |
|---|---|
| AC-034 | DNS resolution tests are defined. |
| AC-035 | Approved and denied traffic-flow tests are defined. |
| AC-036 | Hybrid connectivity failure tests are defined. |
| AC-037 | Monitoring and alert-delivery tests are defined. |
| AC-038 | Route-propagation and effective-route checks are defined. |
| AC-039 | No real customer, employer, tenant, subscription, IP, hostname, or credential information is present. |
| AC-040 | Markdown links, spelling, and document formatting have been reviewed. |

## Status Transition

The pattern may move to **Reviewed** when:

1. All definition documents are complete.
2. The architecture diagrams and decisions are available.
3. Security, reliability, operations, cost, and performance reviews are
   completed.
4. All mandatory acceptance criteria have supporting evidence.
5. No unresolved confidentiality or intellectual-property concerns remain.

Reviewed status does not mean that the pattern is automatically approved for
production use.
