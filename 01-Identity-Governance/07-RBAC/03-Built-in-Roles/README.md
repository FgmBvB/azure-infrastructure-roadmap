# Azure RBAC Built-in Roles

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains the most important built-in Azure RBAC roles, their permissions, and the scenarios in which they should be used.

---

## Overview

Azure provides hundreds of built-in roles that simplify permission management.

Each role is a predefined collection of permissions designed for a specific administrative responsibility.

Rather than creating custom roles, Microsoft recommends using built-in roles whenever they satisfy business requirements.

---

## Learning Objectives

After completing this section you should be able to:

- Identify the most common Azure built-in roles.
- Differentiate administrative responsibilities.
- Select the appropriate role for different scenarios.
- Apply least-privilege principles.
- Understand when a custom role may be required.

---

## Role Hierarchy

```text
                Owner
                  │
         ┌────────┴────────┐
         │                 │
         ▼                 ▼
Contributor      User Access Administrator
         │
         ▼
      Reader
```

---

## Most Common Roles

| Role | Permissions | Can Assign Roles |
|------|-------------|------------------|
| **Owner** | Full management of Azure resources. | Yes |
| **Contributor** | Create and manage Azure resources. | No |
| **Reader** | View resources only. | No |
| **User Access Administrator** | Manage Azure RBAC role assignments. | Yes |

These four roles are the most frequently tested in the AZ-104 exam.

---

## Role Relationships

The four most common Azure RBAC roles have different responsibilities.

A useful way to understand them is:

```text
Owner
│
├── Contributor
│      └── Manage Azure resources
│
└── User Access Administrator
       └── Manage Azure RBAC assignments
```

In practice:

- **Contributor** manages Azure resources.
- **User Access Administrator** manages access permissions.
- **Owner** combines both capabilities.

This relationship helps administrators choose the minimum level of privilege required for each responsibility.

---

## Owner

The **Owner** role provides full administrative access to Azure resources.

Capabilities include:

- Create resources.
- Modify resources.
- Delete resources.
- Assign Azure RBAC roles.

Because of its broad permissions, this role should be assigned only when absolutely necessary.

---

## Contributor

The **Contributor** role can manage Azure resources but cannot grant permissions to other identities.

Typical tasks include:

- Create Virtual Machines.
- Configure networking.
- Deploy Storage Accounts.
- Modify existing Azure resources.

Contributor is one of the most commonly assigned roles for infrastructure administrators.

---

## Reader

The **Reader** role provides read-only access.

Typical scenarios include:

- Auditing.
- Monitoring.
- Inventory.
- Compliance reviews.

Readers cannot modify Azure resources.

---

## User Access Administrator

The **User Access Administrator** role manages Azure RBAC assignments.

Capabilities include:

- Assign Azure roles.
- Remove Azure role assignments.
- Manage access at supported scopes.

This role cannot create or modify Azure resources unless additional roles are assigned.

---

## Data Plane Roles

Some Azure services require separate **Data Plane** roles.

Examples include:

- Storage Blob Data Reader
- Storage Blob Data Contributor
- Storage Queue Data Contributor

These roles grant access to the data stored inside Azure resources rather than to the Azure resource itself.

---

## Service-Specific Built-in Roles

Azure provides many built-in roles designed for specific services.

Some commonly encountered roles in the AZ-104 exam include:

| Role | Typical Responsibility |
|------|------------------------|
| **Virtual Machine Contributor** | Manage virtual machines without managing networking or access permissions. |
| **Network Contributor** | Manage Azure networking resources such as VNets, Load Balancers, and Network Security Groups. |
| **Storage Account Contributor** | Manage Storage Accounts without automatically granting access to blob or file data. |
| **Storage Blob Data Contributor** | Read, write, and delete blob data. |

These specialized roles support least-privilege administration by limiting permissions to specific Azure services.

---

## Choosing the Correct Role

| Requirement | Recommended Role |
|------------|------------------|
| Full resource management | Owner |
| Manage Azure resources | Contributor |
| Read-only access | Reader |
| Manage Azure RBAC assignments | User Access Administrator |
| Access Storage blobs | Storage Blob Data Contributor |

---

## Resource Locks and RBAC

Azure Resource Locks protect resources from accidental modification or deletion.

Important considerations include:

- **Contributor** cannot create, modify, or delete Resource Locks.
- **Owner** can manage Resource Locks because the role includes full management permissions.
- Resource Locks are evaluated before resource operations, helping prevent accidental changes even by highly privileged users.

Resource Locks provide an additional layer of protection beyond Azure RBAC permissions.

---

## Enterprise Scenario

An infrastructure team receives the **Contributor** role on a Resource Group.

The security team receives the **Reader** role at the Subscription scope.

The IAM team receives the **User Access Administrator** role to manage permissions without modifying Azure resources.

Only a small number of administrators receive the **Owner** role.

---

## Best Practices

- Follow the principle of least privilege.
- Prefer Contributor over Owner whenever possible.
- Assign roles to groups instead of individual users.
- Review privileged role assignments regularly.
- Use PIM for highly privileged roles.
- Use Data Plane roles when access to resource data is required.

---

## Common Pitfalls

- Assigning Owner unnecessarily.
- Assuming Contributor can assign roles.
- Confusing Azure RBAC roles with Microsoft Entra roles.
- Forgetting that Data Plane permissions require dedicated roles.
- Granting permissions at an unnecessarily high scope.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Owner
> - Contributor
> - Reader
> - User Access Administrator
> - Data Plane roles
> - Least privilege

---

## Key Takeaways

- Azure provides many built-in roles for common administrative tasks.
- Owner includes permission management, while Contributor does not.
- Reader provides read-only access.
- User Access Administrator manages Azure RBAC assignments.
- Data Plane roles are required to access data stored inside supported Azure resources.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Azure built-in roles](https://learn.microsoft.com/azure/role-based-access-control/built-in-roles) | Complete list of built-in roles |
| [Azure RBAC overview](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure RBAC concepts |
| [Understand Azure role definitions](https://learn.microsoft.com/azure/role-based-access-control/role-definitions) | Role permissions and definitions |
| [Azure Storage data access roles](https://learn.microsoft.com/azure/storage/blobs/assign-azure-role-data-access) | Storage Data Plane roles |
| [Microsoft Learn – Secure Azure resources with Azure RBAC](https://learn.microsoft.com/training/modules/secure-azure-resources-with-rbac/) | Microsoft Learn module |
