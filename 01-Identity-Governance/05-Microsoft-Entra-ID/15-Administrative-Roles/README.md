# Administrative Roles

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Microsoft Entra Administrative Roles, Role-Based Access Control (RBAC), delegated administration, Privileged Identity Management (PIM), and Microsoft's security best practices for privileged access.

---

## Overview

Microsoft Entra ID uses **Role-Based Access Control (RBAC)** to delegate administrative permissions across the identity platform.

Instead of granting full administrative privileges to every administrator, Microsoft Entra ID provides specialized built-in roles that follow the **principle of least privilege**, allowing organizations to securely manage users, groups, devices, applications, authentication, and identity governance.

Administrative Roles are a fundamental component of Microsoft Entra security and are frequently tested throughout the AZ-104 certification.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Microsoft Entra RBAC.
- Differentiate Microsoft Entra RBAC from Azure RBAC.
- Identify the purpose of the main built-in administrative roles.
- Assign administrative permissions securely.
- Configure delegated administration using Administrative Units.
- Manage privileged access with Microsoft Entra Privileged Identity Management (PIM).
- Apply Microsoft's security recommendations for privileged administration.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Microsoft Entra RBAC, administrative scopes, Administrative Units, Role-Assignable Groups, and PIM overview. |
| **02 - Built-in Roles** | Global Administrator, User Administrator, Authentication Administrator, Security Administrator, Cloud Application Administrator, and other built-in roles. |
| **03 - Role Assignments** | Direct assignments, Role-Assignable Groups, Administrative Units, Active vs Eligible assignments, and PIM activation. |
| **04 - Best Practices** | Least privilege, privileged access, emergency access accounts, auditing, and governance recommendations. |

---

## Architecture

```text
                Microsoft Entra ID
                       │
                       ▼
          Role-Based Access Control
                       │
      ┌────────────────┼────────────────┐
      │                │                │
      ▼                ▼                ▼
 Built-in Roles   Custom Roles   Administrative Units
      │                │                │
      └────────────────┼────────────────┘
                       │
                       ▼
              Role Assignments
                       │
                       ▼
      Users • Groups • PIM Activation
                       │
                       ▼
          Administrative Operations
```

---

## Skills Covered

This section includes:

- Microsoft Entra RBAC
- Administrative Roles
- Built-in Roles
- Custom Roles
- Global Administrator
- User Administrator
- Authentication Administrator
- Cloud Application Administrator
- Security Administrator
- Global Reader
- Role Assignments
- Role-Assignable Groups
- Administrative Units
- Privileged Identity Management (PIM)
- Eligible Assignments
- Least Privilege

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Manage Microsoft Entra administrative roles.
- Delegate administrative permissions.
- Configure Role-Based Access Control (RBAC).
- Assign administrative roles securely.
- Configure Administrative Units.
- Manage privileged access using PIM.
- Apply least-privilege principles.

---

## Key Takeaways

- Microsoft Entra RBAC provides secure delegated administration.
- Built-in roles grant permissions based on specific administrative responsibilities.
- Administrative Units reduce the scope of administrative permissions.
- PIM minimizes standing privileged access through Just-in-Time activation.
- Following the principle of least privilege significantly improves the security of Microsoft Entra environments.
