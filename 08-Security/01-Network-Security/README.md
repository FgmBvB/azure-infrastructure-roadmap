# Network Security

> [!NOTE]
> This section is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers the Azure networking security services used to protect workloads, control network traffic, isolate resources, and implement secure communication across Azure environments.

---

# Overview

Network security is one of the core pillars of Azure infrastructure.

Microsoft provides multiple security services that work together to protect resources at different layers of the network stack. Rather than relying on a single security appliance, Azure follows a **Defense in Depth** strategy by combining traffic filtering, segmentation, perimeter protection, private connectivity, and continuous monitoring.

Understanding how these services complement each other is essential for designing secure Azure architectures and is heavily evaluated throughout the AZ-104 certification.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure's layered network security model.
- Configure Network Security Groups (NSGs).
- Understand Application Security Groups (ASGs).
- Design secure network segmentation.
- Understand Azure Firewall architecture.
- Protect applications with Web Application Firewall (WAF).
- Protect Internet-facing workloads with Azure DDoS Protection.
- Secure Azure PaaS services using Private Endpoints.
- Secure administrative access with Azure Bastion.
- Apply Microsoft's network security best practices.

---

# Section Structure

| Document | Description |
|----------|-------------|
| **01 - Overview** | Azure network security architecture, Defense in Depth, NSGs, ASGs, Azure Firewall, WAF, Azure DDoS Protection, Private Endpoints, security layers, default NSG rules, NSG evaluation order, and AZ-104 concepts. |
| **02 - Best Practices** | Network segmentation, Azure Firewall with UDRs, Azure Bastion, Private Endpoints, DDoS Protection, least privilege, monitoring, hybrid security, and Microsoft's production recommendations. |

---

# Azure Network Security Architecture

```text
Internet

↓

Azure DDoS Protection

↓

Azure Firewall / Application Gateway (WAF)

↓

Virtual Network (VNet)

↓

Network Security Groups (NSGs)

↓

Application Security Groups (ASGs)

↓

Virtual Machines
Containers
PaaS Resources
```

Each layer protects against different attack vectors and contributes to a secure Azure environment.

---

# Core Security Services

## Network Security Groups (NSGs)

Layer 3 and Layer 4 packet filtering.

Typical capabilities:

- Allow and deny rules
- Stateful inspection
- Inbound filtering
- Outbound filtering
- Subnet protection
- NIC protection

---

## Application Security Groups (ASGs)

Logical grouping of workloads.

Benefits include:

- Simpler NSG rules
- Improved readability
- Easier management
- Better scalability

---

## Azure Firewall

Centralized managed firewall service.

Capabilities include:

- Network rules
- Application rules
- DNAT
- Threat Intelligence
- Centralized outbound filtering
- Fully managed high availability

---

## Web Application Firewall (WAF)

Application-layer protection for web workloads.

Protects against:

- SQL Injection
- Cross-Site Scripting (XSS)
- OWASP Top 10 attacks
- Protocol violations

---

## Azure DDoS Protection

Protection against volumetric attacks.

Provides:

- Automatic mitigation
- Adaptive tuning
- Attack telemetry
- Continuous monitoring

---

## Private Endpoints

Private access to Azure PaaS services.

Benefits include:

- Private IP connectivity
- No Internet exposure
- Private DNS integration
- Reduced attack surface

---

## Azure Bastion

Secure browser-based administration for virtual machines.

Benefits include:

- No public IP required on VMs
- Secure RDP and SSH over HTTPS
- Reduced attack surface
- Browser-based access

---

# Typical Security Flow

```text
Internet

↓

Azure DDoS Protection

↓

Azure Firewall / WAF

↓

NSG

↓

Azure Resource
```

Multiple security controls inspect traffic before it reaches the destination workload.

---

# Design Principles

Microsoft recommends following these principles:

- Defense in Depth
- Least Privilege
- Zero Trust
- Default Deny
- Explicit Allow
- Network Segmentation
- Minimize Public Exposure

---

# AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Network Security Groups
- Application Security Groups
- Azure Firewall
- Azure Bastion
- Azure DDoS Protection
- Web Application Firewall
- Private Endpoints
- Network segmentation
- Defense in Depth
- Secure Azure networking

---

# Key Takeaways

- Azure network security combines multiple complementary services that operate at different layers of the network stack to implement a Defense in Depth strategy.
- Network Security Groups, Application Security Groups, Azure Firewall, Web Application Firewall, Azure DDoS Protection, Private Endpoints, and Azure Bastion each solve different security challenges and are often deployed together.
- Secure Azure network architectures rely on segmentation, least privilege, private connectivity, centralized traffic inspection, and continuous monitoring rather than a single perimeter device.
- Understanding how Azure networking security services interact—including NSG processing, Azure Firewall routing, Bastion access, and private connectivity—is essential for designing secure infrastructures.
- Mastering Azure network security concepts is a major objective of the AZ-104 certification and a foundational skill for Azure administrators.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Network Security | https://learn.microsoft.com/azure/security/fundamentals/network-overview |
| Network Security Groups | https://learn.microsoft.com/azure/virtual-network/network-security-groups-overview |
| Azure Firewall | https://learn.microsoft.com/azure/firewall/overview |
| Azure DDoS Protection | https://learn.microsoft.com/azure/ddos-protection/ddos-protection-overview |
| Azure Web Application Firewall | https://learn.microsoft.com/azure/web-application-firewall/overview |
| Private Link | https://learn.microsoft.com/azure/private-link/private-link-overview |
| Azure Bastion | https://learn.microsoft.com/azure/bastion/bastion-overview |
| Microsoft Learn – Secure your Azure network infrastructure | https://learn.microsoft.com/training/modules/secure-network-connectivity-azure/
