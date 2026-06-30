# Azure VPN Gateway and ExpressRoute

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains Azure VPN Gateway, Azure ExpressRoute, hybrid connectivity options, gateway types, routing, BGP, coexistence scenarios, and Microsoft's recommended best practices for connecting Azure with on-premises networks.

---

# Overview

Hybrid networking is one of the most common enterprise scenarios in Azure.

Organizations frequently need to connect Azure Virtual Networks with on-premises datacenters, branch offices, or other cloud environments while maintaining secure and reliable communication.

Azure provides two primary hybrid connectivity solutions:

- **Azure VPN Gateway**
- **Azure ExpressRoute**

Both provide connectivity between Azure and external networks, but they differ significantly in cost, performance, availability, latency, and security.

Understanding when to choose each solution is a core objective of the **AZ-104** certification.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure VPN Gateway.
- Understand Azure ExpressRoute.
- Differentiate Site-to-Site, Point-to-Site, and VNet-to-VNet VPNs.
- Understand Gateway Types.
- Understand BGP routing.
- Compare VPN Gateway and ExpressRoute.
- Design hybrid connectivity architectures.

---

# Hybrid Connectivity Architecture

```text
                    On-Premises Network
                           │
            ┌──────────────┴──────────────┐
            │                             │
            ▼                             ▼
      VPN Gateway                 ExpressRoute
            │                             │
            └──────────────┬──────────────┘
                           │
                    Azure Virtual Network
                           │
                    Azure Resources
```

---

# Azure VPN Gateway

Azure VPN Gateway provides encrypted communication over the public Internet.

It enables secure connectivity between Azure Virtual Networks and external networks using industry-standard VPN protocols.

Common scenarios include:

- Site-to-Site (S2S) VPN
- Point-to-Site (P2S) VPN
- VNet-to-VNet VPN

---

# Site-to-Site VPN

A Site-to-Site VPN permanently connects an on-premises VPN device with Azure.

Characteristics:

- Always-on connection
- IPsec/IKE encryption
- Requires a VPN appliance
- Supports branch offices and datacenters

Typical architecture:

```text
Office

↓

VPN Appliance

↓

Internet

↓

Azure VPN Gateway

↓

Azure VNet
```

---

# Point-to-Site VPN

Point-to-Site VPN allows individual users to connect securely to Azure.

Characteristics:

- User-initiated connection
- Remote access
- Supports Windows, macOS and Linux
- Suitable for administrators and remote workers

Authentication options include:

- Microsoft Entra ID
- Certificates
- RADIUS

---

# VNet-to-VNet VPN

VNet-to-VNet VPN securely connects two Azure Virtual Networks.

Common scenarios:

- Multi-region deployments
- Environment isolation
- Disaster recovery
- Cross-subscription connectivity

Traffic remains encrypted between gateways.

---

# Azure ExpressRoute

Azure ExpressRoute provides private connectivity between Azure and on-premises environments.

Unlike VPN Gateway:

- Traffic does not traverse the public Internet.
- Connectivity uses a dedicated provider network.
- Lower latency.
- Higher bandwidth.
- Predictable performance.

ExpressRoute is designed for enterprise and mission-critical workloads.

---

# ExpressRoute Benefits

Advantages include:

- Private connectivity
- High reliability
- Lower latency
- Predictable performance
- Higher bandwidth
- SLA-backed availability
- Supports Microsoft Peering and Private Peering

---

# VPN Gateway vs ExpressRoute

| Feature | VPN Gateway | ExpressRoute |
|----------|-------------|--------------|
| Internet | Yes | No |
| Encryption | Yes | Optional (recommended when required) |
| Private Connectivity | No | Yes |
| Typical Latency | Higher | Lower |
| Bandwidth | Lower | Higher |
| Cost | Lower | Higher |
| Enterprise Workloads | Good | Excellent |

---

# Gateway Types

Azure Virtual Networks support different gateway types.

| Gateway | Purpose |
|----------|---------|
| VPN Gateway | Encrypted VPN connectivity |
| ExpressRoute Gateway | ExpressRoute connectivity |

Each Virtual Network can contain only one gateway of each supported type.

---

## VPN Gateway Generations and SKUs

Azure VPN Gateway is available in two hardware generations.

### Generation 1

Generation 1 gateways support basic hybrid networking scenarios.

