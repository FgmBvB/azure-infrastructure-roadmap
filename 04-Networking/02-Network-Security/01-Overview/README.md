# Azure Network Security Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure networking security services, including Network Security Groups (NSGs), Application Security Groups (ASGs), Azure Firewall, DDoS Protection, Private Endpoints, Service Endpoints, Azure Bastion, and Zero Trust networking principles.

---

# Overview

Network security is a fundamental pillar of every Azure infrastructure.

Azure provides multiple security layers that protect workloads from unauthorized access while allowing administrators to control traffic between resources, Virtual Networks, on-premises environments, and the Internet.

Rather than relying on a single security device, Azure follows a **defense-in-depth** strategy where multiple security services work together.

Understanding how these services interact is essential for the AZ-104 certification.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure networking security services.
- Differentiate NSGs and Azure Firewall.
- Understand Application Security Groups.
- Differentiate Service Endpoints and Private Endpoints.
- Understand Azure Bastion.
- Understand DDoS Protection.
- Apply Zero Trust networking principles.

---

# Azure Network Security Architecture

```text
                           Internet
                               │
                               ▼
                    DDoS Protection Standard
                               │
                               ▼
                       Azure Firewall / WAF
                               │
                     ┌─────────┴─────────┐
                     │                   │
                     ▼                   ▼
                 Virtual Network    Private Link
                     │                   │
          ┌──────────┴──────────┐        │
          │                     │        │
          ▼                     ▼        ▼
     Network Security     Azure Bastion  Private Endpoints
         Groups
```

---

# Network Security Layers

Azure networking security is built using multiple complementary layers.

| Layer | Purpose |
|--------|---------|
| **DDoS Protection** | Protects against volumetric network attacks |
| **Azure Firewall** | Centralized network filtering |
| **Network Security Groups** | Subnet and NIC traffic filtering |
| **Application Security Groups** | Logical workload grouping |
| **Private Endpoints** | Private access to Azure PaaS services |
| **Service Endpoints** | Secure service access over Azure backbone |
| **Azure Bastion** | Secure VM administration without Public IPs |

Each service addresses different security requirements.

---

# Network Security Groups (NSGs)

Network Security Groups filter inbound and outbound traffic.

NSGs contain security rules based on:

- Source
- Destination
- Port
- Protocol
- Direction
- Action (Allow or Deny)

NSGs can be associated with:

- Subnets
- Network Interfaces (NICs)

---

## NSG Processing Order

Network Security Groups can be associated with both:

- Subnets
- Network Interfaces (NICs)

When both associations exist, Azure evaluates security rules in a specific order.

### Inbound Traffic

```text
Internet

↓

Subnet NSG

↓

NIC NSG

↓

Virtual Machine
```

The packet must be allowed by **both** Network Security Groups.

If either NSG contains a matching **Deny** rule, the traffic is blocked.

---

### Outbound Traffic

```text
Virtual Machine

↓

NIC NSG

↓

Subnet NSG

↓

Destination
```

Again, both NSGs must allow the traffic.

> [!IMPORTANT]
> NSGs operate as layered security controls. A single matching **Deny** rule at either the subnet or NIC level immediately blocks the traffic.

---

# Application Security Groups (ASGs)

Application Security Groups simplify NSG rule management.

Instead of creating rules based on IP addresses, administrators group Virtual Machines by application role.

Example:

```text
Web Servers

↓

Application Security Group

↓

NSG Rule

↓

Database Servers
```

This reduces administrative complexity as infrastructures grow.

---

# Azure Firewall

Azure Firewall is a fully managed stateful firewall service.

Capabilities include:

- Centralized network filtering
- Application rules
- Network rules
- FQDN filtering
- Threat Intelligence
- Logging
- High availability

Azure Firewall is typically deployed in a Hub Virtual Network.

---

# DDoS Protection

Azure provides two protection levels.

| Service | Description |
|----------|-------------|
| **Basic** | Included with Azure by default |
| **Standard** | Advanced protection, monitoring, and financial protection |

DDoS Protection Standard integrates with Virtual Networks and protects Internet-facing workloads.

---

# Azure DDoS Protection

Azure automatically protects all public IP resources with **DDoS Infrastructure Protection**.

For enhanced protection, organizations can enable **Azure DDoS Network Protection**.

| Protection Level | Description |
|------------------|-------------|
| **Infrastructure Protection** | Automatically included for all Azure services. Protects against common network-layer attacks. |
| **Azure DDoS Network Protection** | Provides advanced mitigation, attack analytics, telemetry, and cost protection for Internet-facing workloads. |

