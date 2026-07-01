# Azure Security Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It consolidates Microsoft's recommended security practices across Azure networking, identity, governance, monitoring, workload protection, and infrastructure management. This document serves as the engineering summary of the **Security** pillar and reinforces the principles most frequently evaluated in the AZ-104 certification.

---

# Overview

Security in Azure is based on multiple complementary layers rather than a single protection mechanism.

Microsoft recommends combining identity protection, network security, workload protection, governance, monitoring, encryption, and continuous assessment into a unified **Defense in Depth** strategy.

No single Azure service provides complete protection. Secure Azure environments rely on the interaction of Microsoft Entra ID, Azure RBAC, NSGs, Azure Firewall, Microsoft Defender for Cloud, Azure Policy, Azure Monitor, Key Vault, and many other services working together.

---

# Follow Microsoft's Security Principles

Microsoft recommends applying the following principles across every Azure deployment:

- Zero Trust
- Defense in Depth
- Least Privilege
- Assume Breach
- Continuous Monitoring
- Policy-Driven Governance
- Secure by Default
- Automation First

These principles should guide every architectural decision.

---

# Protect Identities First

Identity is Azure's primary security boundary.

Best practices include:

- Enforce Multi-Factor Authentication (MFA).
- Implement Conditional Access.
- Use Privileged Identity Management (PIM).
- Separate Microsoft Entra ID roles from Azure RBAC roles.
- Grant least privilege.
- Review privileged assignments regularly.
- Maintain emergency ("break-glass") accounts.

Compromised identities remain one of the most common attack vectors in cloud environments.

---

# Secure Network Boundaries

Reduce the attack surface wherever possible.

Recommendations include:

- Use Network Security Groups (NSGs).
- Group workloads with Application Security Groups (ASGs).
- Route traffic through Azure Firewall.
- Protect web applications with Web Application Firewall (WAF).
- Enable Azure DDoS Protection where appropriate.
- Use Azure Bastion instead of exposing RDP or SSH.
- Prefer Private Endpoints over public connectivity.

Public exposure should be minimized whenever possible.

---

# Protect Workloads Continuously

Enable Microsoft Defender for Cloud.

Use it to:

- Improve Secure Score.
- Review recommendations.
- Enable Defender Plans.
- Protect production workloads.
- Monitor regulatory compliance.
- Implement Just-In-Time VM Access.
- Automate remediation workflows.

Security posture should improve continuously.

---

# Use Azure Policy for Governance

Azure Policy should enforce organizational security standards automatically.

Typical uses include:

- Require resource tags.
- Restrict allowed locations.
- Restrict VM SKUs.
- Require encryption.
- Deny public endpoints.
- Audit security settings.
- Deploy required monitoring agents.

Policy-based governance reduces configuration drift.

---

# Protect Secrets Properly

Never store secrets inside:

- Source code
- ARM templates
- Bicep files
- Scripts
- Configuration files

Instead, use Azure Key Vault.

Store:

- Passwords
- Certificates
- Keys
- Connection strings
- Secrets

Applications should authenticate using Managed Identities whenever possible.

---

# Encrypt Data Everywhere

Protect data:

- At rest
- In transit
- During backup

Recommendations include:

- Storage Service Encryption
- Azure Disk Encryption (where applicable)
- TLS for communications
- Customer-managed keys (when required)

Encryption should be enabled by default whenever supported.

---

# Monitor Continuously

Security requires continuous visibility.

Monitor using:

- Azure Monitor
- Activity Log
- Log Analytics
- Microsoft Defender for Cloud
- Microsoft Sentinel

Investigate:

- Authentication failures
- Privileged role activations
- Security alerts
- Resource changes
- Policy compliance

---

# Automate Security Operations

Reduce manual operations through automation.

Examples include:

- Azure Policy remediation
- Defender Workflow Automation
- Azure Logic Apps
- Azure Automation
- Azure Monitor Alerts
- Action Groups

Automation improves consistency and reduces response times.

---

# Secure Administrative Access

Protect privileged administration by:

