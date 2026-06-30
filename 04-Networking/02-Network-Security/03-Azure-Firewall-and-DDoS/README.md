# Azure Firewall and DDoS Protection

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains Azure Firewall, Azure DDoS Protection, firewall rule processing, threat intelligence, DNAT/SNAT, forced tunneling, and Microsoft's recommended practices for protecting Azure network infrastructures.

---

# Overview

Azure Firewall and Azure DDoS Protection provide complementary layers of network security.

While **Azure Firewall** filters and controls network traffic at Layers 3–7, **Azure DDoS Protection** mitigates large-scale denial-of-service attacks before they reach Azure resources.

Together they provide centralized traffic inspection, Internet protection, and secure connectivity for Azure workloads.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure Firewall.
- Differentiate Azure Firewall and Network Security Groups.
- Understand Azure DDoS Protection.
- Configure firewall rule collections.
- Understand DNAT and SNAT.
- Configure forced tunneling.
- Apply Microsoft networking security best practices.

---

# Azure Security Architecture

```text
                        Internet
                            │
                            ▼
             Azure DDoS Network Protection
                            │
                            ▼
                    Azure Firewall
                            │
      ┌─────────────────────┼─────────────────────┐
      │                     │                     │
      ▼                     ▼                     ▼
 Application          Virtual Machines      Azure PaaS
      │
      ▼
Virtual Network
```

---

# Azure Firewall

Azure Firewall is a fully managed, cloud-native, stateful firewall service.

Microsoft manages:

- High availability
- Scaling
- Platform updates
- Availability Zones (supported regions)

Administrators manage:

- Firewall rules
- Logging
- Threat Intelligence
- Routing
- Security policies

---

# Azure Firewall Features

Azure Firewall provides:

- Stateful packet inspection
- Network filtering
- Application filtering
- FQDN filtering
- Outbound SNAT
- Inbound DNAT
- Threat Intelligence
- TLS inspection (Premium)
- Intrusion Detection and Prevention (Premium)
- Centralized logging

---

# Firewall Rule Types

Azure Firewall evaluates three primary rule types.

| Rule Type | Purpose |
|------------|---------|
| Network Rules | IP addresses, ports and protocols |
| Application Rules | HTTP/HTTPS traffic using FQDNs |
| NAT Rules | Publish internal services through Public IP addresses |

---

# DNAT vs SNAT

Azure Firewall supports both destination and source address translation.

### Destination NAT (DNAT)

Used for inbound traffic.

Example:

```text
Internet

↓

52.x.x.x

↓

Azure Firewall

↓

10.0.1.4
```

The firewall translates the destination address to an internal resource.

---

### Source NAT (SNAT)

Used for outbound traffic.

Example:

```text
10.0.2.5

↓

Azure Firewall

↓

40.x.x.x

↓

Internet
```

Azure Firewall replaces the private source address with its public IP.

---

# Threat Intelligence

Azure Firewall integrates with Microsoft Threat Intelligence.

Available modes:

| Mode | Description |
|------|-------------|
| Alert | Log suspicious traffic |
| Alert and Deny | Log and block malicious traffic |
| Off | Threat Intelligence disabled |

Threat Intelligence uses Microsoft's global security intelligence feeds.

---

# Azure Firewall Premium

Azure Firewall Premium extends the Standard SKU with advanced security features.

Additional capabilities include:

- TLS inspection
- Intrusion Detection and Prevention System (IDPS)
- URL filtering
- Web categories

Premium is recommended for environments requiring advanced threat protection.

---

# Azure DDoS Protection

Azure automatically provides infrastructure-level DDoS protection for all public Azure resources.

Organizations can enable **Azure DDoS Network Protection** for enhanced capabilities.

Benefits include:

- Automatic attack detection
- Layer 3 and Layer 4 attack mitigation
- Real-time attack telemetry
- Attack analytics
- Cost protection during attacks

Azure DDoS Network Protection is associated with one or more Virtual Networks.

---

# Azure Firewall vs NSG

| Feature | Azure Firewall | Network Security Group |
|----------|----------------|------------------------|
| Stateful | Yes | Yes |
| Layer 7 Filtering | Yes | No |
| FQDN Filtering | Yes | No |
| Centralized | Yes | No |
| Threat Intelligence | Yes | No |
| Application Rules | Yes | No |
| Subnet/NIC Filtering | No | Yes |

NSGs protect individual subnets and network interfaces.

Azure Firewall provides centralized inspection for the entire network.

---

# Forced Tunneling

Many organizations require all outbound traffic to pass through Azure Firewall.

Typical architecture:

```text
Virtual Machine

↓

Route Table (0.0.0.0/0)

↓

Azure Firewall

↓

Internet
```

This architecture enables:

- Centralized inspection
- Logging
- Compliance
- Traffic control

---

# Enterprise Scenario

A financial institution deploys:

- Azure DDoS Network Protection
- Azure Firewall Premium
- Hub-and-Spoke networking
- Private Endpoints
- Azure Bastion

All Internet-bound traffic is inspected by Azure Firewall.

Only approved outbound destinations are allowed.

Threat Intelligence blocks known malicious IP addresses automatically.

---

# Best Practices

- Deploy Azure Firewall in a Hub Virtual Network.
- Use Forced Tunneling where appropriate.
- Enable Threat Intelligence.
- Prefer Azure Firewall Premium for critical workloads.
- Enable Azure DDoS Network Protection for Internet-facing applications.
- Centralize firewall management.
- Monitor firewall logs continuously.
- Protect administrative access using Azure Bastion.

---

# Common Pitfalls

- Confusing Azure Firewall with NSGs.
- Publishing unnecessary inbound services.
- Forgetting Route Tables when deploying Azure Firewall.
- Allowing unrestricted outbound traffic.
- Ignoring firewall diagnostics.
- Assuming DDoS Protection replaces Azure Firewall.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Firewall
> - Azure Firewall Premium
> - Firewall rule types
> - DNAT
> - SNAT
> - Threat Intelligence
> - Azure DDoS Network Protection
> - Forced Tunneling
> - Azure Firewall vs NSGs

---

# Key Takeaways

- Azure Firewall provides centralized, stateful network security for Azure environments.
- Azure DDoS Network Protection mitigates volumetric attacks before they reach workloads.
- Firewall rules control inbound and outbound traffic using network, application, and NAT rule collections.
- Forced Tunneling centralizes Internet traffic inspection and improves security.
- Azure Firewall and NSGs are complementary technologies and should be used together in production architectures.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Firewall documentation | https://learn.microsoft.com/azure/firewall/overview |
| Azure Firewall Premium | https://learn.microsoft.com/azure/firewall/premium-features |
| Azure Firewall rule processing | https://learn.microsoft.com/azure/firewall/rule-processing |
| Azure Firewall forced tunneling | https://learn.microsoft.com/azure/firewall/forced-tunneling |
| Azure DDoS Protection | https://learn.microsoft.com/azure/ddos-protection/ddos-protection-overview |
| Azure network security | https://learn.microsoft.com/azure/security/fundamentals/network-overview |
| Microsoft Learn – Secure network connectivity in Azure | https://learn.microsoft.com/training/modules/secure-network-connectivity-azure/ |
