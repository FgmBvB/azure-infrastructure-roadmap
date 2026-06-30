# Azure Network Security Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended best practices for securing Azure networks using Network Security Groups, Azure Firewall, Private Endpoints, DDoS Protection, Azure Bastion, and Zero Trust principles.

---

# Overview

Network security should never rely on a single control.

Microsoft recommends implementing a **defense-in-depth** strategy that combines identity, network segmentation, traffic inspection, private connectivity, and continuous monitoring.

A properly designed Azure network minimizes the attack surface while maintaining operational flexibility and scalability.

---

# Adopt Zero Trust

Microsoft recommends applying Zero Trust networking principles throughout every Azure environment.

Core principles include:

- Verify every connection.
- Assume breach.
- Grant least-privilege access.
- Continuously monitor network activity.
- Minimize lateral movement.

Every network connection should be explicitly authorized.

---

# Minimize Public Exposure

Reduce Internet exposure whenever possible.

Recommendations:

- Avoid unnecessary Public IP addresses.
- Use Azure Bastion for administrative access.
- Prefer Private Endpoints for Azure PaaS services.
- Disable public network access when Private Endpoints are available.
- Restrict inbound traffic to approved sources.

The fewer Internet-facing resources, the smaller the attack surface.

---

# Segment Networks

Separate workloads into dedicated subnets.

Example:

```text
Virtual Network

├── AzureFirewallSubnet
├── AzureBastionSubnet
├── GatewaySubnet
├── Web
├── Application
├── Database
├── Management
└── Private Endpoints
```

Benefits include:

- Improved isolation.
- Granular Network Security Groups.
- Simplified routing.
- Reduced lateral movement.
- Easier troubleshooting.

---

# Apply Least Privilege Networking

Only allow required traffic.

Recommendations:

- Deny unnecessary inbound traffic.
- Restrict outbound traffic where appropriate.
- Avoid "Allow Any" rules.
- Open only required ports.
- Limit administrative access.

Least privilege applies to networking as well as identity.

---

# Use Network Security Groups Correctly

NSGs should be used for subnet and workload segmentation.

Recommendations:

- Associate NSGs with subnets whenever possible.
- Use NIC-level NSGs only when workload-specific filtering is required.
- Organize rules using Application Security Groups.
- Remove unused security rules.
- Review rule priorities regularly.

Avoid creating overly permissive rules.

---

# Centralize Traffic Inspection

Deploy Azure Firewall when centralized filtering is required.

Typical scenarios:

- Hub-and-Spoke architectures.
- Hybrid connectivity.
- Internet egress control.
- Regulatory compliance.
- Threat Intelligence inspection.

Use User-Defined Routes (UDRs) to direct traffic through Azure Firewall.

---

# Secure Azure PaaS Services

Microsoft recommends avoiding public access whenever possible.

Preferred approach:

```text
Virtual Machine

↓

Private Endpoint

↓

Private DNS Zone

↓

Azure Storage
```

Recommendations:

- Use Private Endpoints.
- Disable public network access.
- Use Private DNS Zones.
- Remove unnecessary Service Endpoints.
- Monitor Private Endpoint connections.

---

# Protect Internet-Facing Applications

For workloads exposed to the Internet:

- Enable Azure DDoS Network Protection where appropriate.
- Deploy Azure Firewall.
- Use Web Application Firewall (WAF) for web applications.
- Monitor firewall logs.
- Enable diagnostic logging.

Combine multiple security layers rather than relying on one service.

---

# Secure Administrative Access

Administrative access should never rely on permanently exposed Public IP addresses.

Microsoft recommends:

- Azure Bastion.
- Just-In-Time (JIT) VM Access (Microsoft Defender for Cloud).
- Multi-Factor Authentication (MFA).
- Microsoft Entra ID authentication where supported.
- Privileged Identity Management (PIM) for administrative roles.

---

# Monitor Continuously

