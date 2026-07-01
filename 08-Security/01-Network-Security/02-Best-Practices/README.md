# Network Security Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for designing, implementing, and maintaining secure Azure network environments using native Azure networking security services.

---

# Overview

Azure network security should follow a layered **Defense in Depth** approach.

No single security service protects every workload. Instead, Microsoft recommends combining multiple security controls to reduce the attack surface while maintaining operational flexibility.

A well-designed Azure network uses segmentation, least privilege, centralized filtering, and continuous monitoring to protect resources.

---

# Follow the Defense in Depth Model

Apply multiple independent security layers.

Typical architecture:

```text
Internet

↓

Azure DDoS Protection

↓

Azure Firewall / WAF

↓

Virtual Network

↓

NSGs

↓

Application Workloads

↓

Data
```

Each layer protects against different attack vectors.

---

# Apply Least Privilege

Only allow the traffic that is strictly required.

Avoid:

- Any-to-Any rules
- Broad IP ranges
- Unrestricted inbound access

Prefer explicit allow rules followed by an implicit deny model.

---

# Segment Networks

Separate workloads according to their function.

Typical segmentation includes:

- Web tier
- Application tier
- Database tier
- Management subnet
- Shared services

Segmentation limits lateral movement during security incidents.

---

# Use Network Security Groups

Use NSGs to filter traffic at both:

- Subnet level
- Network Interface (NIC) level

Create small, well-defined rules instead of broad allow rules.

Review NSGs regularly to remove obsolete rules.

---

# Simplify Rules with Application Security Groups

Use Application Security Groups (ASGs) instead of individual IP addresses whenever possible.

Benefits include:

- Simpler rule management
- Better readability
- Easier scalability
- Reduced administrative overhead

Organize ASGs by application role rather than infrastructure.

---

# Centralize Traffic Inspection

Use Azure Firewall for centralized filtering.

Azure Firewall is recommended when organizations require:

- Central outbound filtering
- DNAT
- Threat Intelligence
- FQDN filtering
- Central security policies

Avoid managing identical NSG rules across multiple virtual networks.

---

# Route Traffic Through Azure Firewall

Deploying Azure Firewall inside a Virtual Network does **not** automatically redirect traffic through the firewall.

To inspect traffic, administrators must configure **User Defined Routes (UDRs)**.

A common configuration includes:

- Destination: **0.0.0.0/0**
- Next Hop Type: **Virtual Appliance**
- Next Hop Address: **Azure Firewall private IP**

The route table is then associated with the required subnets.

```text
Virtual Machine

↓

User Defined Route (UDR)

↓

Azure Firewall

↓

Internet
```

Without appropriate routing, traffic bypasses Azure Firewall entirely.

> [!IMPORTANT]
> Azure Firewall protects only the traffic that is explicitly routed through it.

---

# Protect Internet-Facing Applications

Use Web Application Firewall (WAF) for HTTP and HTTPS workloads.

WAF protects against:

- SQL Injection
- Cross-Site Scripting (XSS)
- OWASP Top 10 attacks
- Protocol violations

Deploy WAF in Prevention mode after validating application behavior.

---

# Protect Against DDoS Attacks

Enable Azure DDoS Protection for critical Internet-facing workloads.

Benefits include:

- Automatic mitigation
- Adaptive tuning
- Attack telemetry
- Cost protection
- Continuous monitoring

Combine DDoS Protection with Azure Firewall and WAF for layered protection.

---

# Azure DDoS Protection Options

Azure provides different deployment options for DDoS Protection depending on workload requirements.

**DDoS Network Protection**

- Applied at the Virtual Network level.
- Protects all eligible public IP resources within the protected Virtual Network.
- Designed for enterprise-scale environments.

**DDoS IP Protection**

- Applied to individual Public IP addresses.
- Suitable for protecting specific Internet-facing resources.
- Provides a more granular deployment option.

Administrators should choose the protection model that best aligns with the organization's architecture and operational requirements.

---

# Minimize Public Exposure

Avoid assigning public IP addresses unless absolutely necessary.

Whenever possible, use:

- Private Endpoints
- Azure Bastion
- VPN Gateway
- ExpressRoute

Private connectivity significantly reduces the attack surface.

---

# Secure Administrative Access with Azure Bastion

Microsoft recommends Azure Bastion instead of exposing Remote Desktop (RDP) or Secure Shell (SSH) directly to the Internet.

Azure Bastion requires a dedicated subnet named:

```text
AzureBastionSubnet
```

For current Bastion SKUs, Microsoft recommends a subnet size of **/26 or larger** to support scaling.

Using Azure Bastion provides several security benefits:

- No public IP addresses on virtual machines.
- No inbound RDP (3389) exposure.
- No inbound SSH (22) exposure.
- Browser-based management over HTTPS (443).
- Reduced attack surface.

