# Identity Security

> [!NOTE]
> This section is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure identity and access management, including Microsoft Entra ID, Azure Role-Based Access Control (RBAC), Multi-Factor Authentication (MFA), Conditional Access, Managed Identities, and Privileged Identity Management (PIM). Identity security is a foundational pillar of Azure's Zero Trust architecture and is essential for securing access to Azure resources.

---

# Overview

Identity is the primary security boundary in Azure.

Microsoft Entra ID authenticates users, applications, and managed identities, while Azure RBAC authorizes access to Azure resources. Together with Conditional Access, MFA, Managed Identities, and Privileged Identity Management, these services implement Microsoft's Zero Trust security model.

Understanding how authentication, authorization, privileged access, and identity governance interact is essential for designing secure Azure environments and is heavily evaluated throughout the AZ-104 certification.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Microsoft Entra ID architecture.
- Differentiate authentication from authorization.
- Understand the differences between Microsoft Entra ID roles and Azure RBAC roles.
- Configure Azure Role-Based Access Control (RBAC).
- Apply the principle of least privilege.
- Understand Managed Identities.
- Implement Multi-Factor Authentication (MFA).
- Configure Conditional Access policies.
- Understand Privileged Identity Management (PIM).
- Apply Microsoft's identity security best practices.

---

# Section Structure

| Document | Description |
|----------|-------------|
| **01 - Overview** | Microsoft Entra ID architecture, authentication, authorization, Azure RBAC, Managed Identities, MFA, Conditional Access, PIM, Zero Trust, identity lifecycle, Microsoft Entra roles vs Azure RBAC, Deny Assignments, Managed Identity lifecycle, and AZ-104 concepts. |
| **02 - Best Practices** | Zero Trust, least privilege, Conditional Access validation, Report-only mode, What If analysis, MFA, PIM, Azure Key Vault integration, Managed Identities, emergency access accounts, access reviews, identity governance, and Microsoft's production recommendations. |

---

# Identity Security Architecture

```text
Users / Applications

↓

Microsoft Entra ID

↓

Authentication

↓

Conditional Access

↓

Multi-Factor Authentication

↓

Azure RBAC

↓

Azure Resources
```

Authentication verifies identities, while Azure RBAC determines what authenticated identities are allowed to do.

---

# Core Identity Services

## Microsoft Entra ID

Azure's cloud identity platform.

Provides:

- User identities
- Group management
- Device identities
- Application identities
- Single Sign-On (SSO)
- Hybrid identity
- Identity governance

---

## Azure Role-Based Access Control (RBAC)

Azure's authorization system.

Controls access using:

- Security Principals
- Role Definitions
- Scopes
- Role Assignments

Implements least privilege across Azure resources.

---

## Managed Identities

Managed identities provide Azure resources with automatically managed identities.

Available types:

- System-assigned
- User-assigned

They eliminate the need to manage credentials inside applications.

---

## Multi-Factor Authentication (MFA)

Provides an additional verification layer beyond passwords.

Common authentication factors include:

- Microsoft Authenticator
- FIDO2 Security Keys
- Windows Hello for Business
- SMS (where supported)

---

## Conditional Access

Evaluates sign-in conditions before granting access.

Policies may evaluate:

- User
- Group
- Device
- Application
- Location
- Risk level

Conditional Access enables adaptive security controls.

---

## Privileged Identity Management (PIM)

Provides just-in-time privileged access.

Capabilities include:

- Eligible assignments
- Temporary activation
- MFA enforcement
- Approval workflows
- Access reviews

PIM reduces standing administrative privileges.

---

# Identity Security Principles

Microsoft recommends:

- Zero Trust
- Least Privilege
- Verify Explicitly
- Assume Breach
- Just-In-Time Administration
- Continuous Access Evaluation

These principles form the foundation of secure Azure identity management.

---

# Typical Identity Flow

```text
User

↓

Microsoft Entra ID

↓

Authentication

↓

Conditional Access

↓

MFA

↓

Azure RBAC

↓

Azure Resource
```

Every request is authenticated before authorization is evaluated.

---

# AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Microsoft Entra ID
- Azure RBAC
- Microsoft Entra roles
- Managed Identities
- Multi-Factor Authentication
- Conditional Access
- Privileged Identity Management
- Least Privilege
- Zero Trust
- Identity governance

---

# Key Takeaways

- Microsoft Entra ID provides centralized identity, authentication, and identity governance services for Azure and cloud applications.
- Azure RBAC controls authorization through role assignments at Management Group, Subscription, Resource Group, and Resource scopes, complementing Microsoft Entra ID rather than replacing it.
- Conditional Access, Multi-Factor Authentication, Managed Identities, and Privileged Identity Management strengthen Azure security by enforcing adaptive access controls and minimizing standing privileges.
- Understanding the distinction between identity management and resource authorization, together with Zero Trust principles and least privilege, is essential for secure Azure administration.
- Identity security is one of the most heavily tested domains in the AZ-104 certification and forms the foundation of every secure Azure environment.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Microsoft Entra ID | https://learn.microsoft.com/entra/fundamentals/ |
| Azure RBAC | https://learn.microsoft.com/azure/role-based-access-control/overview |
| Managed Identities | https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview |
| Conditional Access | https://learn.microsoft.com/entra/identity/conditional-access/overview |
| Microsoft Entra MFA | https://learn.microsoft.com/entra/identity/authentication/concept-mfa-howitworks |
| Privileged Identity Management | https://learn.microsoft.com/entra/id-governance/privileged-identity-management/ |
| Microsoft Learn – Secure access to Azure resources | https://learn.microsoft.com/training/modules/secure-access-azure-resources/ |
