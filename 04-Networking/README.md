# Azure Networking

> [!NOTE]
> This module is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> Networking is one of the largest and most important domains of the AZ-104 exam. This module covers Azure Virtual Networks, network security, hybrid connectivity, and load balancing, following Microsoft's recommended architecture and best practices.

---

# Overview

Networking is the foundation of every Azure deployment.

Every Azure resource communicates through the network, making networking one of the core responsibilities of an Azure Administrator.

A well-designed Azure network provides:

- Secure communication
- High availability
- Hybrid connectivity
- Scalable architectures
- Private access to services
- Reliable traffic distribution

This module progressively builds from Virtual Networks to enterprise networking architectures using Microsoft's recommended design patterns.

---

# Learning Objectives

After completing this module you should be able to:

- Design Azure Virtual Networks.
- Plan IP addressing and subnets.
- Configure Azure DNS.
- Understand Azure routing.
- Secure networks using NSGs and Azure Firewall.
- Configure Private Endpoints and Service Endpoints.
- Deploy Azure Bastion.
- Configure VPN Gateway and ExpressRoute.
- Configure Virtual Network Peering.
- Design Hub-and-Spoke architectures.
- Configure Azure Load Balancer.
- Configure Azure Application Gateway.
- Apply Microsoft networking best practices.

---

# Module Structure

| Module | Topics |
|----------|--------|
| **01 - Virtual Networks** | Virtual Networks, Subnets, IP Addressing, Azure DNS, Routing, CIDR planning, GatewaySubnet, AzureFirewallSubnet, Service Delegation and networking fundamentals. |
| **02 - Network Security** | Network Security Groups, Azure Firewall, Azure Bastion, DDoS Protection, Private Endpoints, Service Endpoints, Private DNS integration and network security design. |
| **03 - Hybrid Connectivity** | VPN Gateway, ExpressRoute, BGP, Gateway Transit, VNet Peering, Hub-and-Spoke architecture, hybrid routing and enterprise connectivity. |
| **04 - Load Balancing** | Azure Load Balancer, Application Gateway, WAF, Health Probes, Backend Pools, Session Persistence, NAT Gateway integration and traffic distribution. |
| **05 - Best Practices** | Enterprise networking architecture, security, monitoring, governance, cost optimization and Microsoft's production recommendations. |

---

# Learning Path

```text
Virtual Networks
        │
        ▼
Network Security
        │
        ▼
Hybrid Connectivity
        │
        ▼
Load Balancing
        │
        ▼
Networking Best Practices
```

Each section builds on the previous one, following the same progression used in real Azure enterprise environments.

---

# Networking Architecture

```text
                     Internet
                         │
            ┌────────────┴────────────┐
            │                         │
            ▼                         ▼
   Application Gateway          Azure Firewall
          (WAF)                      │
            │                        │
            └────────────┬───────────┘
                         ▼
                  Azure Load Balancer
                         │
                 Virtual Network
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
      Web Tier       App Tier      Database Tier
                         │
                    Private Endpoint
                         │
                   Azure PaaS Services

──────────────────────────────────────────────────

                 Hybrid Connectivity

      On-Premises
            │
      VPN / ExpressRoute
            │
      Gateway Transit
            │
      Hub Virtual Network
            │
      VNet Peering
            │
        Spoke VNets
```

---

# Core Azure Networking Services

This module covers:

## Core Networking

- Azure Virtual Networks
- Subnets
- CIDR Planning
- Private IP Addresses
- Public IP Addresses
- Azure DNS
- Custom DNS
- Routing
- Route Tables (UDRs)

---

## Network Security

- Network Security Groups (NSGs)
- Azure Firewall
- Azure Bastion
- Azure DDoS Network Protection
- Service Endpoints
- Private Endpoints
- Private DNS Zones

---

## Hybrid Networking

- VPN Gateway
- Site-to-Site VPN
- Point-to-Site VPN
- VNet-to-VNet VPN
- ExpressRoute
- Gateway Transit
- Virtual Network Peering
- BGP
- Hub-and-Spoke

---

## Traffic Distribution

- Azure Load Balancer
- Internal Load Balancer
- Public Load Balancer
- Backend Pools
- Health Probes
- Load Balancing Rules
- NAT Rules
- Application Gateway
- Web Application Firewall (WAF)
- NAT Gateway

---

## Monitoring & Troubleshooting

- Azure Monitor
- Network Watcher
- Connection Monitor
- Connection Troubleshoot
- IP Flow Verify
- Effective Routes
- NSG Flow Logs

---

# Design Principles

Microsoft recommends designing Azure networks according to these principles:

- Plan IP addressing before deployment.
- Avoid overlapping address spaces.
- Prefer private connectivity whenever possible.
- Follow Zero Trust principles.
- Use Hub-and-Spoke for medium and large environments.
- Centralize shared networking services.
- Deploy redundant network paths.
- Protect Internet-facing workloads.
- Monitor networking continuously.
- Keep routing simple and predictable.

---

# AZ-104 Exam Focus

This module aligns with the official Microsoft AZ-104 objectives related to:

- Configure Virtual Networks.
- Configure IP addressing.
- Configure DNS.
- Configure routing.
- Configure Network Security Groups.
- Configure Azure Firewall.
- Configure Azure Bastion.
- Configure Private Endpoints.
- Configure Service Endpoints.
- Configure VPN Gateway.
- Configure ExpressRoute.
- Configure Virtual Network Peering.
- Configure Azure Load Balancer.
- Configure Application Gateway.
- Troubleshoot Azure networking.

---

# Key Takeaways

- Azure networking provides the foundation for secure, scalable, and highly available cloud infrastructures.
- Virtual Networks, routing, and DNS form the core of every Azure deployment.
- Network Security Groups, Azure Firewall, Bastion, and Private Endpoints implement layered network security following Zero Trust principles.
- VPN Gateway, ExpressRoute, and VNet Peering enable resilient hybrid and multi-network architectures.
- Azure Load Balancer and Application Gateway distribute traffic efficiently while improving availability and protecting Internet-facing applications.
- Proper planning, monitoring, governance, and adherence to Microsoft's networking best practices are essential for building production-ready Azure environments.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Networking documentation | https://learn.microsoft.com/azure/networking/ |
| Azure Virtual Network documentation | https://learn.microsoft.com/azure/virtual-network/ |
| Azure Network Security documentation | https://learn.microsoft.com/azure/security/fundamentals/network-overview |
| Azure VPN Gateway documentation | https://learn.microsoft.com/azure/vpn-gateway/ |
| Azure ExpressRoute documentation | https://learn.microsoft.com/azure/expressroute/ |
| Azure Load Balancer documentation | https://learn.microsoft.com/azure/load-balancer/ |
| Azure Application Gateway documentation | https://learn.microsoft.com/azure/application-gateway/ |
| Azure Firewall documentation | https://learn.microsoft.com/azure/firewall/ |
| Azure Network Watcher documentation | https://learn.microsoft.com/azure/network-watcher/ |
| Azure Well-Architected Framework – Networking | https://learn.microsoft.com/azure/well-architected/service-guides/virtual-network |
| Microsoft Learn – AZ-104 Learning Path | https://learn.microsoft.com/training/paths/az-104-administrator-prerequisites/ |
