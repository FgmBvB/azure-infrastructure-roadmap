# Azure Subnets and IP Addressing

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains Azure subnetting, IP addressing, CIDR notation, address planning, reserved IP addresses, IP allocation methods, and Microsoft's recommended networking practices.

---

# Overview

Subnets divide a Virtual Network (VNet) into smaller logical network segments.

They provide network isolation, simplify administration, improve security, and allow Azure services to apply different routing and security policies to different workloads.

Proper IP address planning is one of the most important networking skills required for the AZ-104 certification.

---

# Learning Objectives

After completing this section you should be able to:

- Understand CIDR notation.
- Plan Azure address spaces.
- Design subnet layouts.
- Calculate usable IP addresses.
- Configure static and dynamic private IP addresses.
- Understand Azure reserved IP addresses.
- Avoid overlapping address spaces.

---

# Azure Address Hierarchy

```text
Azure Subscription
        │
        ▼
Virtual Network
10.0.0.0/16
        │
 ┌──────┴──────────────┐
 │                     │
 ▼                     ▼
Frontend           Backend
10.0.1.0/24      10.0.2.0/24
 │                     │
 ▼                     ▼
 VM                 Database
```

---

# CIDR Notation

Azure networks use **Classless Inter-Domain Routing (CIDR)**.

Example:

```text
10.0.0.0/16
```

The prefix length determines the network size.

| CIDR | Total Addresses | Usable in Azure |
|------|----------------:|----------------:|
| /24 | 256 | 251 |
| /25 | 128 | 123 |
| /26 | 64 | 59 |
| /27 | 32 | 27 |
| /28 | 16 | 11 |
| /29 | 8 | 3 |

Azure reserves five addresses in every subnet.

---

# Azure Reserved IP Addresses

Azure reserves the first four IP addresses and the last IP address of every subnet.

Example:

Subnet:

```text
10.0.1.0/24
```

| Address | Purpose |
|----------|---------|
| 10.0.1.0 | Network address |
| 10.0.1.1 | Azure default gateway |
| 10.0.1.2 | Azure DNS |
| 10.0.1.3 | Reserved for Azure platform services |
| 10.0.1.255 | Reserved address |

Because of these reservations, not every IP address can be assigned to Azure resources.

> [!IMPORTANT]
> Azure always reserves **five IP addresses** in every subnet regardless of subnet size.

---

# Address Planning

Good address planning should:

- Leave room for future expansion.
- Avoid overlapping ranges.
- Separate workloads into different subnets.
- Reserve space for future services.
- Support hybrid connectivity.

Example:

```text
10.10.0.0/16

Frontend      10.10.1.0/24

Application   10.10.2.0/24

Database      10.10.3.0/24

Management    10.10.10.0/24

Future        10.10.20.0/24
```

---

# Private IP Address Allocation

Azure supports two allocation methods.

## Dynamic

- Assigned automatically.
- Address remains associated with the resource while it exists.
- Azure manages allocation.

Recommended for most workloads.

---

## Static

Administrator selects the address.

Recommended for:

- Domain Controllers
- DNS Servers
- Firewalls
- Network Virtual Appliances
- Load Balancers

Static addresses must belong to the subnet address range.

---

# Public IP Addresses

Azure resources may optionally receive Public IP addresses.

Characteristics:

- IPv4 or IPv6
- Static or Dynamic
- Standard SKU
- Internet connectivity

Production workloads should minimize Public IP exposure whenever possible.

---

# Multiple Address Spaces

A Virtual Network can contain multiple address spaces.

Example:

```text
10.0.0.0/16

172.16.0.0/16
```

This simplifies network expansion without recreating the Virtual Network.

Additional address spaces must not overlap with connected networks.

---

# Enterprise Scenario

A company initially deploys a Virtual Network using **10.20.0.0/16**.

After several years, additional workloads require more address capacity.

Instead of recreating the Virtual Network, administrators add a second address space:

```text
10.21.0.0/16
```

Existing resources continue operating while new subnets are created inside the additional address range.

---

# Best Practices

- Design address spaces before deployment.
- Allocate generous address ranges.
- Avoid overlapping CIDR blocks.
- Reserve subnet capacity for future growth.
- Use separate subnets for different workloads.
- Minimize Public IP usage.
- Use static Private IPs only when necessary.
- Document IP allocations.

---

# Common Pitfalls

- Creating address spaces that overlap with on-premises networks.
- Using subnet sizes that cannot accommodate future growth.
- Forgetting Azure's five reserved IP addresses.
- Mixing unrelated workloads in the same subnet.
- Assigning static addresses outside the subnet range.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - CIDR notation
> - Address Spaces
> - Subnets
> - Azure reserved IP addresses
> - Static vs Dynamic Private IPs
> - Public IP allocation
> - Address planning
> - Multiple address spaces

---

# Key Takeaways

- Careful IP planning simplifies future expansion and hybrid connectivity.
- Azure reserves five IP addresses in every subnet.
- CIDR notation determines the available address space.
- Separate workloads into dedicated subnets for security and manageability.
- Well-designed subnet layouts improve scalability, availability, and operational efficiency.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Virtual Network overview | https://learn.microsoft.com/azure/virtual-network/virtual-networks-overview |
| IP addressing in Azure | https://learn.microsoft.com/azure/virtual-network/ip-services/private-ip-addresses |
| Azure public IP addresses | https://learn.microsoft.com/azure/virtual-network/ip-services/public-ip-addresses |
| Azure Virtual Network FAQ | https://learn.microsoft.com/azure/virtual-network/virtual-networks-faq |
| Azure networking fundamentals | https://learn.microsoft.com/azure/networking/fundamentals/networking-overview |
| Microsoft Learn – Configure virtual networks | https://learn.microsoft.com/training/modules/configure-virtual-networks/ |
