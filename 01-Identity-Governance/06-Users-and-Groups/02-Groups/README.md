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

### Dynamic Group Limitations

Dynamic Groups automatically calculate membership based on Microsoft Entra attributes.

Important limitations include:

- A Dynamic Group can be configured as either **Dynamic User** or **Dynamic Device**.
- A single Dynamic Group cannot contain both users and devices.
- Dynamic Groups evaluate only the supported object type defined during creation.
- Dynamic membership requires Microsoft Entra ID Premium P1 or P2 licensing for the users covered by the rule.

Dynamic Groups simplify administration by automatically updating membership whenever the evaluated attributes change.

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

Important considerations include:

- Microsoft 365 Groups do **not** support nested group membership.
- Dynamic Groups cannot contain other groups as members.
- Excessive nesting increases administrative complexity and can complicate troubleshooting.
- Not every Microsoft Entra feature evaluates nested group membership in the same way.

Administrators should validate whether a specific Azure service supports nested groups before relying on indirect membership for authorization.

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

## Deleted Groups

The recovery behavior depends on the group type.

| Group Type | Recovery |
|------------|----------|
| **Microsoft 365 Group** | Supports soft deletion for 30 days and can be restored. |
| **Security Group** | Recovery capabilities depend on the deletion mechanism and Microsoft Entra features available in the tenant. |

Restoring a Microsoft 365 Group also restores its associated collaboration resources, such as the SharePoint site, Outlook mailbox, Microsoft Teams team, and Planner content.

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
| [Microsoft Entra groups](https://learn.microsoft.com/entra/identity/users/groups-concept) | Group concepts and management |
| [Group-based licensing](https://learn.microsoft.com/entra/fundamentals/concept-group-based-licensing) | Assign licenses through groups |
| [Dynamic membership rules](https://learn.microsoft.com/entra/identity/users/groups-create-rule) | Create dynamic groups |
| [Microsoft 365 Groups](https://learn.microsoft.com/microsoft-365/admin/create-groups/office-365-groups) | Collaboration groups |
| [Microsoft Learn module](https://learn.microsoft.com/training/modules/create-users-and-groups-in-azure-active-directory/) | AZ-104 learning path |
