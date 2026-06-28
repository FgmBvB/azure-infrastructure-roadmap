# Microsoft Entra Groups

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Microsoft Entra groups, including group types, membership models, licensing, and common administrative tasks.

---

## Overview

Microsoft Entra groups simplify identity and access management by allowing administrators to manage permissions, licenses, and resource access collectively instead of assigning them individually.

Groups are widely used across Microsoft Entra ID, Azure RBAC, Microsoft 365, Conditional Access, Enterprise Applications, and Intune.

---

## Learning Objectives

After completing this section you should be able to:

- Understand the different Microsoft Entra group types.
- Compare assigned and dynamic membership.
- Configure Group-based Licensing.
- Manage group ownership and membership.
- Apply Microsoft best practices for group administration.

---

## Group Types

```text
Microsoft Entra Groups
        │
        ├───────────────┐
        │               │
        ▼               ▼
Security Groups   Microsoft 365 Groups
        │               │
        ▼               ▼
Permissions      Collaboration
RBAC             Teams
Applications     Outlook
Devices          SharePoint
```

---

## Security Groups

Security Groups are used to assign permissions to Azure resources and Microsoft Entra protected resources.

Common use cases include:

- Azure RBAC
- Enterprise Applications
- Conditional Access
- Microsoft Intune
- Administrative delegation

---

## Microsoft 365 Groups

Microsoft 365 Groups provide collaboration features in addition to identity management.

A Microsoft 365 Group automatically integrates with services such as:

- Microsoft Teams
- Outlook
- SharePoint Online
- Planner
- OneNote

These groups are designed primarily for collaboration rather than security administration.

---

## Membership Types

Microsoft Entra supports two membership models.

| Membership | Description |
|------------|-------------|
| **Assigned** | Administrators manually add or remove members. |
| **Dynamic** | Membership is calculated automatically using user or device attributes. |

Dynamic membership reduces administrative effort in large organizations.

---

## Group Ownership

Groups can have one or more owners.

Owners can:

- Manage group membership.
- Update group properties.
- Manage collaboration settings (Microsoft 365 Groups).

Using multiple owners helps prevent orphaned groups.

---

## Group-based Licensing

Microsoft Entra ID supports assigning licenses directly to groups.

When users become members of a licensed group, licenses are assigned automatically.

Benefits include:

- Simplified administration.
- Consistent licensing.
- Automatic onboarding.
- Automatic license removal when users leave the group.

---

## Nested Groups

Security Groups can contain other Security Groups in supported scenarios.

Nested groups simplify permission management in complex environments.

Administrators should avoid excessive nesting because it increases troubleshooting complexity.

---

## Group Management

Administrators can:

- Create groups.
- Modify properties.
- Add or remove members.
- Assign owners.
- Delete and restore groups.
- Configure dynamic membership.

Group management is available through the Microsoft Entra admin center, PowerShell, Microsoft Graph, and Azure CLI.

---

## Enterprise Scenario

A company creates Security Groups for each department.

Azure RBAC permissions, Enterprise Applications, and Conditional Access policies are assigned to these groups.

Microsoft 365 Groups are created for project teams to provide collaboration through Microsoft Teams and SharePoint.

Licenses are assigned automatically using Group-based Licensing.

---

## Best Practices

- Use Security Groups for permissions.
- Use Microsoft 365 Groups for collaboration.
- Prefer Dynamic Groups where appropriate.
- Assign multiple group owners.
- Use Group-based Licensing whenever possible.
- Follow consistent naming conventions.

---

## Common Pitfalls

- Using Microsoft 365 Groups for Azure RBAC assignments.
- Excessive nested groups.
- Managing licenses individually instead of through groups.
- Creating too many similar groups.
- Leaving groups without owners.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Security Groups
> - Microsoft 365 Groups
> - Assigned vs Dynamic Membership
> - Group-based Licensing
> - Group Ownership
> - Nested Groups

---

## Key Takeaways

- Groups simplify identity and permission management.
- Security Groups are primarily used for authorization.
- Microsoft 365 Groups focus on collaboration.
- Dynamic membership automates group administration.
- Group-based Licensing significantly reduces administrative effort.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| https://learn.microsoft.com/entra/identity/users/groups-concept | Microsoft Entra groups |
| https://learn.microsoft.com/entra/fundamentals/concept-group-based-licensing | Group-based licensing |
| https://learn.microsoft.com/entra/identity/users/groups-create-rule | Dynamic membership rules |
| https://learn.microsoft.com/microsoft-365/admin/create-groups/office-365-groups | Microsoft 365 Groups |
| https://learn.microsoft.com/training/modules/create-users-and-groups-in-azure-active-directory/ | Microsoft Learn module |
