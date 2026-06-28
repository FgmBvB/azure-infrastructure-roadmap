# Microsoft Entra Administrative Roles Overview

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It introduces Microsoft Entra Administrative Roles, explains the Role-Based Access Control (RBAC) model, and describes how administrative permissions are delegated following the principle of least privilege.

---

## Administrative Roles Architecture

```text
               Microsoft Entra ID
                      │
                      ▼
        Role-Based Access Control (RBAC)
                      │
        ┌─────────────┼─────────────┐
        │             │             │
        ▼             ▼             ▼
 Built-in Roles   Custom Roles   Administrative Units
        │             │             │
        └─────────────┼─────────────┘
                      │
                      ▼
             Administrative Permissions
```

---

> [!TIP]
> **Key Concepts**
>
> - Microsoft Entra ID uses Role-Based Access Control (RBAC).
> - Administrative roles delegate permissions without granting full administrative access.
> - Roles follow the principle of least privilege.
> - Microsoft provides built-in roles for common administrative tasks.
> - Permissions can be scoped to Administrative Units for delegated administration.

---

## Overview

Microsoft Entra ID uses **Role-Based Access Control (RBAC)** to delegate administrative permissions.

Instead of granting every administrator full control over the tenant, RBAC assigns only the permissions required to perform specific administrative tasks.

This approach reduces security risks while simplifying operational management.

---

## Microsoft Entra RBAC

Microsoft Entra RBAC controls permissions for identity-related resources.

Examples include:

- Users
- Groups
- Enterprise Applications
- App Registrations
- Devices
- Authentication Methods
- Administrative Units

Every administrative action is authorized through an assigned role.

---

## Microsoft Entra RBAC vs Azure RBAC

Although both use Role-Based Access Control, they manage different resource types.

| Feature | Microsoft Entra RBAC | Azure RBAC |
|---------|----------------------|------------|
| Scope | Identity resources | Azure resources |
| Manages | Users, Groups, Applications, Devices | Virtual Machines, Storage, Networking, Azure Services |
| Administration Portal | Microsoft Entra admin center | Azure Portal |
| Examples | User Administrator, Global Administrator | Owner, Contributor, Reader |

These authorization systems operate independently but often complement each other.

---

## Built-in Roles

Microsoft Entra ID includes numerous built-in administrative roles.

Examples include:

- Global Administrator
- User Administrator
- Groups Administrator
- Authentication Administrator
- Cloud Application Administrator
- Security Administrator
- Helpdesk Administrator
- Global Reader

Each role provides only the permissions required for its administrative function.

---

## Administrative Scope

Administrative permissions can apply at different scopes.

Examples include:

- Entire tenant
- Administrative Units
- Individual applications (supported scenarios)

Scoping permissions limits administrative access to only the required resources.

---

## Administrative Units

Administrative Units (AUs) allow organizations to delegate administration over a subset of users, groups, or devices.

For example:

- HR administrators manage only Human Resources users.
- Regional administrators manage only devices located in Europe.
- University IT staff manage only one faculty.

Administrative Units reduce unnecessary administrative privileges in large organizations.

---

## Principle of Least Privilege

Microsoft recommends assigning the minimum permissions necessary.

Benefits include:

- Reduced attack surface.
- Lower risk of accidental changes.
- Better separation of duties.
- Easier auditing.

Administrators should avoid assigning Global Administrator unless absolutely necessary.

---

## Privileged Identity Management (PIM)

Microsoft Entra Privileged Identity Management (PIM) enables **Just-in-Time (JIT)** administration.

Instead of permanent role assignments:

- Users become **Eligible**.
- Roles are activated only when required.
- Activations can require approval or Multi-Factor Authentication.
- Activations are audited.

PIM helps reduce standing administrative privileges.

---

## Role Assignment Flow

```text
Administrator
      │
      ▼
Role Assignment
      │
      ▼
RBAC Evaluation
      │
      ▼
Administrative Scope
      │
      ▼
Authorized Operation
```

---

## Enterprise Scenario

A company has several IT departments.

Helpdesk personnel receive the **Helpdesk Administrator** role, allowing them to reset passwords without managing tenant-wide settings.

Regional IT managers administer only their assigned Administrative Units, while Global Administrators are limited to a small number of emergency and infrastructure accounts.

Privileged administrative roles are activated temporarily using Microsoft Entra Privileged Identity Management (PIM).

---

## Best Practices

- Follow the principle of least privilege.
- Assign built-in roles instead of Global Administrator whenever possible.
- Use Administrative Units to delegate administration.
- Protect privileged roles with Multi-Factor Authentication.
- Use Privileged Identity Management (PIM) for privileged roles.
- Review role assignments regularly.

---

## Common Pitfalls

- Assigning Global Administrator unnecessarily.
- Granting permanent privileged access.
- Ignoring Administrative Units.
- Assigning multiple overlapping roles.
- Forgetting to audit privileged role assignments.
- Not protecting administrator accounts with MFA.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Microsoft Entra RBAC
> - Built-in administrative roles
> - Microsoft Entra RBAC vs Azure RBAC
> - Administrative Units
> - Principle of least privilege
> - Privileged Identity Management (PIM)

---

## Key Takeaways

- Microsoft Entra ID uses RBAC to delegate administrative permissions.
- Administrative roles provide only the permissions required for specific tasks.
- Administrative Units allow scoped administration.
- PIM reduces standing privileged access.
- Least privilege is a fundamental Microsoft security recommendation.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Microsoft Entra built-in roles](https://learn.microsoft.com/entra/identity/role-based-access-control/permissions-reference) | Built-in administrative roles |
| [Role-based access control in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/role-based-access-control/custom-overview) | Microsoft Entra RBAC overview |
| [Administrative Units](https://learn.microsoft.com/entra/identity/role-based-access-control/administrative-units) | Administrative Units |
| [Microsoft Entra Privileged Identity Management](https://learn.microsoft.com/entra/id-governance/privileged-identity-management/pim-configure) | PIM overview |
| [Microsoft Learn – Manage Microsoft Entra permissions by using RBAC](https://learn.microsoft.com/training/modules/manage-permissions-entra-id/) | Microsoft Learn module |
