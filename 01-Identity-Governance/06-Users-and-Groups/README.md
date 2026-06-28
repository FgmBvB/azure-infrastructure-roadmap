# Users and Groups

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers user and group management in Microsoft Entra ID, including identity lifecycle, group administration, licensing, delegation, and Microsoft's recommended operational practices.

---

## Overview

Users and Groups are the foundation of identity management in Microsoft Entra ID.

Users represent identities that authenticate to Azure, Microsoft 365, and integrated applications, while Groups simplify administration by centralizing permissions, license assignments, and access to organizational resources.

Effective management of users and groups improves security, reduces administrative overhead, and supports scalable identity governance.

---

## Learning Objectives

After completing this section you should be able to:

- Create and manage Microsoft Entra users.
- Differentiate Member and Guest accounts.
- Understand Security Groups and Microsoft 365 Groups.
- Configure Dynamic Groups.
- Manage Group-based Licensing.
- Delegate administration using Administrative Units.
- Apply Microsoft best practices for user and group management.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Users** | User lifecycle, Member and Guest accounts, licensing, bulk operations, and user management. |
| **02 - Groups** | Security Groups, Microsoft 365 Groups, Dynamic Groups, ownership, and licensing. |
| **03 - Group Management** | Membership management, Administrative Units, Dynamic Groups, licensing, monitoring, and troubleshooting. |
| **04 - Best Practices** | Security recommendations, governance, licensing, and operational best practices. |

---

## Architecture

```text
              Microsoft Entra ID
                     │
        ┌────────────┴────────────┐
        │                         │
        ▼                         ▼
      Users                    Groups
        │                         │
        ├──────────────┐          │
        │              │          │
        ▼              ▼          ▼
 Authentication   Licenses   Permissions
        │                         │
        └──────────────┬──────────┘
                       ▼
             Azure Resources
          Microsoft 365 Services
      Enterprise Applications
```

---

## Skills Covered

This section includes:

- Microsoft Entra Users
- Member and Guest Accounts
- User Lifecycle
- Security Groups
- Microsoft 365 Groups
- Dynamic Groups
- Group-based Licensing
- Administrative Units
- Bulk Operations
- User and Group Governance
- Identity Administration

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Manage Microsoft Entra users.
- Manage Microsoft Entra groups.
- Configure Group-based Licensing.
- Configure Dynamic Groups.
- Delegate administration.
- Manage Guest users.
- Apply identity governance best practices.

---

## Key Takeaways

- Users represent identities within Microsoft Entra ID.
- Groups simplify permission management and license assignment.
- Dynamic Groups automate membership based on attributes.
- Group-based Licensing improves consistency and scalability.
- Proper identity governance strengthens security and simplifies administration.
