# Azure RBAC Role Assignments

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains how Azure RBAC role assignments work, including assignment scopes, inheritance, effective permissions, and the different methods available to assign roles.

---

## Overview

A role assignment links a **Security Principal** to a **Role Definition** at a specific **Scope**.

Without a role assignment, a user, group, service principal, or managed identity has no permissions to manage Azure resources through Azure RBAC.

Role assignments are the mechanism Azure Resource Manager (ARM) uses to authorize administrative operations.

---

## Learning Objectives

After completing this section you should be able to:

- Understand how role assignments work.
- Assign roles at the correct scope.
- Understand permission inheritance.
- Calculate effective permissions.
- Assign roles using the Azure portal, Azure CLI, PowerShell, and ARM templates.
- Apply least-privilege principles.

---

## Role Assignment Components

Every role assignment contains three elements.

```text
Security Principal
        │
        ▼
 Role Assignment
        │
        ├──────────────┐
        │              │
        ▼              ▼
Role Definition     Scope
```

| Component | Description |
|-----------|-------------|
| **Security Principal** | User, Group, Service Principal, or Managed Identity. |
| **Role Definition** | Collection of allowed permissions. |
| **Scope** | Where the permissions apply. |

---

## Supported Security Principals

Azure RBAC roles can be assigned to:

- Users
- Groups
- Service Principals
- Managed Identities

Assigning roles to groups is Microsoft's recommended approach because it simplifies administration.

---

## Scope Levels

Role assignments can be created at four different scopes.

```text
Management Group
        │
        ▼
 Subscription
        │
        ▼
 Resource Group
        │
        ▼
    Resource
```

Permissions assigned at a higher scope are inherited automatically by child resources.

---

## Permission Inheritance

Azure RBAC uses cumulative permissions.

For example:

| Scope | Role |
|--------|------|
| Subscription | Reader |
| Resource Group | Contributor |

The user has:

- **Reader** permissions across the subscription.
- **Contributor** permissions inside that Resource Group.

Permissions inherited from multiple assignments are combined.

---

## Effective Permissions

When a request reaches Azure Resource Manager:

1. Microsoft Entra ID authenticates the identity.
2. Azure RBAC collects all applicable role assignments.
3. Scope inheritance is evaluated.
4. Allowed permissions are combined.
5. Any applicable Deny Assignments are evaluated.
6. ARM grants or denies the requested operation.

---

## Assignment Methods

Azure roles can be assigned using several tools.

| Method | Typical Use |
|---------|-------------|
| Azure portal | Interactive administration |
| Azure CLI | Automation and scripting |
| Azure PowerShell | Administration and automation |
| ARM Templates / Bicep | Infrastructure as Code (IaC) |
| Azure REST API | Programmatic management |

---

## Azure CLI Example

```bash
az role assignment create \
  --assignee <principal-id> \
  --role Contributor \
  --scope /subscriptions/<subscription-id>/resourceGroups/<resource-group>
```

---

## Azure PowerShell Example

```powershell
New-AzRoleAssignment `
-ObjectId <PrincipalId> `
-RoleDefinitionName Contributor `
-Scope "/subscriptions/<subscription-id>/resourceGroups/<resource-group>"
```

---

## Enterprise Scenario

An organization grants the **Reader** role at the Subscription scope to the Security team.

The Infrastructure team receives the **Contributor** role only for the Production Resource Group.

A Managed Identity receives **Storage Blob Data Contributor** permissions on a Storage Account, allowing an application to access blob data without storing credentials.

---

## Best Practices

- Assign permissions at the lowest appropriate scope.
- Prefer assigning roles to groups instead of individual users.
- Use Managed Identities for Azure workloads.
- Review role assignments regularly.
- Remove unnecessary assignments promptly.
- Apply the principle of least privilege.

---

## Common Pitfalls

- Assigning Owner unnecessarily.
- Assigning permissions at the Subscription scope when Resource Group scope is sufficient.
- Creating duplicate role assignments.
- Forgetting inherited permissions.
- Ignoring Deny Assignments.
- Assigning roles directly to many individual users.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Role assignments
> - Security Principals
> - Scope hierarchy
> - Permission inheritance
> - Effective permissions
> - Azure CLI and PowerShell role assignment
> - Least privilege

---

## Key Takeaways

- A role assignment connects a Security Principal, a Role Definition, and a Scope.
- Permissions inherit from parent scopes to child resources.
- Effective permissions are cumulative across multiple assignments.
- Azure RBAC supports multiple assignment methods for manual and automated administration.
- Assigning permissions at the lowest appropriate scope improves security.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Assign Azure roles](https://learn.microsoft.com/azure/role-based-access-control/role-assignments-portal) | Create and manage role assignments |
| [Understand Azure scopes](https://learn.microsoft.com/azure/role-based-access-control/scope-overview) | Scope hierarchy and inheritance |
| [Azure RBAC overview](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure RBAC architecture |
| [Azure CLI RBAC commands](https://learn.microsoft.com/cli/azure/role/assignment) | Azure CLI role assignment management |
| [Azure PowerShell RBAC](https://learn.microsoft.com/powershell/module/az.resources/new-azroleassignment) | PowerShell role assignment cmdlets |
| [Microsoft Learn – Secure Azure resources with Azure RBAC](https://learn.microsoft.com/training/modules/secure-azure-resources-with-rbac/) | Microsoft Learn module |
