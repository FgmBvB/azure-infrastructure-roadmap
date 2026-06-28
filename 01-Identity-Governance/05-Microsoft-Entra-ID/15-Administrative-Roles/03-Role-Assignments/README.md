# Microsoft Entra Role Assignments

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how administrative roles are assigned in Microsoft Entra ID, including direct assignments, role-assignable groups, Administrative Units, and Privileged Identity Management (PIM).

---

## Role Assignment Architecture

```text
                 Administrator
                        │
                        ▼
              Microsoft Entra Role
                        │
        ┌───────────────┼───────────────┐
        │               │               │
        ▼               ▼               ▼
 Direct Assignment  Role Group    Eligible (PIM)
        │               │               │
        └───────────────┼───────────────┘
                        │
                        ▼
                Administrative Scope
                        │
                        ▼
             Authorized Administration
```

---

> [!TIP]
> **Key Concepts**
>
> - Administrative roles can be assigned directly or through Role-Assignable Groups.
> - Administrative Units provide delegated administration.
> - Privileged Identity Management (PIM) supports Just-in-Time (JIT) access.
> - Eligible assignments reduce standing privileges.
> - Microsoft recommends assigning the minimum permissions required.

---

## Overview

Microsoft Entra ID provides multiple ways to assign administrative roles.

Organizations can assign roles directly to users, delegate them through Role-Assignable Groups, or activate them temporarily using Privileged Identity Management (PIM).

Selecting the appropriate assignment method improves security and simplifies administration.

---

## Direct Role Assignments

A role can be assigned directly to an individual user.

Characteristics include:

- Simple to configure.
- Immediate administrative access.
- Suitable for small environments.
- Difficult to manage at scale.

Microsoft recommends limiting direct assignments whenever possible.

---

## Role-Assignable Groups

Administrative roles can also be assigned to **Role-Assignable Groups**.

Unlike standard security groups, these groups are created with the **isAssignableToRole** property enabled.

Characteristics include:

- Centralized administration.
- Easier permission management.
- Simplified onboarding and offboarding.
- Suitable for large organizations.

Only **Global Administrators** and **Privileged Role Administrators** can manage the membership of Role-Assignable Groups.

---

## Administrative Units

Administrative Units (AUs) limit administrative scope.

Instead of granting tenant-wide permissions, administrators can manage only:

- Selected users.
- Selected groups.
- Selected devices.

This enables delegated administration for departments, campuses, subsidiaries, or geographic regions.

---

## Privileged Identity Management (PIM)

Microsoft Entra Privileged Identity Management reduces permanent privileged access.

Users receive one of two assignment types.

| Assignment Type | Description |
|-----------------|-------------|
| **Active** | Administrative permissions are always available. |
| **Eligible** | Permissions must be activated when needed. |

Eligible assignments reduce standing administrative privileges.

---

## Role Activation

Eligible administrators activate their roles only when necessary.

Activation may require:

- Multi-Factor Authentication
- Approval
- Business justification
- Time limitations

After activation expires, administrative permissions are automatically removed.

---

## Assignment Scope

Administrative roles can be assigned at different scopes.

Examples include:

| Scope | Example |
|--------|---------|
| Tenant | Entire Microsoft Entra tenant |
| Administrative Unit | HR department only |
| Application | Supported application administration scenarios |

Choosing the smallest appropriate scope follows the principle of least privilege.

---

## Assignment Evaluation

```text
User
 │
 ▼
Assigned Role?
 │
 ├── No → Access Denied
 │
 ▼
Assignment Type
 │
 ├── Active
 │        │
 │        ▼
 │   Immediate Access
 │
 └── Eligible
          │
          ▼
     Activate Role
          │
          ▼
 Authorized Operation
```

---

## Enterprise Scenario

A multinational company delegates administration by region.

Regional IT administrators receive the **User Administrator** role scoped to their own Administrative Unit.

Application administrators receive permissions through Role-Assignable Groups.

Global Administrators receive Eligible assignments through Privileged Identity Management and activate their privileges only during maintenance windows.

---

## Best Practices

- Prefer Role-Assignable Groups over direct assignments.
- Use Administrative Units for delegated administration.
- Use Eligible assignments with PIM for privileged roles.
- Minimize permanent administrative access.
- Protect privileged roles with MFA.
- Review role assignments regularly.

---

## Common Pitfalls

- Assigning roles directly to too many users.
- Granting tenant-wide permissions unnecessarily.
- Leaving privileged roles permanently active.
- Ignoring Administrative Units.
- Not reviewing privileged assignments periodically.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Direct role assignments
> - Role-Assignable Groups
> - Administrative Units
> - Active vs Eligible assignments
> - Privileged Identity Management (PIM)
> - Assignment scopes

---

## Key Takeaways

- Microsoft Entra ID supports multiple role assignment methods.
- Role-Assignable Groups simplify permission management.
- Administrative Units reduce administrative scope.
- Eligible assignments improve security by minimizing standing privileges.
- Following least privilege reduces operational risk.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Assign Microsoft Entra roles](https://learn.microsoft.com/entra/identity/role-based-access-control/manage-roles-portal) | Assigning administrative roles |
| [Role-Assignable Groups](https://learn.microsoft.com/entra/identity/role-based-access-control/groups-concept) | Administrative role groups |
| [Administrative Units](https://learn.microsoft.com/entra/identity/role-based-access-control/administrative-units) | Delegated administration |
| [Microsoft Entra Privileged Identity Management](https://learn.microsoft.com/entra/id-governance/privileged-identity-management/pim-configure) | PIM overview |
| [Microsoft Learn – Manage Microsoft Entra permissions by using RBAC](https://learn.microsoft.com/training/modules/manage-permissions-entra-id/) | Microsoft Learn module |
