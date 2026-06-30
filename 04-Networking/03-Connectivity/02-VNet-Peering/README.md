# Azure Virtual Network Peering

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains Azure Virtual Network Peering, Local and Global Peering, gateway transit, remote gateways, peering limitations, pricing considerations, and Microsoft's recommended best practices.

---

# Overview

Azure Virtual Network Peering enables two or more Virtual Networks (VNets) to communicate directly through the Microsoft backbone network.

Unlike VPN Gateway or ExpressRoute, VNet Peering does **not** require gateways or encryption tunnels. Communication occurs over Microsoft's private backbone with very low latency and high bandwidth.

Peering is commonly used to build Hub-and-Spoke architectures, separate workloads, and connect applications distributed across multiple VNets.

Understanding VNet Peering is an important objective of the **AZ-104** certification.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure Virtual Network Peering.
- Differentiate Local and Global Peering.
- Configure Gateway Transit.
- Configure Use Remote Gateway.
- Understand peering limitations.
- Design Hub-and-Spoke architectures.
- Troubleshoot common peering issues.

---

# VNet Peering Architecture

```text
           Virtual Network A
          10.0.0.0/16
                 │
         Microsoft Backbone
                 │
           Virtual Network B
          10.1.0.0/16
```

Both VNets communicate privately without using the public Internet.

---

# Benefits

Azure Virtual Network Peering provides:

- Low latency
- High bandwidth
- Private connectivity
- No VPN Gateway required
- No Internet exposure
- Full Layer 3 connectivity
- Support for hybrid architectures

---

# Local vs Global Peering

| Feature | Local Peering | Global Peering |
|----------|---------------|----------------|
| Same Region | Yes | No |
| Different Regions | No | Yes |
| Microsoft Backbone | Yes | Yes |
| Gateway Required | No | No |
| Low Latency | Excellent | Very Good |

Both options use Microsoft's private global network.

---

# How Peering Works

Once peering is established:

- Resources communicate using private IP addresses.
- Existing NSGs remain enforced.
- Existing Route Tables remain enforced.
- Existing Azure Firewall rules remain enforced.
- Existing DNS configuration remains unchanged.

Peering does not merge Virtual Networks into a single network.

Each VNet maintains independent administration.

---

# Peering Configuration

A peering connection contains several configuration options.

| Option | Purpose |
|---------|---------|
| Allow Virtual Network Access | Enables communication between VNets |
| Allow Forwarded Traffic | Allows forwarded packets from NVAs |
| Allow Gateway Transit | Shares a VPN Gateway or ExpressRoute Gateway |
| Use Remote Gateway | Uses a gateway located in another VNet |

These options enable Hub-and-Spoke architectures.

---

# Gateway Transit

Gateway Transit allows multiple Spoke VNets to share a single gateway deployed in the Hub.

Example:

```text
On-Premises

↓

VPN Gateway

↓

Hub VNet

↓

Gateway Transit

↓

Spoke A

↓

Spoke B

↓

Spoke C
```

Benefits include:

- Lower cost
- Centralized connectivity
- Simplified management
- Easier hybrid networking

---

# Allow Forwarded Traffic

Allow Forwarded Traffic is required when traffic passes through a Network Virtual Appliance (NVA) or Azure Firewall.

Typical scenario:

```text
Spoke VNet

↓

Azure Firewall

↓

Internet
```

Without this option, forwarded packets are dropped across the peering connection.

---

# Hub-and-Spoke Architecture

A common enterprise design uses:

Hub:

- Azure Firewall
- VPN Gateway
- ExpressRoute Gateway
- Azure Bastion
- Shared DNS

Spokes:

- Application workloads
- Databases
- Development environments
- Production environments

The Hub centralizes shared networking services.

---

# Pricing

VNet Peering has no gateway cost.

However:

- Data transferred across peering connections is billed.
- Ingress and egress charges depend on the peering type.
- Global Peering generally incurs higher data transfer costs than Local Peering.

Always review Azure pricing when designing large-scale architectures.

---

# Enterprise Scenario

A company deploys:

Hub:

- Azure Firewall
- VPN Gateway
- Azure Bastion

Spokes:

- HR
- Finance
- Sales
- Production

Each Spoke accesses on-premises resources through Gateway Transit.

Azure Firewall centrally inspects Internet-bound traffic.

No additional VPN Gateways are required.

---

# Best Practices

- Use Hub-and-Spoke for enterprise environments.
- Minimize the number of VPN Gateways.
- Use Gateway Transit whenever appropriate.
- Enable Allow Forwarded Traffic when using Azure Firewall or NVAs.
- Avoid overlapping address spaces.
- Monitor peering status regularly.
- Document all peering relationships.

---

# Common Pitfalls

- Overlapping address spaces.
- Forgetting reciprocal peering.
- Misconfiguring Gateway Transit.
- Forgetting Allow Forwarded Traffic.
- Assuming peering bypasses NSGs.
- Ignoring data transfer costs.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Local Peering
> - Global Peering
> - Gateway Transit
> - Use Remote Gateway
> - Allow Forwarded Traffic
> - Hub-and-Spoke networking
> - Peering limitations
> - Pricing considerations

---

# Key Takeaways

- VNet Peering provides private, high-performance connectivity between Azure Virtual Networks using Microsoft's backbone network.
- Gateway Transit allows multiple VNets to share hybrid connectivity resources, reducing cost and simplifying administration.
- Peering preserves each Virtual Network's security, routing, and DNS configuration while enabling seamless private communication.
- Hub-and-Spoke is Microsoft's recommended enterprise architecture for centralized networking services.
- Proper address planning and peering configuration are essential for scalable and maintainable Azure environments.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Virtual Network Peering | https://learn.microsoft.com/azure/virtual-network/virtual-network-peering-overview |
| Create Virtual Network Peering | https://learn.microsoft.com/azure/virtual-network/tutorial-connect-virtual-networks-portal |
| Gateway Transit | https://learn.microsoft.com/azure/vpn-gateway/vpn-gateway-peering-gateway-transit |
| Azure Virtual Network FAQ | https://learn.microsoft.com/azure/virtual-network/virtual-networks-faq |
| Hub-and-Spoke Network Topology | https://learn.microsoft.com/azure/architecture/networking/architecture/hub-spoke |
| Azure Well-Architected Framework – Networking | https://learn.microsoft.com/azure/well-architected/service-guides/virtual-network |
| Microsoft Learn – Connect virtual networks with VNet peering | https://learn.microsoft.com/training/modules/connect-azure-virtual-networks-with-vnet-peering/ |
