# Users

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how user identities are created, managed, and authenticated within Microsoft Entra ID.

---

## User Lifecycle

```text
      Create User
           │
           ▼
 Assign Identity
           │
           ▼
 Assign Groups
           │
           ▼
 Assign Licenses
           │
           ▼
 Authentication
           │
           ▼
 Authorization
           │
           ▼
 Manage / Disable / Delete
```

---

> [!TIP]
> **Key Concepts**
>
> - Users are Security Principals.
> - Every user has a unique Object ID.
> - Users authenticate through Microsoft Entra ID.
> - Permissions are assigned through Azure RBAC or Microsoft Entra ID roles.
> - Users can be cloud-only, synchronized, or external.

---

## Overview

A user is a digital identity that represents a person within Microsoft Entra ID.

Users authenticate to Microsoft cloud services and applications using passwords, passwordless authentication, certificates, or federated identities.

Every user is represented by a unique object stored in the Microsoft Entra ID directory.

Users are one of the most common Security Principals used throughout Microsoft Azure.

---

## User Types

Microsoft Entra ID supports different identity origins and user types.

| Identity Origin | Typical UserType | Description |
|-----------------|------------------|-------------|
| Cloud User | Member | Created and managed directly in Microsoft Entra ID. |
| Synchronized User | Member | Synchronized from on-premises Active Directory using Microsoft Entra Connect. |
| External User | Guest (default) | Invited through Microsoft Entra External ID (B2B collaboration). |

The **UserType** attribute determines whether a user is treated as a **Member** or **Guest** within the Microsoft Entra ID directory.

Although external users are typically created as **Guest**, organizations can configure other scenarios when required by business needs.

---

## User Object

Every user object contains identity information used for authentication and administration.

Common properties include:

- User Principal Name (UPN)
- Display Name
- Object ID
- Mail
- Department
- Job Title
- Usage Location
- Account Status

The **Object ID** uniquely identifies the user within the tenant and remains immutable throughout the lifetime of the user object.

---

## User Principal Name (UPN)

The User Principal Name (UPN) is the username that users typically enter when signing in.

A UPN follows an email-like format.

Example:

```text
john.doe@contoso.com
```

The UPN does not need to match the user's email address, although many organizations use the same value for simplicity.

Unlike the Object ID, the UPN can be changed if the user's name changes or if the organization changes its domain.

For integrations, automation, and external applications, Microsoft recommends using the immutable **Object ID** whenever possible.

---

## User Management

Administrators can perform common user management tasks, including:

- Create users
- Update user properties
- Reset passwords
- Enable or disable accounts
- Delete or restore users
- Assign licenses
- Assign administrative roles
- Manage authentication methods
- Perform bulk user operations

These operations can be performed through:

- Microsoft Entra admin center
- Microsoft Graph
- Microsoft Graph PowerShell
- Azure CLI (where supported)

In enterprise environments, licenses are commonly assigned through groups rather than directly to individual users. This simplifies administration and automatically applies licenses as users join or leave the appropriate groups.

Large organizations also automate user provisioning through Microsoft Graph, PowerShell, or bulk import operations.

---

## User States

User accounts move through different lifecycle states during their existence.

```text
Enabled
    │
    ▼
Disabled
    │
    ▼
Soft Deleted (30 days)
    │
    ▼
Hard Deleted (Permanent)
```

| State | Description |
|--------|-------------|
| Enabled | The user can authenticate and access assigned resources. |
| Disabled | Authentication is blocked, but the user object remains in the directory. |
| Soft Deleted | The user is moved to the recycle bin and can be restored within 30 days. |
| Hard Deleted | After the retention period expires, the user object is permanently removed and cannot be recovered. |

When a user is restored during the soft-delete period, Microsoft Entra ID restores the user object together with its previous group memberships, assigned licenses, and many associated properties.

---

## Enterprise Scenario

A new employee joins the company.

An administrator creates a cloud user in Microsoft Entra ID, assigns the user to the appropriate security groups, and grants the required Microsoft 365 licenses through group-based licensing.

Authentication methods are configured, and Azure RBAC permissions are inherited from the user's group memberships.

When the employee signs in, Microsoft Entra ID authenticates the identity before Azure RBAC authorizes access to Azure resources.

When the employee leaves the company, the account is disabled immediately to prevent access.

After the retention period and organizational validation, the user account is permanently removed if no longer required.

---

## Best Practices

- Use meaningful User Principal Names (UPNs).
- Assign permissions through groups instead of directly to users.
- Use group-based licensing whenever possible.
- Protect privileged accounts with Multi-Factor Authentication.
- Disable unused accounts immediately.
- Review guest users regularly.
- Apply the principle of least privilege.
- Keep user information up to date.
- Automate user provisioning whenever possible.

---

## Common Pitfalls

- Assigning permissions directly to individual users.
- Confusing the Object ID with the User Principal Name (UPN).
- Forgetting to disable former employee accounts.
- Assigning licenses manually instead of using groups.
- Leaving inactive guest accounts in the tenant.
- Creating excessive Global Administrator accounts.
- Relying on mutable identifiers such as UPN in automation scripts.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - User identities
> - User object properties
> - Cloud users
> - Synchronized users
> - External users
> - Member and Guest user types
> - User Principal Name (UPN)
> - Object ID
> - User lifecycle
> - Soft Delete and Hard Delete
> - User management operations

---

## Key Takeaways

- Users are Security Principals within Microsoft Entra ID.
- Every user has a globally unique and immutable Object ID.
- The User Principal Name (UPN) is commonly used for sign-in but can change.
- Users authenticate through Microsoft Entra ID.
- Permissions are assigned separately through Azure RBAC or Microsoft Entra ID administrative roles.
- Users can originate from the cloud, on-premises synchronization, or external organizations.
- Group-based licensing simplifies administration at enterprise scale.
- Soft-deleted users can be restored during the retention period before permanent deletion.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Manage users in Microsoft Entra ID](https://learn.microsoft.com/entra/fundamentals/how-to-create-delete-users) | User lifecycle and administration |
| [Microsoft Graph User resource](https://learn.microsoft.com/graph/api/resources/user) | User object properties |
| [Microsoft Entra External ID](https://learn.microsoft.com/entra/external-id/what-is-b2b) | External and guest users |
| [Group-based licensing](https://learn.microsoft.com/entra/fundamentals/concept-group-based-licensing) | Assigning licenses through groups |
| [Restore or remove a deleted user](https://learn.microsoft.com/entra/fundamentals/how-to-create-delete-users#restore-or-remove-a-recently-deleted-user) | Soft Delete and Hard Delete |
| [Microsoft Learn – Identity types](https://learn.microsoft.com/training/modules/explore-basic-services-identity-types/) | Microsoft Learn module |
