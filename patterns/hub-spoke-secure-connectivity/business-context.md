# Business Context

## 🏢 Fictional Organization

**Organization:** Contoso Digital Services
**Industry:** Business and digital services
**Operating model:** Hybrid workforce with centralized corporate IT and
distributed application teams
**Primary Azure region:** Fictional and intentionally unspecified during the
definition stage

Contoso Digital Services is modernizing a portfolio of business applications
on Microsoft Azure.

The organization currently operates workloads owned by multiple application
teams. These workloads include internal applications, public-facing services,
integration components, databases, and selected Azure PaaS services.

The organization requires a consistent network foundation before additional
production workloads are introduced.

## 🎯 Business Drivers

The primary business drivers are:

1. **Security consistency**

   Workload teams must use approved connectivity and traffic-control patterns.

2. **Workload isolation**

   Production, non-production, and shared platform services must be separated.

3. **Operational visibility**

   Network diagnostics, security events, and connectivity health must be
   available to centralized operations teams.

4. **Scalable onboarding**

   New workload teams should be able to adopt an established connectivity
   model without redesigning the platform.

5. **Hybrid integration**

   Selected Azure workloads must communicate securely with corporate
   locations and approved private services.

6. **Reduced public exposure**

   Internal application components and supported Azure PaaS services should
   avoid unnecessary public network exposure.

7. **Regional extensibility**

   The organization expects future deployment into additional Azure regions.

## 👥 Stakeholders

| Stakeholder | Primary interests |
|---|---|
| Executive sponsor | Risk reduction, delivery confidence, and business continuity |
| Enterprise architecture | Alignment with organizational technology strategy |
| Cloud platform team | Shared services, standards, automation, and supportability |
| Network team | Routing, hybrid connectivity, DNS, and traffic inspection |
| Security team | Segmentation, monitoring, access control, and threat reduction |
| Application teams | Predictable onboarding and documented connectivity services |
| Operations team | Monitoring, incident response, diagnostics, and service ownership |
| Compliance and risk | Evidence of controls and traceable architecture decisions |
| Finance and FinOps | Shared-service cost visibility and sustainable consumption |

## 📦 Workload Categories

The reference scenario includes:

- Public-facing web applications
- Internal line-of-business applications
- Application integration services
- Data platforms
- Azure PaaS services
- Administrative and management services
- Production and non-production environments

The pattern does not assume that all workloads have identical requirements.

## 🔐 Security Context

The organization follows these high-level principles:

- Deny network communication unless explicitly required
- Minimize direct public exposure
- Use identity-based access controls wherever supported
- Inspect traffic according to risk and policy
- Centralize security-relevant logging
- Separate administrative, platform, and workload responsibilities
- Use private connectivity where it provides a justified security benefit
- Avoid treating network location as the only security control

## 🧑‍💻 Operating Model

The cloud platform team owns shared connectivity services.

Application teams own workload resources within their assigned subscriptions
and spoke networks.

The security and network teams define mandatory guardrails and approve
exceptions.

Responsibilities will be documented more precisely during the operational
design phase.

## 📏 Success Definition

The pattern is successful when it provides a documented and repeatable
foundation that allows workload teams to connect services without bypassing
approved security, DNS, routing, monitoring, and governance controls.
