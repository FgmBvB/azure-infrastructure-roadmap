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
> - Users are security principals.
> - Every user has a unique Object ID.
> - Users authenticate through Microsoft Entra ID.
> - Permissions are assigned through Azure RBAC or Microsoft Entra ID roles.
> - Users can be cloud-only, synchronized, or external.

---

## Overview

A user is a digital identity that represents a person within Microsoft Entra ID.

Users authenticate to Microsoft cloud services and applications using credentials such as passwords, passwordless authentication, certificates, or federated identities.

Every user is represented by a unique object stored in the Microsoft Entra ID directory.

Users are one of the most common Security Principals used throughout Microsoft Azure.

---

## User Types

Microsoft Entra ID supports multiple user types.

| User Type | Description |
|------------|-------------|
| Cloud User | Created and managed directly in Microsoft Entra ID. |
| Synchronized User | Synchronized from on-premises Active Directory using Microsoft Entra Connect. |
| Guest User | External user invited through Microsoft Entra External ID (B2B collaboration). |

Each user type supports different identity management scenarios.

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

The **Object ID** uniquely identifies the user within the tenant and never changes during the lifetime of the object.

---

## User Principal Name (UPN)

The User Principal Name (UPN) is the username that users typically enter when signing in.

A UPN follows an email-like format.

Example:

```text
john.doe@contoso.com
```

The UPN does not need to match the user's email address, although many organizations use the same value for simplicity.

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

These operations can be performed through the Microsoft Entra admin center, Microsoft Graph, PowerShell, or Azure CLI (where supported).

---

## User States

A user account can exist in different operational states.

| State | Description |
|--------|-------------|
| Enabled | The user can authenticate. |
| Disabled | Authentication is blocked but the object remains in the directory. |
| Deleted | The object is moved to the recycle bin for a limited retention period before permanent deletion. |

Soft-deleted users can typically be restored during the retention period.

---

## Enterprise Scenario

A new employee joins the company.

An administrator creates a cloud user in Microsoft Entra ID, assigns the appropriate Microsoft 365 license, adds the user to security groups, configures authentication methods, and grants access to Azure resources through Azure RBAC.

When the employee signs in, Microsoft Entra ID authenticates the identity before Azure RBAC authorizes access to the required resources.

---

## Best Practices

- Use meaningful User Principal Names.
- Assign permissions through groups whenever possible.
- Protect privileged accounts with Multi-Factor Authentication.
- Disable unused accounts promptly.
- Review guest users regularly.
- Apply the principle of least privilege.
- Keep user information up to date.

---

## Common Pitfalls

- Assigning permissions directly to individual users.
- Forgetting to disable former employee accounts.
- Confusing the Object ID with the User Principal Name.
- Using excessive Global Administrator accounts.
- Leaving inactive guest accounts in the tenant.

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
> - Guest users
> - User Principal Name (UPN)
> - Object ID
> - User lifecycle
> - User management

---

## Key Takeaways

- Users are Security Principals.
- Every user has a unique Object ID.
- Users authenticate through Microsoft Entra ID.
- A UPN is commonly used for sign-in.
- Permissions are assigned separately through Azure RBAC or Microsoft Entra ID roles.
- Users can be cloud-only, synchronized, or external.
- Proper lifecycle management improves security.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| https://learn.microsoft.com/entra/fundamentals/how-to-create-delete-users | User management |
| https://learn.microsoft.com/entra/fundamentals/concept-secure-remote-workers | User identities |
| https://learn.microsoft.com/entra/external-id/what-is-b2b | Guest users |
| https://learn.microsoft.com/graph/api/resources/user | User object properties |
| https://learn.microsoft.com/training/modules/explore-basic-services-identity-types/ | Microsoft Learn – User identities |
