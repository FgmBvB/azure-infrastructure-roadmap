# Azure Virtual Networks

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Virtual Networks (VNets), including IP addressing, subnet design, DNS, routing, connectivity, and Microsoft's recommended networking best practices.

---

# Overview

Azure Virtual Network (VNet) is the foundation of networking in Microsoft Azure.

A VNet provides secure communication between Azure resources while enabling connectivity to the Internet, on-premises datacenters, and other Azure Virtual Networks.

It allows administrators to design isolated network environments, control traffic flow, implement security boundaries, and build scalable hybrid cloud architectures.

Understanding Virtual Networks is one of the most important networking skills required for the AZ-104 certification.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure Virtual Networks.
- Design address spaces and subnets.
- Configure IP addressing.
- Understand Azure DNS and name resolution.
- Configure custom routing.
- Apply Azure networking best practices.
- Build scalable and secure network architectures.

---

# Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Virtual Networks, network architecture, address spaces, subnets, network interfaces, public and private IP addresses, Internet connectivity, and Azure DNS fundamentals. |
| **02 - Subnets and IP Addressing** | CIDR notation, subnet planning, Azure reserved IP addresses, static and dynamic IP allocation, subnet delegation, reserved Azure subnets, and address space expansion. |
| **03 - DNS** | Azure-provided DNS, Azure DNS, Private DNS Zones, Custom DNS Servers, Virtual Network Links, auto-registration, and DNS resolution. |
| **04 - Routing** | System Routes, User-Defined Routes (UDRs), Route Tables, Effective Routes, Next Hop types, route precedence, IP Forwarding, gateway route propagation, and forced tunneling. |
| **05 - Best Practices** | Network design, subnet planning, DNS, routing, security, governance, monitoring, high availability, and operational recommendations. |

---

# Azure Virtual Network Architecture

```text
                          Azure Virtual Network
                                     │
        ┌────────────────────────────┼────────────────────────────┐
        │                            │                            │
        ▼                            ▼                            ▼
 Address Space                  DNS Services                 Routing Engine
        │                            │                            │
        ▼                            ▼                            ▼
     Subnets                 Azure / Private DNS          System & UDR Routes
        │
        ▼
 Azure Resources
(VMs, PaaS, Private Endpoints)
```

---

# Skills Covered

This section includes:

- Azure Virtual Networks
- Address Spaces
- CIDR Notation
- Subnets
- Azure Reserved IP Addresses
- Static and Dynamic Private IPs
- Public IP Addresses
- Standard Public IP SKU
- GatewaySubnet
- AzureFirewallSubnet
- Subnet Delegation
- Azure-provided DNS
- Azure DNS
- Azure Private DNS
- Custom DNS Servers
- Virtual Network Links
- Auto-registration
- System Routes
- User-Defined Routes (UDRs)
- Route Tables
- Effective Routes
- Route Precedence
- Next Hop Types
- IP Forwarding
- Gateway Route Propagation
- Forced Tunneling

---

# AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Configure Azure Virtual Networks.
- Configure address spaces and subnets.
- Configure private and public IP addresses.
- Configure Azure DNS and Custom DNS.
- Configure Route Tables and User-Defined Routes.
- Understand route selection and Effective Routes.
- Implement subnet delegation.
- Design secure and scalable Virtual Network architectures.

---

# Key Takeaways

- Azure Virtual Networks provide the networking foundation for Azure resources.
- Proper address planning simplifies future growth, hybrid connectivity, and network management.
- DNS and routing are core services that determine how Azure resources communicate.
- User-Defined Routes, subnet delegation, and dedicated Azure subnets enable advanced networking scenarios.
- Following Microsoft's networking best practices improves security, scalability, availability, and operational efficiency.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Virtual Network documentation | https://learn.microsoft.com/azure/virtual-network/ |
| Azure Virtual Network overview | https://learn.microsoft.com/azure/virtual-network/virtual-networks-overview |
| Azure networking fundamentals | https://learn.microsoft.com/azure/networking/fundamentals/networking-overview |
| Azure DNS documentation | https://learn.microsoft.com/azure/dns/ |
| Azure Private DNS | https://learn.microsoft.com/azure/dns/private-dns-overview |
| Azure route tables | https://learn.microsoft.com/azure/virtual-network/manage-route-table |
| Azure routing overview | https://learn.microsoft.com/azure/virtual-network/virtual-networks-udr-overview |
| Azure Well-Architected Framework – Networking | https://learn.microsoft.com/azure/well-architected/service-guides/virtual-network |
| Microsoft Learn – Configure virtual networks | https://learn.microsoft.com/training/modules/configure-virtual-networks/ |
