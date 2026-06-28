# Users and Groups Best Practices

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for managing users and groups securely, efficiently, and at scale within Microsoft Entra ID.

---

## Overview

Effective user and group management is essential for maintaining a secure and well-governed Microsoft Entra environment.

Microsoft recommends automating identity management whenever possible, following the principle of least privilege, and using groups instead of individual assignments to simplify administration.

---

## Identity Management Lifecycle

```text
Create Identity
       │
       ▼
Assign Groups
       │
       ▼
Assign Licenses
       │
       ▼
Grant Resource Access
       │
       ▼
Review Permissions
       │
       ▼
Disable or Remove
```

---

> [!TIP]
> **Key Concepts**
>
> - Apply the principle of least privilege.
> - Prefer groups over individual assignments.
> - Automate administration whenever possible.
> - Review identities regularly.
> - Remove unused accounts promptly.

---

## User Management

Microsoft recommends:

- Use consistent naming conventions.
- Complete important user attributes such as Department, Job Title, and Usage Location.
- Use Group-based Licensing whenever possible.
- Review Guest accounts periodically.
- Disable inactive accounts before deleting them.
- Restore accidentally deleted users whenever appropriate instead of creating new identities.

---

## Group Management

For groups, Microsoft recommends:

- Use **Security Groups** for permissions.
- Use **Microsoft 365 Groups** for collaboration.
- Prefer **Dynamic Groups** where appropriate.
- Assign multiple group owners.
- Avoid unnecessary nested groups.
- Remove obsolete groups regularly.

---

## Licensing

To simplify administration:

- Assign licenses through groups instead of individual users.
- Verify that sufficient licenses are available.
- Monitor licensing errors regularly.
- Configure the **Usage Location** property before assigning licenses.

---

## Security

Strengthen identity security by:

- Enforcing Multi-Factor Authentication (MFA).
- Protecting privileged accounts with Conditional Access.
- Applying the principle of least privilege.
- Reviewing administrative permissions regularly.
- Monitoring sign-in activity and Audit Logs.

---

## Governance

Good governance includes:

- Regular access reviews.
- Removing inactive users and groups.
- Monitoring Guest user access.
- Reviewing Dynamic Group rules periodically.
- Documenting naming standards and ownership.

---

## Enterprise Scenario

A company standardizes identity management across multiple departments.

New employees are automatically added to Dynamic Groups based on their department, receive Microsoft 365 licenses through Group-based Licensing, and inherit access to Enterprise Applications and Azure resources through Security Groups.

Quarterly reviews identify inactive accounts, obsolete groups, and unnecessary permissions, improving security while reducing administrative effort.

---

## Best Practices Checklist

- Use Security Groups for permissions.
- Use Microsoft 365 Groups for collaboration.
- Prefer Dynamic Groups when appropriate.
- Use Group-based Licensing.
- Configure Usage Location before licensing users.
- Assign multiple group owners.
- Follow least privilege.
- Review Guest users regularly.
- Monitor licensing and audit logs.
- Remove inactive users and obsolete groups.

---

## Common Pitfalls

- Assigning permissions directly to users.
- Managing licenses individually.
- Forgetting Usage Location before licensing.
- Leaving Guest users indefinitely.
- Creating duplicate or unnecessary groups.
- Ignoring Dynamic Group validation.
- Not reviewing inactive accounts.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - User lifecycle management
> - Group management
> - Dynamic Groups
> - Group-based Licensing
> - Guest users
> - Usage Location
> - Least privilege
> - Administrative governance

---

## Key Takeaways

- Groups simplify permission and license management.
- Dynamic Groups reduce administrative overhead.
- Group-based Licensing improves consistency and scalability.
- Regular reviews strengthen governance and security.
- Proper user lifecycle management is essential for maintaining a secure Microsoft Entra environment.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Manage users](https://learn.microsoft.com/entra/identity/users/users-manage) | User lifecycle and administration |
| [Microsoft Entra groups](https://learn.microsoft.com/entra/identity/users/groups-concept) | Group concepts and management |
| [Group-based licensing](https://learn.microsoft.com/entra/fundamentals/concept-group-based-licensing) | License assignment through groups |
| [Dynamic membership rules](https://learn.microsoft.com/entra/identity/users/groups-create-rule) | Configure Dynamic Groups |
| [Microsoft Entra B2B collaboration](https://learn.microsoft.com/entra/external-id/what-is-b2b) | Guest user management |
| [Microsoft Learn – Create users and groups in Microsoft Entra ID](https://learn.microsoft.com/training/modules/create-users-and-groups-in-azure-active-directory/) | Microsoft Learn module |
