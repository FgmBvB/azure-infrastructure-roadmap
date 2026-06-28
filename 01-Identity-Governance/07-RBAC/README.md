# Azure Role-Based Access Control (RBAC)

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Role-Based Access Control (Azure RBAC), including its architecture, built-in roles, role assignments, custom roles, and Microsoft's recommended governance practices.

---

## Overview

Azure Role-Based Access Control (Azure RBAC) is Azure's authorization system.

It enables organizations to control who can manage Azure resources, which actions they can perform, and the scope at which permissions apply.

Azure RBAC is a fundamental component of Azure governance and security, implementing the principle of least privilege through fine-grained access control.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure RBAC architecture.
- Differentiate Azure RBAC from Microsoft Entra RBAC.
- Configure role assignments.
- Understand built-in and custom roles.
- Apply permissions at the appropriate scope.
- Implement least-privilege access.
- Apply Microsoft best practices for Azure authorization.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Azure RBAC architecture, authorization process, security principals, scopes, and permission evaluation. |
| **02 - Role Assignments** | Role assignments, inheritance, effective permissions, supported assignment methods, and scopes. |
| **03 - Built-in Roles** | Owner, Contributor, Reader, User Access Administrator, Data Plane roles, and service-specific roles. |
| **04 - Custom Roles** | Custom role architecture, JSON structure, Actions, DataActions, Assignable Scopes, and limitations. |
| **05 - Best Practices** | Least privilege, governance, auditing, Resource Locks, Managed Identities, and operational recommendations. |

---

## Architecture

```text
            Microsoft Entra ID
          (Authentication)
                   │
                   ▼
      Azure Resource Manager (ARM)
           (Authorization)
                   │
                   ▼
            Azure RBAC Engine
                   │
      ┌────────────┼────────────┐
      │            │            │
      ▼            ▼            ▼
 Security     Role Definition   Scope
 Principal
      │            │            │
      └────────────┼────────────┘
                   │
                   ▼
           Role Assignment
                   │
                   ▼
          Azure Resources
```

---

## Skills Covered

This section includes:

- Azure RBAC
- Authentication vs Authorization
- Security Principals
- Role Definitions
- Role Assignments
- Built-in Roles
- Custom Roles
- Scope Hierarchy
- Permission Inheritance
- Data Plane Permissions
- Managed Identities
- Resource Locks
- Least Privilege

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Configure Azure RBAC.
- Assign Azure roles.
- Configure role scopes.
- Manage built-in and custom roles.
- Implement least-privilege access.
- Troubleshoot Azure authorization issues.
- Secure Azure resources using RBAC.

---

## Key Takeaways

- Azure RBAC controls authorization to Azure resources.
- Permissions are granted through role assignments that combine a Security Principal, a Role Definition, and a Scope.
- Built-in Roles should be preferred over Custom Roles whenever possible.
- Permissions are inherited through the Azure resource hierarchy.
- Applying least privilege and assigning permissions at the lowest appropriate scope improves both security and operational efficiency.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Azure RBAC overview](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure RBAC concepts and architecture |
| [Azure built-in roles](https://learn.microsoft.com/azure/role-based-access-control/built-in-roles) | Built-in role reference |
| [Azure role definitions](https://learn.microsoft.com/azure/role-based-access-control/role-definitions) | Role definition structure |
| [Assign Azure roles](https://learn.microsoft.com/azure/role-based-access-control/role-assignments-portal) | Role assignment methods |
| [Microsoft Learn – Secure Azure resources with Azure RBAC](https://learn.microsoft.com/training/modules/secure-azure-resources-with-rbac/) | Microsoft Learn module |
