# Azure Networking Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended best practices for designing, securing, operating, and troubleshooting Azure networking services, including Virtual Networks, Network Security, Hybrid Connectivity, and Load Balancing.

---

# Overview

Networking is one of the most important domains of Azure administration.

Well-designed networks improve:

- Security
- Availability
- Scalability
- Performance
- Operational simplicity

Microsoft recommends building Azure networks using layered security, centralized management, and standardized architectures.

---

# Plan IP Addressing Before Deployment

Network redesign is significantly more complex than network expansion.

Recommendations:

- Use RFC1918 private address ranges.
- Avoid overlapping CIDR blocks.
- Reserve address space for future growth.
- Separate environments into dedicated subnets.
- Document every address range.

Proper planning greatly simplifies future peering and hybrid connectivity.

---

# Design Around Hub-and-Spoke

For medium and large environments, Microsoft recommends a Hub-and-Spoke topology.

Typical Hub resources:

- Azure Firewall
- VPN Gateway
- ExpressRoute Gateway
- Azure Bastion
- Shared DNS
- Private DNS Zones

Typical Spokes:

- Production
- Development
- Testing
- Databases
- Shared services

Centralizing shared networking services reduces complexity and operational costs.

---

# Apply Least Privilege at the Network Layer

Do not rely on broad network access.

Recommendations:

- Deny unnecessary inbound traffic.
- Restrict outbound traffic where appropriate.
- Use Network Security Groups for segmentation.
- Apply Azure Firewall for centralized filtering.
- Protect administrative access with Azure Bastion.
- Use Just-In-Time VM Access where possible.

Network segmentation should complement identity-based security.

---

# Prefer Private Connectivity

Whenever possible, avoid exposing Azure resources to the Internet.

Microsoft recommends:

- Private Endpoints
- Private DNS Zones
- Azure Bastion
- Internal Load Balancers

Avoid Public IP addresses unless they are required.

Private connectivity reduces the attack surface.

---

# Use the Right Connectivity Service

Choose the networking service based on workload requirements.

| Requirement | Recommended Service |
|------------|----------------------|
| Internal communication | VNet Peering |
| Remote users | Point-to-Site VPN |
| Branch offices | Site-to-Site VPN |
| Enterprise hybrid connectivity | ExpressRoute |
| Public web applications | Application Gateway |
| TCP/UDP traffic | Azure Load Balancer |

Avoid deploying services that exceed business requirements.

---

# Secure Hybrid Networking

Hybrid connectivity should be resilient and secure.

Recommendations:

- Prefer Generation 2 VPN Gateways.
- Use zone-redundant gateway SKUs when available.
- Enable BGP whenever possible.
- Deploy redundant VPN devices on-premises.
- Test failover procedures regularly.
- Size GatewaySubnet appropriately.

Never depend on a single network path.

---

# Build Highly Available Networks

High availability should exist at every networking layer.

Recommendations:

- Deploy resources across Availability Zones.
- Use multiple backend instances.
- Configure Health Probes.
- Use Standard SKU networking resources.
- Design redundant routing paths.

Eliminate single points of failure.

---

# Optimize Routing

Keep routing simple and predictable.

Recommendations:

- Minimize User-Defined Routes.
- Document custom routes.
- Verify Effective Routes after changes.
- Use Azure Firewall instead of complex UDR chains when possible.
- Avoid unnecessary forced tunneling.

Simple routing reduces operational risk.

---

# Secure Public Applications

Internet-facing applications require additional protection.

Recommendations:

- Use Application Gateway with WAF.
- Enable HTTPS only.
- Keep TLS policies updated.
- Redirect HTTP to HTTPS.
- Deploy Azure DDoS Network Protection when appropriate.

Never expose production workloads without proper security controls.

---

# Use Explicit Outbound Connectivity

Production workloads should not depend on implicit outbound Internet access.

Preferred outbound solutions:

- Azure NAT Gateway
- Azure Firewall
- Standard Load Balancer Outbound Rules

Explicit outbound connectivity improves predictability and scalability.

---

# Monitor Continuously

Networking problems should be detected before users are affected.

Recommended monitoring services:

- Azure Monitor
- Network Watcher
- Connection Monitor
- Connection Troubleshoot
- IP Flow Verify
- NSG Flow Logs
- Azure Firewall Logs
- Activity Log

Configure alerts for:

- Gateway failures
- Health Probe failures
- BGP session loss
- Peering disconnects
- High latency
- Packet loss