Administrators can therefore keep management ports closed to Internet traffic while maintaining secure administrative access.

---

# Use Private Endpoints for PaaS

Prefer Private Endpoints over public endpoints.

Benefits include:

- Private IP connectivity
- Private DNS integration
- No Internet exposure
- Reduced data exfiltration risk

Disable public network access whenever workload requirements allow.

---

# Monitor Network Security

Enable monitoring for security resources.

Review:

- NSG Flow Logs (where available and supported)
- Azure Firewall logs
- WAF logs
- DDoS reports
- Azure Monitor alerts

Monitoring is essential for detecting abnormal traffic patterns.

---

# Apply Consistent Naming

Use standardized naming conventions.

Include:

- Environment
- Application
- Region
- Security function

Consistent naming improves administration and troubleshooting.

---

# Review Rules Regularly

Security rules should evolve with the environment.

Regularly:

- Remove unused rules.
- Reduce unnecessary permissions.
- Validate priorities.
- Review exceptions.

Avoid accumulating legacy firewall rules.

---

# Secure Hybrid Connectivity

For hybrid environments:

- Minimize exposed services.
- Inspect traffic where appropriate.
- Apply consistent policies across Azure and on-premises.
- Protect VPN and ExpressRoute gateways.

Hybrid security should follow the same Zero Trust principles as cloud-native deployments.

---

# Validate Security Changes

Before modifying production security rules:

- Review dependencies.
- Validate expected traffic flows.
- Test in non-production when possible.
- Monitor after deployment.

Small firewall changes can have significant operational impact.

---

# Enterprise Scenario

A multinational organization hosts a three-tier application in Azure.

Administrators implement:

- Azure DDoS Protection for Internet-facing resources.
- Web Application Firewall protecting the application gateway.
- Azure Firewall for centralized ingress and egress filtering.
- NSGs on every subnet.
- Application Security Groups separating Web, Application, and Database tiers.
- Private Endpoints for Azure SQL Database and Storage Accounts.
- Azure Bastion for administrative access.
- Continuous monitoring through Azure Monitor and Microsoft Defender for Cloud.

This layered architecture minimizes the attack surface while maintaining operational flexibility.

---

# Best Practices Checklist

- Follow Defense in Depth.
- Apply least privilege.
- Segment networks.
- Use NSGs at subnet and NIC levels.
- Simplify rules with ASGs.
- Centralize filtering with Azure Firewall.
- Protect web applications with WAF.
- Enable DDoS Protection where appropriate.
- Minimize public exposure.
- Prefer Private Endpoints for PaaS.
- Monitor network security continuously.
- Apply consistent naming conventions.
- Review security rules regularly.
- Secure hybrid connectivity.
- Validate security changes before production.

---

# Common Pitfalls

- Allowing unnecessary inbound ports.
- Using overly permissive NSG rules.
- Exposing management ports directly to the Internet.
- Relying only on perimeter firewalls.
- Leaving PaaS services publicly accessible.
- Ignoring outbound traffic controls.
- Failing to review obsolete security rules.
- Deploying Internet-facing workloads without DDoS Protection or WAF.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Defense in Depth
> - Network segmentation
> - NSGs
> - ASGs
> - Azure Firewall
> - Web Application Firewall
> - Azure DDoS Protection
> - Private Endpoints
> - Azure Bastion
> - Hybrid network security
> - Least privilege
> - Secure network architecture

---

# Key Takeaways

- Azure network security relies on multiple complementary security services rather than a single perimeter device.
- Microsoft recommends combining Network Security Groups, Azure Firewall, Web Application Firewall, Azure DDoS Protection, and Private Endpoints to implement a layered Defense in Depth strategy.
- Secure network architectures minimize public exposure, apply least-privilege access, segment workloads, and continuously monitor network activity.
- Regular rule reviews, centralized traffic inspection, and private connectivity improve both security and operational consistency.
- Following Microsoft's network security best practices helps protect Azure workloads while covering key objectives of the AZ-104 certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Network Security | https://learn.microsoft.com/azure/security/fundamentals/network-overview |
| Network Security Groups | https://learn.microsoft.com/azure/virtual-network/network-security-groups-overview |
| Azure Firewall | https://learn.microsoft.com/azure/firewall/overview |
| Azure DDoS Protection | https://learn.microsoft.com/azure/ddos-protection/ddos-protection-overview |
| Azure Web Application Firewall | https://learn.microsoft.com/azure/web-application-firewall/overview |
| Private Link and Private Endpoints | https://learn.microsoft.com/azure/private-link/private-link-overview |
| Microsoft Defender for Cloud | https://learn.microsoft.com/azure/defender-for-cloud/ |
| Microsoft Learn – Secure your Azure network infrastructure | https://learn.microsoft.com/training/modules/secure-network-connectivity-azure/
