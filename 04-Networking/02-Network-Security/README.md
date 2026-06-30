# Azure Network Security

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> This module covers Azure networking security services, including Network Security Groups (NSGs), Application Security Groups (ASGs), Azure Firewall, Azure DDoS Protection, Private Link, Private Endpoints, Azure Bastion, Zero Trust networking, and Microsoft's recommended security best practices.

---

# Overview

Securing Azure networking involves multiple complementary technologies working together to protect workloads, control traffic, reduce the attack surface, and enable secure connectivity.

Rather than relying on a single security device, Azure follows a **defense-in-depth** model where each service addresses a specific layer of network security.

This module explains how Azure protects network traffic at different layers and how these services interact in real-world enterprise environments.

Understanding these concepts is essential for the **AZ-104** certification and forms the foundation for more advanced networking and security certifications.

---

# Learning Objectives

After completing this module you should be able to:

- Understand Azure network security architecture.
- Configure Network Security Groups (NSGs).
- Understand Application Security Groups (ASGs).
- Configure Azure Firewall.
- Differentiate Azure Firewall and NSGs.
- Understand Azure DDoS Protection.
- Configure Private Link and Private Endpoints.
- Secure Azure PaaS services.
- Understand Azure Bastion.
- Apply Zero Trust networking principles.
- Implement Microsoft networking best practices.

---

# Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Azure networking security architecture, Network Security Groups, Application Security Groups, Azure Firewall, Azure DDoS Protection, Private Endpoints, Service Endpoints, Azure Bastion, and Zero Trust principles. |
| **02 - Private Connectivity** | Azure Private Link, Private Endpoints, Service Endpoints, Private DNS integration, hybrid connectivity, Private Endpoint network policies, and secure access to Azure PaaS services. |
| **03 - Azure Firewall and DDoS** | Azure Firewall architecture, rule processing, DNAT, SNAT, Threat Intelligence, Azure Firewall Premium, Azure DDoS Network Protection, Forced Tunneling, and centralized traffic inspection. |
| **04 - Best Practices** | Network segmentation, Zero Trust, NSGs, Azure Firewall, Private Endpoints, monitoring, governance, troubleshooting, and Microsoft's networking security recommendations. |

---

# Azure Network Security Architecture

```text
                               Internet
                                   │
                                   ▼
                    Azure DDoS Network Protection
                                   │
                                   ▼
                         Azure Firewall / WAF
                                   │
                  ┌────────────────┴────────────────┐
                  │                                 │
                  ▼                                 ▼
           Virtual Network                  Private Link
                  │                                 │
        ┌─────────┼─────────┐                       │
        │         │         │                       │
        ▼         ▼         ▼                       ▼
      NSGs      ASGs   Azure Bastion        Private Endpoints
        │
        ▼
 Azure Virtual Machines
 Azure PaaS Services
```

---

# Technologies Covered

This section includes:

- Network Security Groups (NSGs)
- Application Security Groups (ASGs)
- NSG Rule Processing
- Default NSG Rules
- Azure Firewall
- Azure Firewall Premium
- Firewall Rule Collections
- Rule Processing Order
- DNAT and SNAT
- Threat Intelligence
- Forced Tunneling
- Azure DDoS Network Protection
- Azure Private Link
- Private Endpoints
- Service Endpoints
- Private DNS Integration
- Hybrid Connectivity
- Private Endpoint Network Policies
- Azure Bastion
- AzureBastionSubnet
- Zero Trust Networking
- Network Watcher
- IP Flow Verify
- Connection Troubleshoot

---

# Security Layers

Azure networking security is built using multiple layers.

| Layer | Primary Service | Purpose |
|--------|-----------------|---------|
| Identity | Microsoft Entra ID | Authentication and authorization |
| Network Filtering | Network Security Groups | Traffic filtering at subnet and NIC level |
| Central Inspection | Azure Firewall | Stateful centralized filtering |
| Private Connectivity | Private Link | Secure access to Azure PaaS services |
| Internet Protection | Azure DDoS Network Protection | Protection against volumetric attacks |
| Secure Administration | Azure Bastion | Secure RDP and SSH without Public IPs |
| Monitoring | Network Watcher | Network diagnostics and troubleshooting |

Each layer complements the others to implement Microsoft's defense-in-depth strategy.

---

# AZ-104 Exam Focus

This module aligns with the Microsoft AZ-104 objectives related to:

- Configure Network Security Groups.
- Configure Application Security Groups.
- Configure Azure Firewall.
- Configure Azure Bastion.
- Configure Private Link and Private Endpoints.
- Configure Service Endpoints.
- Secure Azure PaaS services.
- Configure Azure DDoS Protection.
- Troubleshoot network connectivity using Network Watcher.
- Apply Zero Trust networking principles.

---

# Key Takeaways

- Azure network security is based on multiple complementary security layers rather than a single security solution.
- Network Security Groups provide distributed traffic filtering, while Azure Firewall delivers centralized inspection and advanced threat protection.
- Private Endpoints are Microsoft's recommended solution for securing Azure PaaS services because they provide true private connectivity and reduce data exfiltration risks.
- Azure Bastion, Azure DDoS Network Protection, and Network Watcher complete the security architecture by providing secure administration, attack mitigation, and operational troubleshooting.
- Understanding how these services interact is essential for designing secure, scalable, and production-ready Azure environments.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure network security documentation | https://learn.microsoft.com/azure/security/fundamentals/network-overview |
| Network Security Groups | https://learn.microsoft.com/azure/virtual-network/network-security-groups-overview |
| Application Security Groups | https://learn.microsoft.com/azure/virtual-network/application-security-groups |
| Azure Firewall | https://learn.microsoft.com/azure/firewall/overview |
| Azure Firewall Premium | https://learn.microsoft.com/azure/firewall/premium-features |
| Azure DDoS Protection | https://learn.microsoft.com/azure/ddos-protection/ddos-protection-overview |
| Azure Private Link | https://learn.microsoft.com/azure/private-link/private-link-overview |
| Azure Private Endpoint | https://learn.microsoft.com/azure/private-link/private-endpoint-overview |
| Azure Bastion | https://learn.microsoft.com/azure/bastion/bastion-overview |
| Azure Network Watcher | https://learn.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview |
| Azure Well-Architected Framework – Networking | https://learn.microsoft.com/azure/well-architected/service-guides/virtual-network |
| Microsoft Learn – Secure network connectivity in Azure | https://learn.microsoft.com/training/modules/secure-network-connectivity-azure/ |
