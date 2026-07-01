# Security

> [!NOTE]
> This section is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers the core security services used to protect Azure environments, including network security, identity and access management, cloud security posture management, workload protection, and Microsoft's recommended security practices. Together, these services implement Azure's **Defense in Depth** and **Zero Trust** security models.

---

# Overview

Security is a fundamental pillar of every Azure deployment.

Rather than relying on a single security product, Azure provides multiple integrated services that protect identities, networks, workloads, data, and infrastructure throughout the entire resource lifecycle.

This module introduces the security mechanisms most frequently encountered by Azure administrators and explains how they work together to build resilient, production-ready environments.

Understanding these services—and knowing when to use each one—is essential for designing secure Azure architectures and for successfully passing the **AZ-104** certification.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure's layered security architecture.
- Secure Azure networking using native security services.
- Protect identities with Microsoft Entra ID and Azure RBAC.
- Implement Zero Trust and Least Privilege principles.
- Understand Microsoft Defender for Cloud.
- Interpret Secure Score and security recommendations.
- Apply Azure security best practices.
- Reduce attack surfaces across Azure environments.
- Design secure production-ready Azure infrastructures.

---

# Section Structure

| Section | Description |
|----------|-------------|
| **01 - Network Security** | Network Security Groups (NSGs), Application Security Groups (ASGs), Azure Firewall, Web Application Firewall (WAF), Azure DDoS Protection, Private Endpoints, Azure Bastion, network segmentation, and secure connectivity. |
| **02 - Identity Security** | Microsoft Entra ID, Azure RBAC, Managed Identities, Multi-Factor Authentication (MFA), Conditional Access, Privileged Identity Management (PIM), Zero Trust, and identity governance. |
| **03 - Microsoft Defender for Cloud** | Cloud Security Posture Management (CSPM), Cloud Workload Protection (CWPP), Secure Score, Defender Plans, Azure Policy integration, Just-In-Time VM Access, Workflow Automation, Regulatory Compliance, and continuous security assessment. |
| **04 - Best Practices** | Microsoft's recommended security architecture, Zero Trust, Defense in Depth, least privilege, governance, monitoring, workload protection, encryption, automation, and production security recommendations. |

---

# Azure Security Architecture

```text
Users & Applications

↓

Microsoft Entra ID

↓

Authentication & Authorization

↓

Network Security

↓

Azure Resources

↓

Microsoft Defender for Cloud

↓

Monitoring & Continuous Improvement
```

Azure security is implemented through multiple complementary layers that protect identities, communications, workloads, and infrastructure.

---

# Core Security Domains

## Identity Security

Protects users, administrators, applications, and managed identities through authentication, authorization, and identity governance.

---

## Network Security

Protects communications using segmentation, traffic filtering, private connectivity, and perimeter security services.

---

## Workload Protection

Continuously monitors Azure resources, detects threats, and provides actionable security recommendations.

---

## Governance

Enforces organizational security standards through Azure Policy, RBAC, monitoring, and automated remediation.

---

# Security Design Principles

Microsoft recommends designing Azure environments according to these principles:

- Zero Trust
- Defense in Depth
- Least Privilege
- Assume Breach
- Continuous Monitoring
- Policy-Driven Governance
- Secure by Default
- Automation First

These principles should guide every security decision regardless of workload or architecture.

---

# AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Network Security
- Microsoft Entra ID
- Azure RBAC
- Multi-Factor Authentication (MFA)
- Conditional Access
- Managed Identities
- Privileged Identity Management (PIM)
- Microsoft Defender for Cloud
- Secure Score
- Azure Policy integration
- Zero Trust
- Defense in Depth
- Security best practices

---

# Key Takeaways

- Azure security is built on a layered **Defense in Depth** architecture that combines identity, network, workload, governance, and monitoring services.
- Microsoft Entra ID, Azure RBAC, Azure networking security services, and Microsoft Defender for Cloud work together to reduce risk and protect Azure resources throughout their lifecycle.
- Zero Trust, Least Privilege, continuous assessment, policy-driven governance, and automated remediation form the foundation of Microsoft's cloud security strategy.
- Secure Azure environments require coordinated protection across identities, communications, workloads, and operational processes rather than relying on isolated security controls.
- Mastering these security concepts is essential for designing secure Azure infrastructures and successfully passing the **AZ-104** certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Security Documentation | https://learn.microsoft.com/azure/security/ |
| Microsoft Cloud Adoption Framework – Secure | https://learn.microsoft.com/azure/cloud-adoption-framework/secure/ |
| Azure Security Benchmark | https://learn.microsoft.com/security/benchmark/azure/ |
| Microsoft Defender for Cloud | https://learn.microsoft.com/azure/defender-for-cloud/ |
| Microsoft Entra ID | https://learn.microsoft.com/entra/fundamentals/ |
| Azure Policy | https://learn.microsoft.com/azure/governance/policy/overview |
| Microsoft Learn – Secure your Azure infrastructure | https://learn.microsoft.com/training/paths/secure-your-azure-services/
