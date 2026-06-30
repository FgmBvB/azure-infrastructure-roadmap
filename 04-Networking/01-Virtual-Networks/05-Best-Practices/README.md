# Azure Virtual Networks Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended best practices for designing, securing, scaling, and operating Azure Virtual Networks in production environments.

---

# Overview

A well-designed Virtual Network is the foundation of a secure, scalable, and maintainable Azure environment.

Poor network planning often results in complex migrations, routing conflicts, security issues, and unnecessary operational costs.

Microsoft recommends designing Virtual Networks with future growth, hybrid connectivity, and security in mind from the beginning.

---

# Network Design

Microsoft recommends:

- Plan address spaces before deploying resources.
- Allocate larger address spaces than currently required.
- Leave room for future expansion.
- Avoid overlapping address ranges.
- Separate production, development, and testing environments.

Well-planned address spaces simplify future VPN, ExpressRoute, and VNet Peering deployments.

---

# Subnet Design

Organize workloads into dedicated subnets.

Example:

```text
Virtual Network

├── GatewaySubnet
├── AzureFirewallSubnet
├── Frontend
├── Backend
├── Database
├── Management
└── Private Endpoints
```

Benefits include:

- Better security boundaries.
- Simpler administration.
- Easier troubleshooting.
- Granular routing policies.
- Independent Network Security Groups.

Avoid deploying unrelated workloads inside the same subnet.

---

# IP Address Planning

Follow these recommendations:

- Use RFC1918 private address ranges.
- Avoid overlapping CIDR blocks.
- Consider future hybrid connectivity.
- Reserve address space for additional subnets.
- Document every allocated range.

Remember that Azure reserves five IP addresses in every subnet.

---

# Public IP Addresses

Expose Public IP addresses only when required.

Whenever possible:

- Use Private IP addresses.
- Publish applications through Load Balancers or Application Gateway.
- Protect Internet-facing workloads with Azure Firewall or Web Application Firewall (WAF).

Use **Standard SKU Public IPs** for production deployments.

---

# DNS

Microsoft recommends:

- Use Azure-provided DNS for simple environments.
- Deploy redundant Custom DNS Servers when required.
- Use Private DNS Zones with Private Endpoints.
- Avoid exposing internal namespaces publicly.
- Document DNS architecture and forwarding rules.

---

# Routing

Use Azure System Routes unless custom routing is necessary.

When using User-Defined Routes:

- Keep routing tables simple.
- Avoid unnecessary route entries.
- Document every custom route.
- Validate routing after changes.
- Use Effective Routes during troubleshooting.

---

# Security

Apply Zero Trust networking principles.

Recommendations:

- Minimize Public IP exposure.
- Use Network Security Groups.
- Use Azure Firewall for centralized inspection.
- Use Private Endpoints whenever possible.
- Restrict administrative access.
- Apply least privilege.

Security should be layered rather than relying on a single control.

---

# Monitoring

Continuously monitor network health using:

- Azure Monitor
- Network Watcher
- Connection Monitor
- NSG Flow Logs
- Activity Log

Configure alerts for:

- Connectivity failures.
- Routing changes.
- Firewall events.
- VPN failures.
- DNS issues.

---

# High Availability

Design networks for resilience.

Recommendations:

- Deploy redundant VPN Gateways where appropriate.
- Use Availability Zones when supported.
- Use Standard SKU networking resources.
- Avoid single points of failure.
- Test failover procedures regularly.

---

# Governance

Establish consistent governance policies.

Recommendations:

- Standardize naming conventions.
- Use Tags consistently.
- Apply Azure Policy.
- Protect critical resources using Resource Locks.
- Review network configurations periodically.

---

# Cost Optimization

Reduce networking costs by:

- Removing unused Public IP addresses.
- Deleting unused Network Interfaces.
- Removing unused Route Tables.
- Cleaning up orphaned NSGs.
- Monitoring data transfer costs.
- Reviewing Azure Advisor recommendations.

---

# Enterprise Scenario

A multinational company deploys a Hub-and-Spoke architecture.

The Hub Virtual Network contains:

- Azure Firewall
- VPN Gateway
- Shared DNS services

Each business unit is deployed into its own Spoke Virtual Network with dedicated subnets, Private Endpoints, and Network Security Groups.

This architecture provides centralized security while allowing independent workload management.

---

# Best Practices Checklist

- Plan address spaces before deployment.
- Avoid overlapping networks.
- Separate workloads into dedicated subnets.
- Use Private IPs whenever possible.
- Minimize Public IP exposure.
- Use Standard SKU networking resources.
- Protect workloads using NSGs and Azure Firewall.
- Use Private Endpoints for Azure PaaS services.
- Monitor network health continuously.
- Document network architecture.

---

# Common Pitfalls

- Overlapping address spaces.
- Flat network designs.
- Excessive Public IP exposure.
- Missing Network Security Groups.
- Poor subnet planning.
- Unnecessary User-Defined Routes.
- Ignoring Azure reserved IP addresses.
- Lack of DNS redundancy.
- No monitoring or alerting.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Address planning
> - CIDR design
> - Subnet segmentation
> - Azure DNS
> - Route Tables
> - User-Defined Routes
> - Public vs Private IPs
> - Azure networking best practices
> - Security recommendations
> - Hybrid network planning

---

# Key Takeaways

- Careful Virtual Network design simplifies future growth, hybrid connectivity, and operational management.
- Proper subnet segmentation improves security, scalability, and troubleshooting.
- Private networking should always be preferred over direct Internet exposure.
- Standardized governance, monitoring, and documentation are essential for production environments.
- Following Microsoft's networking best practices results in more secure, resilient, and maintainable Azure infrastructures.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Virtual Network best practices | https://learn.microsoft.com/azure/virtual-network/concepts-and-best-practices |
| Azure networking fundamentals | https://learn.microsoft.com/azure/networking/fundamentals/networking-overview |
| Azure Virtual Network overview | https://learn.microsoft.com/azure/virtual-network/virtual-networks-overview |
| Azure route tables | https://learn.microsoft.com/azure/virtual-network/manage-route-table |
| Azure DNS | https://learn.microsoft.com/azure/dns/ |
| Azure Private DNS | https://learn.microsoft.com/azure/dns/private-dns-overview |
| Azure Network Watcher | https://learn.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview |
| Azure Well-Architected Framework – Networking | https://learn.microsoft.com/azure/well-architected/service-guides/virtual-network |
| Microsoft Learn – Configure virtual networks | https://learn.microsoft.com/training/modules/configure-virtual-networks/ |
