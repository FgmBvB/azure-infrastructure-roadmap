# Azure RBAC Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for implementing Azure Role-Based Access Control (RBAC) securely, efficiently, and at scale.

---

## Overview

Azure RBAC is one of the most important security mechanisms in Azure.

A well-designed RBAC strategy reduces security risks, simplifies administration, and ensures users receive only the permissions necessary to perform their tasks.

Microsoft recommends implementing Azure RBAC following the **principle of least privilege** while regularly reviewing permissions and avoiding unnecessary administrative access.

---

## RBAC Lifecycle

```text
Identify Requirements
         │
         ▼
Choose Built-in Role
         │
         ▼
Assign at Lowest Scope
         │
         ▼
Assign to Groups
         │
         ▼
Monitor & Audit
         │
         ▼
Review & Remove
```

---

> [!TIP]
> **Key Concepts**
>
> - Apply the principle of least privilege.
> - Prefer built-in roles.
> - Assign permissions to groups.
> - Use the lowest possible scope.
> - Review permissions regularly.

---

## Role Assignment

Microsoft recommends:

- Assign permissions at the lowest appropriate scope.
- Prefer Resource Group scope over Subscription whenever possible.
- Avoid unnecessary Owner assignments.
- Use Reader for audit scenarios.
- Use Contributor instead of Owner when permission management is not required.

---

## Built-in vs Custom Roles

General recommendations include:

- Use Built-in Roles whenever possible.
- Create Custom Roles only when built-in roles cannot satisfy business requirements.
- Keep Custom Roles simple and well documented.
- Review Custom Roles periodically as Azure services evolve.

---

## Identity Management

For better administration:

- Assign roles to **Security Groups** instead of individual users.
- Use **Managed Identities** for Azure workloads.
- Remove orphaned role assignments.
- Regularly review privileged accounts.

---

## Scope Management

To reduce risk:

- Assign permissions at the lowest possible scope.
- Understand permission inheritance.
- Avoid assigning broad permissions at the Subscription or Management Group level unless required.
- Review inherited permissions regularly.

---

## Security

Strengthen Azure RBAC by:

- Protecting privileged accounts with Multi-Factor Authentication (MFA).
- Using Microsoft Entra Privileged Identity Management (PIM) where available.
- Enabling Conditional Access for administrative accounts.
- Using Resource Locks to protect critical resources.
- Reviewing Audit Logs regularly.

---

## Governance

Good governance includes:

- Regular permission reviews.
- Removing unused role assignments.
- Monitoring role assignment changes.
- Documenting administrative responsibilities.
- Reviewing access after organizational changes.

---

## Enterprise Scenario

A company assigns Azure RBAC roles exclusively to Security Groups.

Infrastructure administrators receive the **Contributor** role at the Resource Group scope, while only a small security team receives the **Owner** role when required.

Privileged access is managed through Microsoft Entra PIM, and quarterly reviews remove unnecessary role assignments and orphaned identities.

---

## Best Practices Checklist

- Apply least privilege.
- Prefer Built-in Roles.
- Create Custom Roles only when necessary.
- Assign permissions to groups.
- Use Managed Identities for Azure services.
- Assign roles at the lowest appropriate scope.
- Review privileged access regularly.
- Remove orphaned role assignments.
- Monitor Audit Logs.
- Protect critical resources with Resource Locks.

---

## Common Pitfalls

- Assigning Owner unnecessarily.
- Assigning permissions directly to users.
- Using Subscription scope when Resource Group scope is sufficient.
- Creating unnecessary Custom Roles.
- Ignoring inherited permissions.
- Forgetting to remove orphaned role assignments.
- Not reviewing privileged access periodically.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Least privilege
> - Scope selection
> - Built-in vs Custom Roles
> - Role assignment strategy
> - Managed Identities
> - Resource Locks
> - Privileged access management

---

## Key Takeaways

- Azure RBAC should follow the principle of least privilege.
- Built-in Roles are preferred over Custom Roles whenever possible.
- Assigning roles to groups simplifies administration and improves scalability.
- Permissions should be granted at the lowest appropriate scope.
- Regular reviews and monitoring help maintain a secure Azure environment.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Azure RBAC overview](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure RBAC concepts |
| [Azure built-in roles](https://learn.microsoft.com/azure/role-based-access-control/built-in-roles) | Built-in role reference |
| [Custom Azure roles](https://learn.microsoft.com/azure/role-based-access-control/custom-roles) | Custom Role guidance |
| [Assign Azure roles](https://learn.microsoft.com/azure/role-based-access-control/role-assignments-portal) | Role assignment management |
| [Microsoft Learn – Secure Azure resources with Azure RBAC](https://learn.microsoft.com/training/modules/secure-azure-resources-with-rbac/) | Microsoft Learn module |