They are compatible with older gateway SKUs and provide lower maximum throughput.

---

### Generation 2

Generation 2 gateways provide:

- Higher throughput
- Improved scalability
- Support for newer VPN Gateway SKUs
- Better performance for enterprise deployments

Microsoft recommends Generation 2 for new production environments whenever supported.

---

### VPN Gateway SKUs

Modern Azure deployments typically use the **VpnGw** family.

Examples include:

- VpnGw1
- VpnGw2
- VpnGw3
- VpnGw4
- VpnGw5

Zone-redundant variants are also available:

- VpnGw1AZ
- VpnGw2AZ
- VpnGw3AZ
- VpnGw4AZ
- VpnGw5AZ

Zone-redundant gateways provide higher availability by distributing gateway instances across Availability Zones.

> [!IMPORTANT]
> The Basic VPN Gateway SKU has significant limitations, including reduced throughput, limited Site-to-Site connections, and no support for BGP or ExpressRoute coexistence.

---

# Border Gateway Protocol (BGP)

BGP is a dynamic routing protocol supported by both VPN Gateway and ExpressRoute.

Benefits include:

- Automatic route exchange
- Dynamic failover
- Simplified route management
- Reduced administrative overhead

BGP is recommended for enterprise hybrid environments.

---

# Gateway Subnet

Every VPN Gateway and ExpressRoute Gateway requires a dedicated subnet.

Requirements:

- Name must be **GatewaySubnet**
- Microsoft recommends a subnet size of **/27** or larger
- No other Azure resources may be deployed in this subnet

---

# Coexistence

Azure supports VPN Gateway and ExpressRoute operating within the same Virtual Network.

Typical scenarios:

- ExpressRoute for production workloads
- VPN Gateway as backup connectivity
- Migration from VPN to ExpressRoute

Gateway coexistence requires an appropriately sized **GatewaySubnet**.

---

# Enterprise Scenario

A multinational company connects its primary datacenter to Azure using ExpressRoute.

Branch offices use Site-to-Site VPN connections.

Remote administrators connect through Point-to-Site VPN.

BGP automatically exchanges routes between Azure and the corporate network.

ExpressRoute provides production connectivity while VPN Gateway serves as a backup path.

---

# Best Practices

- Use ExpressRoute for mission-critical production workloads.
- Use VPN Gateway for branch offices and smaller deployments.
- Enable BGP whenever supported.
- Allocate sufficient address space for GatewaySubnet.
- Use redundant VPN devices on-premises.
- Monitor gateway health continuously.
- Plan IP addressing before deployment.
- Document hybrid routing topology.

---

# Common Pitfalls

- Deploying resources inside GatewaySubnet.
- Choosing a GatewaySubnet that is too small.
- Forgetting BGP configuration.
- Overlapping address spaces.
- Assuming ExpressRoute encrypts traffic by default.
- Confusing Site-to-Site and Point-to-Site VPNs.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - VPN Gateway
> - Site-to-Site VPN
> - Point-to-Site VPN
> - VNet-to-VNet VPN
> - ExpressRoute
> - GatewaySubnet
> - BGP
> - Gateway coexistence
> - VPN Gateway vs ExpressRoute

---

# Key Takeaways

- Azure VPN Gateway provides secure encrypted connectivity over the Internet.
- Azure ExpressRoute provides dedicated private connectivity with predictable performance.
- BGP simplifies route management and improves hybrid network resilience.
- GatewaySubnet is mandatory for deploying Azure VPN Gateway and ExpressRoute Gateway.
- Selecting the appropriate hybrid connectivity solution depends on security, performance, availability, and business requirements.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure VPN Gateway documentation | https://learn.microsoft.com/azure/vpn-gateway/ |
| Azure VPN Gateway overview | https://learn.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways |
| Azure ExpressRoute documentation | https://learn.microsoft.com/azure/expressroute/ |
| ExpressRoute overview | https://learn.microsoft.com/azure/expressroute/expressroute-introduction |
| About BGP with VPN Gateway | https://learn.microsoft.com/azure/vpn-gateway/vpn-gateway-bgp-overview |
| ExpressRoute FAQ | https://learn.microsoft.com/azure/expressroute/expressroute-faqs |
| Microsoft Learn – Connect your on-premises network to Azure | https://learn.microsoft.com/training/modules/connect-on-premises-network-with-vpn-gateway/ |
