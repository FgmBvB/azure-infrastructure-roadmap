# Azure RBAC Custom Roles

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains Azure RBAC Custom Roles, their structure, permissions, supported operations, limitations, and when they should be used instead of built-in roles.

---

## Overview

Azure RBAC includes hundreds of built-in roles that satisfy most administrative scenarios.

When built-in roles do not provide the required level of access, administrators can create **Custom Roles** that include only the permissions needed for a specific job.

Custom Roles support the principle of least privilege by allowing organizations to grant precise permissions while avoiding unnecessary administrative access.

---

## Learning Objectives

After completing this section you should be able to:

- Understand when to use Custom Roles.
- Identify the components of a Custom Role.
- Differentiate Actions and DataActions.
- Configure Assignable Scopes.
- Understand Custom Role limitations.
- Apply least-privilege access.

---

## Custom Role Architecture

```text
Custom Role
      │
      ├──────────────┐
      │              │
      ▼              ▼
 Permissions   Assignable Scopes
      │
      ▼
Role Assignment
      │
      ▼
Security Principal
```

---

## When to Use Custom Roles

Custom Roles are appropriate when:

- Built-in roles provide too many permissions.
- A specific combination of permissions is required.
- Organizations implement strict least-privilege policies.
- Administrative tasks must be delegated with limited capabilities.

Whenever a built-in role satisfies the requirement, Microsoft recommends using the built-in role instead.

---

## Custom Role Structure

A Custom Role is defined using JSON.

The most important properties are:

| Property | Purpose |
|----------|---------|
| **Name** | Role name. |
| **Description** | Role description. |
| **Actions** | Allowed management operations. |
| **NotActions** | Excluded management operations. |
| **DataActions** | Allowed data operations. |
| **NotDataActions** | Excluded data operations. |
| **AssignableScopes** | Scopes where the role can be assigned. |

---

## Actions vs DataActions

Azure RBAC separates management permissions from data permissions.

| Property | Plane |
|----------|-------|
| **Actions** | Control Plane |
| **NotActions** | Control Plane |
| **DataActions** | Data Plane |
| **NotDataActions** | Data Plane |

Examples:

- Creating a Virtual Machine uses **Actions**.
- Reading blob data uses **DataActions**.

---

## Assignable Scopes

Every Custom Role defines one or more **Assignable Scopes**.

These determine where the role can be assigned.

Common scopes include:

- Management Group
- Subscription
- Resource Group

A role cannot be assigned outside its configured Assignable Scopes.

---

## Custom Role Example

```json
{
  "Name": "Virtual Machine Operator",
  "Description": "Manage virtual machines without RBAC permissions.",
  "Actions": [
    "Microsoft.Compute/virtualMachines/*"
  ],
  "NotActions": [
    "Microsoft.Authorization/*"
  ],
  "AssignableScopes": [
    "/subscriptions/<subscription-id>"
  ]
}
```

---

## Limitations

Custom Roles have some important limitations.

- They cannot grant permissions beyond Azure RBAC capabilities.
- They must include at least one Assignable Scope.
- They should be reviewed regularly as Azure services evolve.
- Built-in roles are updated automatically by Microsoft, while Custom Roles must be maintained by administrators.

---

## Enterprise Scenario

A support team must restart Virtual Machines but should not modify networking resources or assign Azure RBAC permissions.

Instead of assigning the Contributor role, the organization creates a Custom Role containing only the required Microsoft.Compute operations.

This follows the principle of least privilege while reducing operational risk.

---

## Best Practices

- Prefer built-in roles whenever possible.
- Create narrowly scoped Custom Roles.
- Document every Custom Role.
- Review Custom Roles periodically.
- Assign Custom Roles to groups rather than individual users.
- Validate permissions before production deployment.

---

## Common Pitfalls

- Creating unnecessary Custom Roles.
- Granting excessive permissions.
- Forgetting Assignable Scopes.
- Not documenting Custom Roles.
- Duplicating existing built-in roles.
- Failing to review Custom Roles after Azure service updates.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Custom Roles
> - JSON role structure
> - Actions vs DataActions
> - Assignable Scopes
> - Least privilege
> - Built-in vs Custom Roles

---

## Key Takeaways

- Custom Roles provide granular Azure RBAC permissions.
- Actions manage Azure resources, while DataActions manage resource data.
- Assignable Scopes define where a role can be used.
- Built-in roles should be preferred whenever they meet business requirements.
- Well-designed Custom Roles improve security by enforcing least privilege.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Custom Azure roles](https://learn.microsoft.com/azure/role-based-access-control/custom-roles) | Create and manage Custom Roles |
| [Azure role definitions](https://learn.microsoft.com/azure/role-based-access-control/role-definitions) | Role definition structure |
| [Azure RBAC overview](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure RBAC concepts |
| [Assign Azure roles](https://learn.microsoft.com/azure/role-based-access-control/role-assignments-portal) | Assigning custom roles |
| [Microsoft Learn – Secure Azure resources with Azure RBAC](https://learn.microsoft.com/training/modules/secure-azure-resources-with-rbac/) | Microsoft Learn module |
