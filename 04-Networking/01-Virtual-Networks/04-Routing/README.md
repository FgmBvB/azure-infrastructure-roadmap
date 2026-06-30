# Azure Routing

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains how Azure routes network traffic, including system routes, user-defined routes (UDRs), route tables, next hops, effective routes, and routing decisions within Azure Virtual Networks.

---

# Overview

Routing determines how network traffic travels between Azure resources, Virtual Networks, on-premises environments, and the Internet.

Azure automatically creates system routes that enable communication within Azure. Administrators can customize routing behavior using **User-Defined Routes (UDRs)** to control traffic flow for security, inspection, or hybrid networking scenarios.

Understanding Azure routing is fundamental for designing secure and scalable Azure networks and is a core objective of the AZ-104 certification.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure routing.
- Differentiate System Routes and User-Defined Routes.
- Configure Route Tables.
- Understand Next Hop types.
- Interpret Effective Routes.
- Design custom routing scenarios.
- Troubleshoot routing problems.

---

# Azure Routing Architecture

```text
                 Azure Virtual Network
                          │
                  Azure Routing Engine
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
        ▼                 ▼                 ▼
  System Routes     User-Defined      BGP Routes
                        Routes
                          │
                    Route Table
                          │
                     Next Hop
```

---

# System Routes

Azure automatically creates system routes for every Virtual Network.

These routes provide connectivity to:

- Local Virtual Network
- Internet
- Virtual Network Peering
- Virtual Network Gateway
- Azure service endpoints

System routes require no administrator intervention.

---

# User-Defined Routes (UDRs)

User-Defined Routes override Azure system routing.

Administrators use UDRs to:

- Inspect traffic through Azure Firewall.
- Redirect traffic to Network Virtual Appliances (NVAs).
- Implement forced tunneling.
- Control hybrid connectivity.
- Customize network paths.

UDRs are stored inside **Route Tables**, which are associated with one or more subnets.

---

# Route Tables

A Route Table contains one or more routing rules.

Each route consists of:

- Address Prefix
- Next Hop Type
- Optional Next Hop IP Address

Example:

| Address Prefix | Next Hop |
|---------------|----------|
| 0.0.0.0/0 | Azure Firewall |
| 10.1.0.0/16 | Virtual Appliance |
| 172.16.0.0/16 | Virtual Network Gateway |

---

## Gateway Route Propagation

Route Tables include an option called **Propagate gateway routes**.

When enabled (default):

- Routes learned through VPN Gateway or ExpressRoute using BGP are automatically added to the subnet.

When disabled:

- BGP-learned routes are ignored for that Route Table.
- Only System Routes and User-Defined Routes are evaluated.

Disabling gateway route propagation is commonly used when:

- Building DMZ architectures.
- Forcing all traffic through Azure Firewall.
- Preventing direct routing to on-premises networks.

> [!TIP]
> Gateway route propagation provides greater flexibility when implementing centralized security and traffic inspection.

---

# Next Hop Types

Azure supports several Next Hop types.

| Next Hop | Purpose |
|-----------|---------|
| Virtual Network | Traffic remains inside the VNet |
| Internet | Internet-bound traffic |
| Virtual Appliance | Network Virtual Appliance (NVA) |
| Virtual Network Gateway | VPN or ExpressRoute |
| None | Drop traffic |

Choosing the appropriate Next Hop determines how packets leave a subnet.

---

## IP Forwarding

By default, Azure Virtual Machines process only traffic addressed to their own network interfaces.

If a Virtual Machine is used as a:

- Network Virtual Appliance (NVA)
- Router
- Firewall
- Proxy

the associated Network Interface must have **IP Forwarding** enabled.

Without IP Forwarding:

- Packets forwarded by User-Defined Routes are discarded.
- Transit traffic cannot pass through the Virtual Machine.

IP Forwarding is configured on the Azure Network Interface (NIC), not inside the guest operating system.

> [!IMPORTANT]
> User-Defined Routes alone are not sufficient for Network Virtual Appliances. IP Forwarding must also be enabled on the NIC.

---

# Effective Routes

Every Network Interface automatically receives an **Effective Route Table**.

Effective Routes combine:

- Azure System Routes
- User-Defined Routes
- BGP Routes

Administrators can view Effective Routes from the Network Interface in the Azure portal.

This feature is commonly used when troubleshooting routing issues.

---

# Route Selection

Azure evaluates routes according to the following principles:

1. Longest Prefix Match.
2. User-Defined Routes override System Routes.
3. BGP Routes may override System Routes depending on the destination.

Example:

```text
Destination:

10.0.1.20

Routes:

10.0.0.0/16
10.0.1.0/24

Selected:

10.0.1.0/24
```

The most specific matching prefix is always selected.

---

## Route Precedence

Azure always evaluates routes using **Longest Prefix Match**.

When multiple routes have the same destination prefix, Azure applies the following precedence:

1. User-Defined Routes (UDRs)
2. BGP Routes
3. System Routes

Example:

```text
Destination:

0.0.0.0/0

Available Routes:

UDR → Azure Firewall

BGP → On-premises Gateway

System Route → Internet
```

Result:

```text
Traffic → Azure Firewall
```

because the User-Defined Route has the highest priority.

> [!IMPORTANT]
> Azure first selects the most specific prefix. Only when multiple routes have the same prefix length does Azure evaluate route precedence.

---

# Forced Tunneling

Forced Tunneling redirects outbound Internet traffic through a centralized security device.

Typical implementations use:

- Azure Firewall
- Network Virtual Appliance
- On-premises firewall through VPN
- On-premises firewall through ExpressRoute

This improves centralized inspection and compliance.

---

# Enterprise Scenario

A company deploys Azure Firewall in a dedicated subnet.

A Route Table is associated with every application subnet.

Default route:

```text
0.0.0.0/0

↓

Azure Firewall
```

All outbound Internet traffic is inspected before leaving Azure.

---

# Best Practices

- Use Azure System Routes whenever possible.
- Use UDRs only when customization is required.
- Document all Route Tables.
- Use Effective Routes for troubleshooting.
- Minimize unnecessary custom routes.
- Centralize Internet inspection using Azure Firewall where appropriate.
- Validate routing after infrastructure changes.

---

# Common Pitfalls

- Forgetting to associate Route Tables with subnets.
- Creating overlapping route prefixes.
- Incorrect Next Hop configuration.
- Breaking Internet connectivity with invalid default routes.
- Assuming UDRs apply automatically to all subnets.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - System Routes
> - User-Defined Routes (UDRs)
> - Route Tables
> - Next Hop Types
> - Effective Routes
> - Longest Prefix Match
> - Forced Tunneling
> - Route troubleshooting

---

# Key Takeaways

- Azure automatically manages routing through System Routes.
- Route Tables allow administrators to customize network traffic.
- Effective Routes combine all applicable routing sources.
- Azure always selects the most specific matching route.
- Proper routing design improves security, scalability, and hybrid connectivity.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure routing overview | https://learn.microsoft.com/azure/virtual-network/virtual-networks-udr-overview |
| Azure route tables | https://learn.microsoft.com/azure/virtual-network/manage-route-table |
| User-defined routes | https://learn.microsoft.com/azure/virtual-network/virtual-networks-udr-overview |
| Effective routes | https://learn.microsoft.com/azure/virtual-network/diagnose-network-routing-problem |
| Azure Virtual Network FAQ | https://learn.microsoft.com/azure/virtual-network/virtual-networks-faq |
| Microsoft Learn – Configure routing and network traffic | https://learn.microsoft.com/training/modules/configure-network-routing-endpoints/ |
