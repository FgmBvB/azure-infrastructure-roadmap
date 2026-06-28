# Azure RBAC Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Role-Based Access Control (Azure RBAC), explains its architecture, core components, inheritance model, and how authorization is evaluated within Azure Resource Manager (ARM).

---

## Overview

Azure Role-Based Access Control (Azure RBAC) is Azure's authorization system.

It controls **who** can perform **which actions** on **which Azure resources** by assigning roles to security principals at different scopes.

Azure RBAC follows the **principle of least privilege**, allowing organizations to grant only the permissions required to perform administrative tasks.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure RBAC architecture.
- Differentiate authentication from authorization.
- Identify RBAC components.
- Understand role assignment inheritance.
- Differentiate Azure RBAC from Microsoft Entra RBAC.
- Apply least-privilege access to Azure resources.

---

## Authorization Flow

```text
User / Group / Service Principal
               │
               ▼
     Microsoft Entra ID
(Authentication)
               │
               ▼
 Azure Resource Manager (ARM)
 (Authorization)
               │
               ▼
     Azure RBAC Evaluation
               │
        ┌──────┴──────┐
        │             │
        ▼             ▼
   Permission     Scope Check
   Evaluation
        │
        ▼
 Allow / Deny
```

---

## Authentication vs Authorization

Azure separates authentication from authorization.

| Process | Service |
|----------|---------|
| **Authentication** | Microsoft Entra ID verifies the identity. |
| **Authorization** | Azure RBAC determines what the identity can do. |

Authentication always occurs before authorization.

---

## Core Components

Azure RBAC consists of four primary components.

| Component | Description |
|-----------|-------------|
| **Security Principal** | User, Group, Service Principal, or Managed Identity requesting access. |
| **Role Definition** | Collection of allowed permissions. |
| **Scope** | Level where permissions apply. |
| **Role Assignment** | Links a Security Principal to a Role Definition at a specific Scope. |

---

### Role Definition Permissions

A Role Definition specifies the operations that a Security Principal is allowed to perform.

Permissions are divided into two categories.

| Permission Type | Purpose |
|-----------------|---------|
| **Actions / NotActions** | Manage Azure resources (Control Plane). |
| **DataActions / NotDataActions** | Access data stored inside supported Azure resources (Data Plane). |

For example:

- Creating a Virtual Machine is a **Control Plane** operation.
- Reading blobs from an Azure Storage account is a **Data Plane** operation.

Many built-in roles, such as **Contributor**, manage Azure resources but do not automatically grant access to resource data.

---

## Security Principals

Azure RBAC supports several identity types.

- Users
- Groups
- Service Principals
- Managed Identities

Permissions are always assigned to one of these security principals.

---

## Scope Hierarchy

Permissions can be assigned at different levels.

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

Permissions assigned at a higher scope are inherited by all child resources.

---

### Permission Inheritance

Azure RBAC permissions are cumulative.

If a Security Principal receives multiple role assignments, the effective permissions are the union of all allowed actions within the applicable scope.

For example:

- **Reader** at the Subscription scope.
- **Contributor** at a Resource Group.

The user becomes **Contributor** within that Resource Group while remaining **Reader** elsewhere in the subscription.

It is also important to understand that **NotActions** does not explicitly deny access.

If another applicable role grants the same permission, Azure RBAC allows the operation.

---

## Permission Evaluation

When a request reaches Azure Resource Manager:

1. The identity is authenticated by Microsoft Entra ID.
2. Azure RBAC evaluates all applicable role assignments.
3. The requested operation is compared against the allowed permissions.
4. Scope inheritance is evaluated.
5. Access is granted or denied.

---

### Permission Evaluation Rules

Azure RBAC follows an **allow-based authorization model**.

If no role assignment grants the requested permission, access is denied automatically.

Azure Resource Manager also evaluates **Deny Assignments** before granting access.

Important characteristics include:

- Deny Assignments always take precedence over role assignments.
- Administrators cannot create custom Deny Assignments directly.
- Deny Assignments are created automatically by certain Azure services and resource protection features.
- A matching Deny Assignment blocks access even if the user has the **Owner** role.

---

## Azure RBAC vs Microsoft Entra RBAC

Although both use Role-Based Access Control, they manage different resources.

| Azure RBAC | Microsoft Entra RBAC |
|------------|----------------------|
| Manages Azure resources | Manages Microsoft Entra objects |
| Evaluated by Azure Resource Manager | Evaluated by Microsoft Entra ID |
| Controls subscriptions, resource groups, and resources | Controls users, groups, devices, applications, and directory administration |

---

## Enterprise Scenario

An organization grants the **Contributor** role at the Resource Group scope to the infrastructure team.

Team members can create and manage Azure resources within that Resource Group but cannot assign permissions to other users.

The Security team receives the **Reader** role at the Subscription scope, allowing them to audit resources without making changes.

---

## Best Practices

- Apply the principle of least privilege.
- Assign roles to groups instead of individual users whenever possible.
- Grant permissions at the lowest appropriate scope.
- Review role assignments regularly.
- Protect privileged accounts with Multi-Factor Authentication (MFA).
- Use Privileged Identity Management (PIM) where available.

---

## Common Pitfalls

- Assigning permissions at the Subscription scope unnecessarily.
- Confusing Azure RBAC with Microsoft Entra RBAC.
- Assigning roles directly to users instead of groups.
- Granting Owner permissions when Contributor is sufficient.
- Forgetting that permissions are inherited.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure RBAC architecture
> - Authentication vs Authorization
> - Security Principals
> - Role Definitions
> - Role Assignments
> - Scope hierarchy
> - Permission inheritance

---

## Key Takeaways

- Azure RBAC is Azure's authorization system.
- Microsoft Entra ID authenticates identities before Azure RBAC evaluates permissions.
- Role assignments combine a Security Principal, a Role Definition, and a Scope.
- Permissions inherit from parent scopes to child resources.
- Applying least privilege improves security and simplifies administration.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [What is Azure RBAC?](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure RBAC overview |
| [Understand Azure role definitions](https://learn.microsoft.com/azure/role-based-access-control/role-definitions) | Role definitions and permissions |
| [Understand Azure scopes](https://learn.microsoft.com/azure/role-based-access-control/scope-overview) | RBAC scope hierarchy |
| [Assign Azure roles](https://learn.microsoft.com/azure/role-based-access-control/role-assignments-portal) | Role assignment methods |
| [Microsoft Learn – Secure Azure resources with Azure RBAC](https://learn.microsoft.com/training/modules/secure-azure-resources-with-rbac/) | Microsoft Learn module |
