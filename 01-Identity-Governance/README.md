# Identity & Governance

> [!NOTE]
> This section is part of my Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Microsoft Entra ID, identity management, authorization, governance, compliance, and resource protection across Azure.

---

## Overview

Identity and Governance form the security foundation of every Azure environment.

This section covers how identities are authenticated, how permissions are assigned, how organizational standards are enforced, and how Azure resources are protected throughout their lifecycle.

The topics included here align closely with the governance objectives of the Microsoft AZ-104 certification and represent many of the day-to-day responsibilities of an Azure Administrator.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Microsoft Entra ID.
- Manage users and groups.
- Configure authentication and authorization.
- Implement Multi-Factor Authentication (MFA).
- Configure Conditional Access.
- Manage Azure RBAC.
- Implement Azure Policy.
- Protect Azure resources with Resource Locks.
- Organize resources using Azure Tags.
- Apply Azure governance best practices.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **05 - Microsoft Entra ID** | Microsoft Entra architecture, tenants, identities, licensing, and directory fundamentals. |
| **06 - Users and Groups** | User lifecycle, Security Groups, Microsoft 365 Groups, Dynamic Groups, Administrative Units, and licensing. |
| **07 - Azure RBAC** | Authorization, role assignments, built-in roles, custom roles, and least privilege. |
| **08 - Azure Policy** | Governance, Policy Definitions, Assignments, Initiatives, compliance, and remediation. |
| **09 - Resource Locks** | Protecting Azure resources from accidental modification or deletion. |
| **10 - Tags** | Resource organization, governance, Cost Management, and Azure Policy integration. |

---

## Identity and Governance Architecture

```text
                  Microsoft Entra ID
                         │
      ┌──────────────────┼──────────────────┐
      │                  │                  │
      ▼                  ▼                  ▼
 Users & Groups         MFA        Conditional Access
      │
      ▼
 Azure RBAC
(Authorization)
      │
      ▼
 Azure Policy
(Governance)
      │
      ▼
Resource Locks
      │
      ▼
 Azure Tags
```

---

## Skills Covered

This section includes:

- Microsoft Entra ID
- Identity Management
- Hybrid Identity
- Microsoft Entra Connect
- Multi-Factor Authentication (MFA)
- Conditional Access
- Users and Groups
- Azure RBAC
- Azure Policy
- Resource Locks
- Azure Tags
- Identity Governance
- Least Privilege
- Compliance
- Resource Protection

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Manage Microsoft Entra ID.
- Configure authentication and authorization.
- Manage users and groups.
- Configure Azure RBAC.
- Implement Azure Policy.
- Protect Azure resources with Resource Locks.
- Organize Azure resources using Tags.
- Apply governance and compliance best practices.

---

## Key Takeaways

- Microsoft Entra ID provides identity and authentication services for Azure.
- Azure RBAC controls **who** can manage Azure resources.
- Azure Policy governs **how** Azure resources should be configured.
- Resource Locks protect deployed resources from accidental changes.
- Azure Tags improve organization, governance, automation, and Cost Management.
- Combining these services creates a secure, scalable, and well-governed Azure environment.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Microsoft Entra documentation](https://learn.microsoft.com/entra/) | Microsoft Entra ID concepts and administration |
| [Azure RBAC overview](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure authorization |
| [Azure Policy overview](https://learn.microsoft.com/azure/governance/policy/overview) | Azure governance |
| [Lock your Azure resources](https://learn.microsoft.com/azure/azure-resource-manager/management/lock-resources) | Resource protection |
| [Use tags to organize Azure resources](https://learn.microsoft.com/azure/azure-resource-manager/management/tag-resources) | Resource organization |
| [Microsoft Learn – AZ-104 Learning Path](https://learn.microsoft.com/training/paths/az-104-administrator-prerequisites/) | Microsoft Learn for AZ-104 |