Azure DDoS Network Protection integrates with Virtual Networks and protects supported public IP resources deployed within those VNets.

> [!IMPORTANT]
> Azure DDoS Network Protection is recommended for production environments that expose critical Internet-facing applications.

---

# Service Endpoints

Service Endpoints extend a Virtual Network identity to supported Azure services.

Characteristics:

- Traffic remains on the Microsoft backbone network.
- Public endpoints are still used.
- Simple to configure.
- Improve security compared to unrestricted public access.

---

# Private Endpoints

Private Endpoints assign a private IP address from your Virtual Network to an Azure service.

Benefits include:

- Private connectivity.
- No Internet exposure.
- Azure backbone communication.
- Integration with Private DNS.

Private Endpoints are recommended for production workloads.

---

# Azure Bastion

Azure Bastion enables secure RDP and SSH access through the Azure portal.

Benefits include:

- No Public IP on Virtual Machines.
- Browser-based administration.
- Encrypted connections.
- Reduced attack surface.

---

## Azure Bastion Deployment Requirements

Azure Bastion requires a dedicated subnet within the Virtual Network.

Requirements include:

- The subnet must be named exactly **AzureBastionSubnet**.
- The minimum supported subnet size is **/26**.
- No other Azure resources can be deployed in this subnet.

Because Azure Bastion is a managed platform service, administrators should avoid configurations that interfere with its operation, such as blocking required management traffic.

Azure Bastion also requires:

- A Standard SKU Public IP address.
- Deployment within the same Virtual Network as the Virtual Machines it manages.

> [!IMPORTANT]
> Azure Bastion uses a dedicated subnet that is reserved exclusively for the service. It should not host Virtual Machines or other workloads.

---

# Zero Trust Networking

Azure networking follows Zero Trust principles.

Recommendations include:

- Verify every connection.
- Minimize Public IP addresses.
- Use least privilege.
- Inspect traffic.
- Encrypt communications.
- Continuously monitor activity.

---

# Enterprise Scenario

A company deploys a Hub-and-Spoke architecture.

The Hub Virtual Network contains:

- Azure Firewall
- Azure Bastion
- DDoS Protection Standard

Each Spoke Virtual Network uses:

- NSGs
- ASGs
- Private Endpoints
- Private DNS Zones

No production Virtual Machine has a Public IP address.

---

# Best Practices

- Minimize Internet exposure.
- Use NSGs for subnet segmentation.
- Use ASGs instead of IP-based rules.
- Deploy Azure Firewall for centralized filtering.
- Prefer Private Endpoints over public connectivity.
- Use Azure Bastion for administrative access.
- Enable DDoS Protection Standard for Internet-facing workloads.
- Apply Zero Trust principles.

---

# Common Pitfalls

- Allowing unrestricted inbound traffic.
- Using Public IPs unnecessarily.
- Creating overly permissive NSG rules.
- Managing NSGs using individual IP addresses instead of ASGs.
- Confusing Service Endpoints with Private Endpoints.
- Forgetting to monitor firewall activity.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Network Security Groups
> - Application Security Groups
> - Azure Firewall
> - DDoS Protection
> - Service Endpoints
> - Private Endpoints
> - Azure Bastion
> - Zero Trust networking

---

# Key Takeaways

- Azure network security uses multiple complementary services rather than a single security solution.
- NSGs provide traffic filtering at the subnet and NIC level, while Azure Firewall offers centralized, stateful inspection.
- Private Endpoints and Azure Bastion significantly reduce Internet exposure.
- Zero Trust networking minimizes risk by verifying every connection and limiting network access.
- Layered security is the recommended approach for production Azure environments.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure network security documentation | https://learn.microsoft.com/azure/security/fundamentals/network-overview |
| Network Security Groups | https://learn.microsoft.com/azure/virtual-network/network-security-groups-overview |
| Application Security Groups | https://learn.microsoft.com/azure/virtual-network/application-security-groups |
| Azure Firewall | https://learn.microsoft.com/azure/firewall/overview |
| Azure DDoS Protection | https://learn.microsoft.com/azure/ddos-protection/ddos-protection-overview |
| Private Link and Private Endpoints | https://learn.microsoft.com/azure/private-link/private-link-overview |
| Service Endpoints | https://learn.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview |
| Azure Bastion | https://learn.microsoft.com/azure/bastion/bastion-overview |
| Microsoft Learn – Secure your Azure network | https://learn.microsoft.com/training/modules/secure-network-connectivity-azure/ |