- Using Azure Bastion.
- Eliminating unnecessary public IP addresses.
- Enabling PIM.
- Enforcing MFA.
- Using dedicated administrative accounts.
- Applying Conditional Access.
- Reviewing privileged activity regularly.

Administrative access should always follow Zero Trust principles.

---

# Keep Resources Updated

Regularly review:

- Secure Score
- Defender recommendations
- Azure Policy compliance
- RBAC assignments
- Defender Plans
- Guest accounts
- Managed Identities
- Monitoring agents

Security posture changes as infrastructure evolves.

---

# Build Security into Deployments

Security should be incorporated into Infrastructure as Code (IaC).

Recommendations include:

- Use ARM Templates or Bicep.
- Validate deployments before execution.
- Store secrets in Azure Key Vault.
- Use secure parameters.
- Apply Azure Policy automatically.
- Review deployments using What-If.

Infrastructure should be secure from deployment through retirement.

---

# Enterprise Security Workflow

```text
Identity Protection

↓

Network Protection

↓

Workload Protection

↓

Continuous Monitoring

↓

Threat Detection

↓

Automated Response

↓

Continuous Improvement
```

Azure security should operate as an ongoing lifecycle rather than a one-time implementation.

---

# Security Checklist

- Implement Zero Trust.
- Enforce MFA.
- Use Conditional Access.
- Apply least privilege.
- Protect secrets with Azure Key Vault.
- Use Managed Identities.
- Secure networks with NSGs and Azure Firewall.
- Enable Microsoft Defender for Cloud.
- Improve Secure Score continuously.
- Govern resources with Azure Policy.
- Monitor continuously.
- Automate remediation.
- Review security posture regularly.

---

# Common Pitfalls

- Assigning excessive permissions.
- Leaving management ports exposed.
- Ignoring Secure Score recommendations.
- Disabling Azure Policy.
- Hardcoding secrets.
- Treating compliance as security.
- Neglecting monitoring.
- Failing to review privileged access.
- Allowing configuration drift.

---

> [!IMPORTANT]
> **AZ-104 Security Summary**
>
> Successful Azure administrators understand that Azure security is built from multiple complementary services rather than a single security product.
>
> Microsoft Entra ID, Azure RBAC, Azure Policy, Network Security Groups, Azure Firewall, Azure Key Vault, Microsoft Defender for Cloud, Azure Monitor, and Microsoft Sentinel work together to implement Zero Trust, Defense in Depth, and Least Privilege across the Azure platform.

---

# Key Takeaways

- Azure security is implemented through a layered Defense in Depth strategy that combines identity, networking, governance, monitoring, workload protection, and encryption.
- Microsoft Entra ID, Azure RBAC, Azure Policy, Microsoft Defender for Cloud, Azure Key Vault, Azure Firewall, and Azure Monitor work together to reduce risk and continuously improve security posture.
- Organizations should automate governance, enforce least privilege, minimize public exposure, protect secrets, and continuously monitor security events throughout the resource lifecycle.
- Secure Azure environments rely on continuous assessment, policy enforcement, automated remediation, and Zero Trust principles rather than isolated security controls.
- Mastering these security practices provides the foundation required for designing secure Azure infrastructures and successfully passing the AZ-104 certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Microsoft Azure Security Documentation | https://learn.microsoft.com/azure/security/ |
| Microsoft Cloud Adoption Framework – Security | https://learn.microsoft.com/azure/cloud-adoption-framework/secure/ |
| Azure Security Benchmark | https://learn.microsoft.com/security/benchmark/azure/ |
| Microsoft Defender for Cloud | https://learn.microsoft.com/azure/defender-for-cloud/ |
| Microsoft Entra ID | https://learn.microsoft.com/entra/fundamentals/ |
| Azure Policy | https://learn.microsoft.com/azure/governance/policy/overview |
| Azure Key Vault | https://learn.microsoft.com/azure/key-vault/general/overview |
| Microsoft Learn – Secure your Azure infrastructure | https://learn.microsoft.com/training/paths/secure-your-azure-services/
