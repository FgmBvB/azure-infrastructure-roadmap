# Azure Virtual Networks Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Virtual Networks (VNets), explains their architecture, IP addressing, subnets, network interfaces, public and private IP addresses, and the fundamental networking concepts required for Azure administration.

---

# Overview

An **Azure Virtual Network (VNet)** is the fundamental networking component in Azure.

It enables Azure resources to communicate securely with each other, the Internet, and on-premises networks while providing complete control over IP addressing, routing, name resolution, and network security.

Every production Azure environment relies on Virtual Networks as the foundation for connectivity.

---

# Learning Objectives

After completing this section you should be able to:

* Understand Azure Virtual Networks.
* Design IP address spaces using CIDR.
* Configure subnets.
* Understand private and public IP addressing.
* Understand Network Interfaces (NICs).
* Differentiate Azure networking components.
* Build secure network architectures.

---

# Azure Networking Architecture

```text
                    Azure Subscription
                            │
                            ▼
                     Resource Group
                            │
                            ▼
                    Virtual Network (VNet)
                            │
        ┌─────────────┬──────────────┬──────────────┐
        │             │              │
        ▼             ▼              ▼
     Subnet A      Subnet B      Subnet C
        │             │              │
      VM1           VM2        App Service
        │
        ▼
     Network Interface
        │
 ┌──────┴────────┐
 │               │
 ▼               ▼
Private IP    Public IP
```

---

# What is a Virtual Network?

A Virtual Network provides:

* Private IP address space
* Network segmentation
* Secure communication
* DNS resolution
* Internet connectivity
* Hybrid connectivity
* Routing
* Traffic isolation

A VNet is logically isolated from every other Azure Virtual Network unless connectivity is explicitly configured.

---

# Address Space

Every Virtual Network requires one or more IP address ranges defined using **CIDR notation**.

Example:

```text
10.0.0.0/16
```

A VNet can contain multiple address spaces if required.

Example:

```text
10.0.0.0/16
172.16.0.0/16
```

Address spaces cannot overlap with directly connected networks such as:

* Peered VNets
* VPN-connected networks
* ExpressRoute-connected networks

---

# Subnets

Subnets divide a Virtual Network into smaller network segments.

Example:

```text
VNet
10.0.0.0/16

├── Frontend
│      10.0.1.0/24
│
├── Backend
│      10.0.2.0/24
│
└── Database
       10.0.3.0/24
```

Benefits include:

* Security boundaries
* Traffic isolation
* Simplified management
* Different routing policies
* Service delegation

Every Azure resource connects to a subnet.

---

# Network Interfaces (NICs)

A Network Interface (NIC) connects Azure resources to a Virtual Network.

A NIC contains:

* Private IP address
* Optional Public IP address
* Network Security Group association
* DNS settings
* IP forwarding configuration

Virtual Machines require at least one NIC.

---

# Private IP Addresses

Private IP addresses enable communication within Azure and connected private networks.

Characteristics:

* Assigned from the subnet address range.
* Can be static or dynamic.
* Not directly accessible from the Internet.
* Used for internal communication.

---

# Public IP Addresses

Public IP addresses provide Internet connectivity.

Characteristics:

* Reachable from the Internet.
* Can be static or dynamic.
* Available as Basic or Standard SKU.
* Can be IPv4 or IPv6.

Not every Azure resource requires a Public IP.

---

# Internet Connectivity

Azure resources can access the Internet through:

* Public IP Address
* Azure Load Balancer
* NAT Gateway
* Azure Firewall

Inbound Internet connectivity should always be minimized following Zero Trust principles.

---

# DNS Resolution

Azure automatically provides DNS name resolution within a Virtual Network.

Organizations can also configure:

* Azure DNS Private Resolver
* Custom DNS Servers
* Active Directory-integrated DNS

DNS configuration is inherited by all resources inside the Virtual Network unless overridden.

---

# Enterprise Scenario

A company deploys a Virtual Network using the address space **10.10.0.0/16**.

Separate subnets are created for:

* Web servers
* Application servers
* Database servers

Only the web subnet exposes Public IP addresses.

Application and database servers communicate exclusively through Private IP addresses while using Azure Private DNS for internal name resolution.

---

# Best Practices

* Plan IP address ranges before deployment.
* Avoid overlapping address spaces.
* Separate workloads into dedicated subnets.
* Use Private IPs whenever possible.
* Minimize Public IP exposure.
* Use Standard SKU Public IPs for production.
* Document IP allocations.
* Design networks with future expansion in mind.

---

# Common Pitfalls

* Overlapping address spaces.
* Creating excessively large flat networks.
* Assigning Public IPs unnecessarily.
* Forgetting future subnet growth.
* Mixing production and development resources within the same subnet.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> * Virtual Networks
> * Address Spaces
> * CIDR notation
> * Subnets
> * Network Interfaces
> * Public IPs
> * Private IPs
> * DNS
> * Internet connectivity

---

# Key Takeaways

* Virtual Networks provide the foundation for Azure networking.
* Every Azure resource connects to a subnet within a Virtual Network.
* Proper IP planning simplifies scalability and hybrid connectivity.
* Private networking should be preferred over public exposure whenever possible.
* Designing Virtual Networks correctly improves security, availability, and operational efficiency.

---

# References

| Microsoft Documentation                            | URL                                                                                  |
| -------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Azure Virtual Network documentation                | https://learn.microsoft.com/azure/virtual-network/                                   |
| Azure Virtual Network overview                     | https://learn.microsoft.com/azure/virtual-network/virtual-networks-overview          |
| IP addressing in Azure                             | https://learn.microsoft.com/azure/virtual-network/ip-services/private-ip-addresses   |
| Azure public IP addresses                          | https://learn.microsoft.com/azure/virtual-network/ip-services/public-ip-addresses    |
| Azure DNS                                          | https://learn.microsoft.com/azure/dns/                                               |
| Azure networking fundamentals                      | https://learn.microsoft.com/azure/networking/fundamentals/networking-overview        |
| Microsoft Learn – Introduction to Azure networking | https://learn.microsoft.com/training/modules/introduction-to-azure-virtual-networks/ |