Security requires continuous monitoring.

Use:

- Azure Monitor
- Network Watcher
- Activity Log
- Azure Firewall Logs
- NSG Flow Logs (where supported)
- Microsoft Defender for Cloud

Configure alerts for:

- Denied traffic.
- Firewall rule changes.
- DDoS attacks.
- Administrative changes.
- Unusual network activity.

---

# Governance

Implement consistent governance across networking resources.

Recommendations:

- Apply Azure Policy.
- Use Resource Locks for critical resources.
- Standardize naming conventions.
- Apply Tags consistently.
- Review firewall and NSG configurations regularly.
- Document routing and DNS architecture.

---

# Enterprise Scenario

A global organization deploys a Hub-and-Spoke architecture.

The Hub contains:

- Azure Firewall Premium
- Azure Bastion
- VPN Gateway
- Private DNS
- Azure DDoS Network Protection

Each Spoke Virtual Network contains:

- Dedicated application subnets
- Network Security Groups
- Private Endpoints
- User-Defined Routes

No production Virtual Machine has a Public IP address.

All Internet-bound traffic passes through Azure Firewall.

---

# Best Practices Checklist

- Plan network segmentation before deployment.
- Minimize Public IP usage.
- Use Private Endpoints whenever possible.
- Deploy Azure Firewall for centralized inspection.
- Apply Network Security Groups consistently.
- Use Application Security Groups to simplify rule management.
- Enable Azure DDoS Network Protection for critical Internet-facing workloads.
- Use Azure Bastion for VM administration.
- Monitor network security continuously.
- Review firewall and NSG rules regularly.
- Apply Zero Trust principles.
- Document all networking configurations.

---

# Common Pitfalls

- Exposing Virtual Machines directly to the Internet.
- Using broad NSG rules such as "Allow Any".
- Mixing unrelated workloads in the same subnet.
- Forgetting Private DNS when deploying Private Endpoints.
- Using Service Endpoints where Private Endpoints are more appropriate.
- Forgetting User-Defined Routes when deploying Azure Firewall.
- Not reviewing firewall rule order.
- Ignoring diagnostic logs and monitoring.
- Assuming NSGs replace Azure Firewall or vice versa.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Defense-in-depth
> - Zero Trust networking
> - Network segmentation
> - Network Security Groups
> - Application Security Groups
> - Azure Firewall
> - Private Endpoints
> - Azure Bastion
> - Azure DDoS Network Protection
> - Monitoring and governance best practices

---

# Key Takeaways

- Network security in Azure is built through multiple complementary layers rather than a single technology.
- Private connectivity, centralized inspection, and least-privilege networking significantly reduce the attack surface.
- Azure Firewall, NSGs, DDoS Protection, and Private Endpoints each address different security requirements.
- Continuous monitoring and governance are essential for maintaining a secure Azure environment.
- Following Microsoft's networking best practices results in more resilient, scalable, and secure cloud infrastructures.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure network security documentation | https://learn.microsoft.com/azure/security/fundamentals/network-overview |
| Microsoft Cloud Adoption Framework – Network topology and connectivity | https://learn.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/hub-spoke-network-topology |
| Azure Well-Architected Framework – Networking | https://learn.microsoft.com/azure/well-architected/service-guides/virtual-network |
| Network Security Groups | https://learn.microsoft.com/azure/virtual-network/network-security-groups-overview |
| Azure Firewall | https://learn.microsoft.com/azure/firewall/overview |
| Azure DDoS Protection | https://learn.microsoft.com/azure/ddos-protection/ddos-protection-overview |
| Azure Private Link | https://learn.microsoft.com/azure/private-link/private-link-overview |
| Azure Bastion | https://learn.microsoft.com/azure/bastion/bastion-overview |
| Microsoft Learn – Secure network connectivity in Azure | https://learn.microsoft.com/training/modules/secure-network-connectivity-azure/ |