---

# Governance

Maintain consistent governance across networking resources.

Recommendations:

- Standardize naming conventions.
- Apply Tags consistently.
- Protect critical resources with Resource Locks.
- Use Azure Policy.
- Review NSG rules regularly.
- Audit Public IP addresses.
- Remove unused networking resources.

Operational consistency improves long-term maintainability.

---

# Cost Optimization

Networking services can generate significant costs.

Recommendations:

- Delete unused Public IP addresses.
- Remove obsolete VPN Gateways.
- Remove unused peerings.
- Share Gateways using Gateway Transit.
- Use Internal Load Balancers whenever possible.
- Review Azure Advisor recommendations.
- Monitor data transfer costs across regions.

---

# Enterprise Scenario

A multinational organization deploys:

Hub:

- Azure Firewall Premium
- Azure Bastion
- ExpressRoute Gateway
- VPN Gateway
- Shared DNS

Spokes:

- Production
- Development
- Analytics
- Shared Services

Application traffic:

- Application Gateway with WAF
- Azure Load Balancer
- Virtual Machine Scale Sets

Private PaaS access:

- Private Endpoints
- Private DNS Zones

Operations:

- Azure Monitor
- Network Watcher
- Azure Policy
- Azure Advisor

The environment provides centralized management, private connectivity, layered security, and high availability.

---

# Best Practices Checklist

- Plan IP ranges before deployment.
- Avoid overlapping address spaces.
- Use Hub-and-Spoke architecture.
- Deploy Standard SKU networking resources.
- Prefer Private Endpoints over public access.
- Protect public applications with WAF.
- Use Azure Bastion for administration.
- Use Azure Firewall for centralized filtering.
- Deploy redundant gateways.
- Enable BGP where supported.
- Configure Health Probes correctly.
- Use Azure NAT Gateway for outbound Internet access.
- Monitor networking continuously.
- Review security rules regularly.
- Document networking architecture.

---

# Common Pitfalls

- Overlapping address spaces.
- Deploying resources in reserved subnets.
- Assuming VNet Peering is transitive.
- Forgetting Health Probes.
- Using Basic networking SKUs.
- Exposing unnecessary Public IP addresses.
- Depending on implicit outbound Internet access.
- Ignoring DNS configuration.
- Forgetting Gateway Transit requirements.
- Not monitoring networking resources.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Virtual Networks
> - Subnets
> - Network Security Groups
> - Azure Firewall
> - Azure Bastion
> - Private Endpoints
> - VPN Gateway
> - ExpressRoute
> - VNet Peering
> - Azure Load Balancer
> - Application Gateway
> - Network Watcher
> - Azure NAT Gateway
> - High Availability
> - Networking best practices

---

# Key Takeaways

- Azure networking should be designed around security, scalability, simplicity, and resilience rather than immediate requirements.
- Hub-and-Spoke architecture, private connectivity, and layered network security are Microsoft's recommended design patterns for enterprise environments.
- Standard SKU networking resources, Health Probes, explicit outbound connectivity, and continuous monitoring improve reliability and operational stability.
- Proper IP planning, DNS configuration, routing, and governance significantly reduce troubleshooting complexity.
- Following Microsoft's networking best practices results in secure, highly available, and production-ready Azure infrastructures.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Virtual Network documentation | https://learn.microsoft.com/azure/virtual-network/ |
| Azure Networking documentation | https://learn.microsoft.com/azure/networking/ |
| Azure Network Security documentation | https://learn.microsoft.com/azure/security/fundamentals/network-overview |
| Azure VPN Gateway documentation | https://learn.microsoft.com/azure/vpn-gateway/ |
| Azure ExpressRoute documentation | https://learn.microsoft.com/azure/expressroute/ |
| Azure Load Balancer documentation | https://learn.microsoft.com/azure/load-balancer/ |
| Azure Application Gateway documentation | https://learn.microsoft.com/azure/application-gateway/ |
| Azure Firewall documentation | https://learn.microsoft.com/azure/firewall/ |
| Azure Network Watcher documentation | https://learn.microsoft.com/azure/network-watcher/ |
| Azure Well-Architected Framework – Networking | https://learn.microsoft.com/azure/well-architected/service-guides/virtual-network |
| Microsoft Learn – Azure networking learning path | https://learn.microsoft.com/training/paths/design-implement-microsoft-azure-networking-solutions-az-700/ |
