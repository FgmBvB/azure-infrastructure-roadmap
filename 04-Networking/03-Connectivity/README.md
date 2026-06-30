# Azure Hybrid Connectivity

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> This module covers Azure hybrid networking technologies, including VPN Gateway, ExpressRoute, Virtual Network Peering, Hub-and-Spoke architectures, Gateway Transit, BGP, and Microsoft's recommended best practices for building secure and scalable connectivity between Azure and on-premises environments.

---

# Overview

Hybrid connectivity is a fundamental capability of Microsoft Azure.

Most enterprise environments require secure communication between Azure, on-premises datacenters, branch offices, remote users, and multiple Azure Virtual Networks.

Azure provides several complementary connectivity technologies, each designed for different scenarios:

- Azure VPN Gateway
- Azure ExpressRoute
- Virtual Network Peering

Together, these services enable organizations to build highly available, scalable, and secure hybrid infrastructures while minimizing operational complexity.

Understanding how these technologies interact is a core objective of the **AZ-104** certification.

---

# Learning Objectives

After completing this module you should be able to:

- Understand Azure VPN Gateway.
- Differentiate Site-to-Site, Point-to-Site, and VNet-to-VNet VPNs.
- Understand Azure ExpressRoute.
- Compare VPN Gateway and ExpressRoute.
- Configure Virtual Network Peering.
- Understand Gateway Transit.
- Configure Hub-and-Spoke architectures.
- Understand BGP route propagation.
- Apply Microsoft hybrid networking best practices.

---

# Module Structure

| Module | Description |
|---------|-------------|
| **01 - VPN and ExpressRoute** | Azure VPN Gateway, Site-to-Site VPN, Point-to-Site VPN, VNet-to-VNet VPN, ExpressRoute, gateway SKUs, BGP, GatewaySubnet, hybrid routing, and ExpressRoute coexistence. |
| **02 - VNet Peering** | Local and Global Peering, Gateway Transit, Allow Forwarded Traffic, Use Remote Gateway, Hub-and-Spoke networking, peering states, non-transitive routing, and shared services across peered VNets. |
| **03 - Best Practices** | Hybrid architecture design, gateway sizing, high availability, BGP, monitoring, governance, routing optimization, Hub-and-Spoke design, and Microsoft's recommended operational practices. |

---

# Azure Hybrid Connectivity Architecture

```text
                    On-Premises Network
                            │
                  ┌─────────┴─────────┐
                  │                   │
                  ▼                   ▼
            VPN Gateway        ExpressRoute
                  │                   │
                  └─────────┬─────────┘
                            │
                     Hub Virtual Network
                            │
              ┌─────────────┼─────────────┐
              │             │             │
              ▼             ▼             ▼
         Spoke VNet    Spoke VNet    Spoke VNet
```

The Hub centralizes connectivity and shared network services, while Spoke VNets host application workloads.

---

# Technologies Covered

This section includes:

- Azure VPN Gateway
- Site-to-Site VPN
- Point-to-Site VPN
- VNet-to-VNet VPN
- VPN Gateway Generations
- VPN Gateway SKUs (VpnGw)
- ExpressRoute
- ExpressRoute Peering
- BGP
- GatewaySubnet
- Gateway Transit
- Virtual Network Peering
- Local Peering
- Global Peering
- Allow Forwarded Traffic
- Use Remote Gateway
- Peering Connection States
- Non-Transitive Peering
- Hub-and-Spoke Architecture
- Connection Monitor
- IP Flow Verify
- Connection Troubleshoot
- High Availability
- Hybrid Routing

---

# Connectivity Models

Azure provides multiple connectivity options depending on business requirements.

| Technology | Typical Use Case |
|------------|------------------|
| **Site-to-Site VPN** | Permanent branch office or datacenter connectivity |
| **Point-to-Site VPN** | Remote administrators and remote users |
| **VNet-to-VNet VPN** | Secure connectivity between Azure Virtual Networks |
| **ExpressRoute** | Enterprise private connectivity |
| **VNet Peering** | Low-latency communication between Azure Virtual Networks |

Each technology addresses different networking requirements and can be combined in enterprise environments.

---

# Enterprise Design Principles

Microsoft recommends designing hybrid connectivity around a centralized networking model.

Typical Hub services include:

- Azure Firewall
- VPN Gateway
- ExpressRoute Gateway
- Azure Bastion
- Shared DNS
- Private DNS Zones

Spoke VNets host:

- Production applications
- Development environments
- Databases
- Shared business services

This architecture simplifies management, reduces costs, and improves security.

---

# AZ-104 Exam Focus

This module aligns with the Microsoft AZ-104 objectives related to:

- Configure Azure VPN Gateway.
- Configure Site-to-Site and Point-to-Site VPNs.
- Configure ExpressRoute.
- Configure Virtual Network Peering.
- Configure Gateway Transit.
- Configure BGP.
- Design Hub-and-Spoke architectures.
- Troubleshoot hybrid connectivity.
- Apply Azure networking best practices.

---

# Key Takeaways

- Azure provides multiple hybrid connectivity options designed for different business requirements.
- VPN Gateway offers encrypted connectivity over the Internet, while ExpressRoute provides dedicated private connectivity with predictable performance.
- Virtual Network Peering enables high-performance communication between Azure VNets without requiring gateways.
- Hub-and-Spoke architecture, Gateway Transit, and BGP simplify large-scale enterprise networking.
- Proper address planning, gateway sizing, routing design, and continuous monitoring are essential for building secure and resilient hybrid infrastructures.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure VPN Gateway documentation | https://learn.microsoft.com/azure/vpn-gateway/ |
| Azure ExpressRoute documentation | https://learn.microsoft.com/azure/expressroute/ |
| Virtual Network Peering | https://learn.microsoft.com/azure/virtual-network/virtual-network-peering-overview |
| Gateway Transit | https://learn.microsoft.com/azure/vpn-gateway/vpn-gateway-peering-gateway-transit |
| Azure VPN Gateway BGP overview | https://learn.microsoft.com/azure/vpn-gateway/vpn-gateway-bgp-overview |
| Azure architecture – Hub-and-Spoke | https://learn.microsoft.com/azure/architecture/networking/architecture/hub-spoke |
| Azure Well-Architected Framework – Networking | https://learn.microsoft.com/azure/well-architected/service-guides/virtual-network |
| Azure Network Watcher | https://learn.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview |
| Microsoft Learn – Connect your on-premises network to Azure | https://learn.microsoft.com/training/modules/connect-on-premises-network-with-vpn-gateway/ |
| Microsoft Learn – Connect virtual networks with VNet peering | https://learn.microsoft.com/training/modules/connect-azure-virtual-networks-with-vnet-peering/ |
