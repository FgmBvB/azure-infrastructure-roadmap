# Network Security Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Network Security services and concepts used to protect Azure resources, control network traffic, enforce segmentation, and secure communication between workloads.

---

# Overview

Network security is a fundamental pillar of Azure infrastructure.

Azure provides multiple services that work together to control network traffic, protect workloads from external attacks, isolate resources, and enforce organizational security policies.

Rather than relying on a single security appliance, Azure implements a layered security model where multiple services protect different layers of the network stack.

Understanding how these services interact is essential for designing secure Azure environments and is a major objective of the AZ-104 certification.

---

# Network Security Architecture

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

Each layer provides a different level of protection, forming a Defense in Depth security model.

---

# Security Layers

Azure network security combines multiple technologies.

## Network Security Groups (NSGs)

NSGs filter inbound and outbound traffic.

Capabilities include:

- Allow rules
- Deny rules
- Priority evaluation
- Stateful filtering
- Subnet protection
- NIC protection

NSGs provide Layer 3 and Layer 4 filtering.

---

## Application Security Groups (ASGs)

ASGs simplify NSG rule management.

Instead of filtering by IP addresses, administrators group workloads logically.

Example:

- Web Servers
- Application Servers
- Database Servers

ASGs improve scalability and readability.

---

## Azure Firewall

Azure Firewall is Microsoft's managed firewall service.

Capabilities include:

- Centralized filtering
- Network rules
- Application rules
- DNAT
- Threat Intelligence
- High availability

Azure Firewall protects traffic entering and leaving Azure networks.

---

## Azure DDoS Protection

Azure DDoS Protection mitigates distributed denial-of-service attacks.

Features include:

- Automatic attack detection
- Adaptive tuning
- Traffic scrubbing
- Telemetry
- Attack analytics

It protects public IP resources from volumetric attacks.

---

## Web Application Firewall (WAF)

Azure Web Application Firewall protects web applications.

Typical attacks blocked include:

- SQL Injection
- Cross-Site Scripting (XSS)
- Command Injection
- Protocol violations

WAF operates at Layer 7.

---

## Private Endpoints

Private Endpoints provide private access to Azure PaaS services.

Benefits include:

- Private IP connectivity
- No public Internet exposure
- Integration with Private DNS
- Improved security posture

---

# Defense in Depth

Azure follows a layered security strategy.

```text
Identity

↓

Network

↓

Compute

↓

Application

↓

Data
```

Each layer contributes to the overall security posture.

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

Traffic is evaluated by multiple security controls before reaching the destination workload.

---

# Common Security Principles

Microsoft recommends:

- Least Privilege
- Defense in Depth
- Zero Trust
- Network Segmentation
- Default Deny
- Explicit Allow
- Secure by Default

These principles guide Azure network security design.

---

# Design Considerations

When designing secure Azure networks, administrators should consider:

- Internet exposure
- East-West traffic
- North-South traffic
- Hybrid connectivity
- Private access
- High availability
- Regulatory compliance

Security controls should be selected according to workload requirements.

---

# Enterprise Scenario

A company deploys a three-tier application in Azure.

The architecture includes:

- Azure DDoS Protection for Internet-facing resources.
- Azure Firewall for centralized network filtering.
- NSGs to restrict subnet communication.
- ASGs to simplify security rules.
- WAF protecting the web application.
- Private Endpoints for Azure SQL and Storage.

Each security layer protects against different attack vectors while maintaining controlled communication between application components.

---

# Common Pitfalls

- Opening unnecessary inbound ports.
- Using overly permissive NSG rules.
- Relying only on NSGs for perimeter security.
- Exposing PaaS services publicly when Private Endpoints are available.
- Ignoring outbound traffic filtering.
- Not implementing network segmentation.
- Assuming Azure automatically secures every workload.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Network Security Groups
> - Application Security Groups
> - Azure Firewall
> - Azure DDoS Protection
> - Web Application Firewall
> - Private Endpoints
> - Defense in Depth
> - Network segmentation
> - Secure network design

---

# Key Takeaways

- Azure network security is built on a layered Defense in Depth model that combines multiple services to protect workloads and control traffic.
- Network Security Groups and Application Security Groups provide Layer 3 and Layer 4 filtering, while Azure Firewall and Web Application Firewall extend protection to more advanced scenarios.
- Azure DDoS Protection safeguards Internet-facing resources against volumetric attacks, and Private Endpoints eliminate unnecessary public exposure of PaaS services.
- Secure Azure network design relies on segmentation, least privilege, default-deny principles, and selecting the appropriate security controls for each workload.
- Understanding how Azure networking security services complement each other is essential for designing secure infrastructures and for success in the AZ-104 certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Network Security | https://learn.microsoft.com/azure/security/fundamentals/network-overview |
| Network Security Groups | https://learn.microsoft.com/azure/virtual-network/network-security-groups-overview |
| Azure Firewall | https://learn.microsoft.com/azure/firewall/overview |
| Azure DDoS Protection | https://learn.microsoft.com/azure/ddos-protection/ddos-protection-overview |
| Azure Web Application Firewall | https://learn.microsoft.com/azure/web-application-firewall/overview |
| Private Endpoint | https://learn.microsoft.com/azure/private-link/private-endpoint-overview |
| Microsoft Learn – Secure your Azure network infrastructure | https://learn.microsoft.com/training/modules/secure-network-connectivity-azure/
