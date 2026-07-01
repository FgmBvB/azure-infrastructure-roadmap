# Identity Security Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure identity and access management concepts, including Microsoft Entra ID, Azure RBAC, Managed Identities, Multi-Factor Authentication (MFA), Conditional Access, and Privileged Identity Management (PIM). These services protect identities, control access to Azure resources, and implement Zero Trust security principles.

---

# Overview

Identity is the first security boundary in Azure.

Rather than trusting users or devices based on their network location, Azure adopts a **Zero Trust** model where every authentication and authorization request is continuously evaluated.

Microsoft Entra ID serves as the identity provider for Azure and integrates authentication, authorization, policy enforcement, and identity governance across cloud resources.

Understanding Azure identity security is essential for securing Azure environments and is a major objective of the AZ-104 certification.

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

Multi-Factor Authentication (MFA)

↓

Azure RBAC

↓

Azure Resources
```

Authentication verifies identity, while authorization determines what authenticated identities are allowed to do.

---

# Core Identity Services

## Microsoft Entra ID

Microsoft Entra ID is Azure's cloud identity and access management service.

Capabilities include:

- User authentication
- Device identities
- Application identities
- Single Sign-On (SSO)
- Hybrid identity
- Identity governance

Microsoft Entra ID authenticates users before access decisions are evaluated.

---

## Azure Role-Based Access Control (RBAC)

Azure RBAC controls access to Azure resources.

RBAC assignments consist of:

- Security Principal
- Role Definition
- Scope

Common built-in roles include:

- Owner
- Contributor
- Reader
- User Access Administrator

Azure RBAC implements the principle of least privilege.

---

# Microsoft Entra Roles vs Azure RBAC

Microsoft Entra ID roles and Azure RBAC roles serve different purposes.

Although they both grant permissions, they operate on different control planes.

| Microsoft Entra ID Roles | Azure RBAC Roles |
|---------------------------|------------------|
| Manage identities and directory services | Manage Azure resources |
| Apply at the tenant level | Apply at Management Group, Subscription, Resource Group, or Resource level |
| Evaluated by Microsoft Entra ID | Evaluated by Azure Resource Manager (ARM) |
| Examples: Global Administrator, User Administrator | Examples: Owner, Contributor, Reader |

A Microsoft Entra administrator does **not** automatically receive permissions to manage Azure resources.

Likewise, an Azure subscription Owner does **not** automatically gain permissions to administer Microsoft Entra ID.

---

## Emergency Access

A **Global Administrator** can temporarily elevate access to Azure resources by enabling:

```text
Access management for Azure resources
```

This option assigns the **User Access Administrator** role at the root scope, allowing recovery of orphaned Azure RBAC permissions.

> [!IMPORTANT]
> Microsoft Entra ID manages identities, while Azure RBAC manages Azure resources. Understanding this distinction is essential for the AZ-104 exam.

---

# Deny Assignments

Azure authorization follows a **deny-overrides-allow** model.

Although Azure RBAC is primarily based on allow permissions, Azure also supports **Deny Assignments**.

Key characteristics:

- Created automatically by certain Azure services.
- Read-only from an administrator perspective.
- Cannot be manually created using standard Azure RBAC.
- Override any allow permission.

If a Deny Assignment blocks an operation, the action is denied even if the user holds the **Owner** role.

Typical scenarios include:

- Azure Deployment Stacks
- Azure Managed Applications
- Other Azure-managed protection mechanisms

> [!IMPORTANT]
> Explicit deny permissions always take precedence over allow permissions.

---


## Managed Identities

Managed Identities eliminate the need to store credentials inside applications.

Two types are available:

- System-assigned
- User-assigned

Managed Identities are commonly used to access:

- Azure Key Vault
- Storage Accounts
- Azure SQL Database
- Azure Resource Manager

---

## Multi-Factor Authentication (MFA)

Multi-Factor Authentication requires users to provide multiple forms of verification.

Typical factors include:

- Password
- Microsoft Authenticator
- FIDO2 Security Key
- SMS (where supported)

MFA significantly reduces the risk of compromised credentials.

---

## Conditional Access

Conditional Access evaluates sign-in conditions before granting access.

Policies can evaluate:

- User identity
- Group membership
- Device compliance
- Location
- Risk level
- Client application

Policies can require MFA, block access, or enforce other security controls.

---

## Privileged Identity Management (PIM)

Microsoft Entra Privileged Identity Management provides just-in-time administrative access.

Capabilities include:

- Eligible role assignments
- Time-limited activation
- Approval workflows
- MFA enforcement
- Access reviews

PIM reduces standing administrative privileges.

---

# Authentication vs Authorization

```text
Authentication

"Who are you?"

↓

Authorization

"What are you allowed to do?"
```

Microsoft Entra ID performs authentication.

Azure RBAC performs authorization.

---

# Zero Trust Model

Azure identity security follows Microsoft's Zero Trust principles.

Core concepts include:

- Verify explicitly
- Use least privilege
- Assume breach

Every access request is evaluated independently.

---

# Identity Lifecycle

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

Access is granted only after all security controls are successfully evaluated.

---

# Enterprise Scenario

A global organization manages Azure resources across multiple subscriptions.

Administrators implement:

- Microsoft Entra ID for centralized identities.
- Conditional Access requiring MFA for privileged accounts.
- Azure RBAC following least privilege.
- Managed Identities for Azure applications.
- PIM for temporary administrator access.
- Regular access reviews for privileged roles.

This architecture minimizes credential exposure while maintaining secure administrative access.

---

# Common Pitfalls

- Assigning Owner permissions unnecessarily.
- Using permanent privileged accounts instead of PIM.
- Disabling or not enforcing MFA.
- Storing credentials in application code.
- Assigning RBAC roles at overly broad scopes.
- Ignoring Conditional Access policies.
- Sharing administrator accounts.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Microsoft Entra ID
> - Azure RBAC
> - Managed Identities
> - Multi-Factor Authentication (MFA)
> - Conditional Access
> - Privileged Identity Management (PIM)
> - Least privilege
> - Zero Trust
> - Authentication vs Authorization

---

# Key Takeaways

- Microsoft Entra ID provides centralized identity and authentication services for Azure resources and cloud applications.
- Azure RBAC controls authorization through role assignments based on security principals, role definitions, and scopes.
- Managed Identities eliminate credential management for Azure workloads, while Conditional Access and MFA strengthen authentication security.
- Privileged Identity Management enables just-in-time administration, reducing the risks associated with permanent privileged accounts.
- Understanding Azure identity security, Zero Trust principles, and access control mechanisms is essential for secure Azure administration and success in the AZ-104 certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Microsoft Entra ID documentation | https://learn.microsoft.com/entra/fundamentals/ |
| Azure RBAC | https://learn.microsoft.com/azure/role-based-access-control/overview |
| Managed Identities | https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview |
| Microsoft Entra Conditional Access | https://learn.microsoft.com/entra/identity/conditional-access/overview |
| Microsoft Entra MFA | https://learn.microsoft.com/entra/identity/authentication/concept-mfa-howitworks |
| Microsoft Entra Privileged Identity Management | https://learn.microsoft.com/entra/id-governance/privileged-identity-management/ |
| Microsoft Learn – Secure access to Azure resources | https://learn.microsoft.com/training/modules/secure-access-azure-resources/
