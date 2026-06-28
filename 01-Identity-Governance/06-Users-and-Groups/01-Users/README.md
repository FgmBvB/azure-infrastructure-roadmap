# Microsoft Entra Users

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Microsoft Entra user accounts, user lifecycle management, licensing, guest users, bulk operations, and common administrative tasks.

---

## Overview

Microsoft Entra ID stores and manages user identities for Azure, Microsoft 365, and other integrated cloud applications.

Administrators can create, modify, license, and delete user accounts while controlling authentication and access to organizational resources.

User management is one of the most common administrative tasks in Microsoft Entra ID and is a core objective of the AZ-104 certification.

---

## Learning Objectives

After completing this section you should be able to:

- Create and manage Microsoft Entra users.
- Differentiate Member and Guest accounts.
- Manage user properties and licenses.
- Perform bulk user operations.
- Restore deleted users.
- Understand the user lifecycle.
- Apply Microsoft best practices.

---

## User Lifecycle

```text
Create User
     │
     ▼
Assign License
     │
     ▼
Configure Access
     │
     ▼
Manage User
     │
     ▼
Disable / Delete
     │
     ▼
Restore (if required)
```

---

## User Types

Microsoft Entra ID supports different user account types.

| User Type | Description |
|-----------|-------------|
| **Member** | Internal user belonging to the organization. |
| **Guest** | External user invited through Microsoft Entra B2B collaboration. |

Member users typically receive licenses and corporate resources, while Guest users are commonly used for collaboration with external partners.

---

## User Properties

Each user object contains identity information such as:

- Display Name
- User Principal Name (UPN)
- Email Address
- Department
- Job Title
- Usage Location
- Manager
- Assigned Licenses

These properties can be used for administration, reporting, and Dynamic Group membership.

---

## User Management

Administrators can perform common tasks such as:

- Create users.
- Edit user properties.
- Reset passwords.
- Block sign-in.
- Delete users.
- Restore deleted users.
- Assign or remove licenses.

Most user management tasks can be performed from the Microsoft Entra admin center, Azure PowerShell, Microsoft Graph, or Azure CLI.

---

## Guest Users (B2B)

Guest users allow organizations to collaborate securely with external users.

Typical scenarios include:

- Business partners.
- Contractors.
- Vendors.
- Customers.
- External consultants.

Guest users authenticate using their existing identity provider while access is governed through Microsoft Entra ID.

---

## License Assignment

Licenses enable Microsoft cloud services.

Licenses can be assigned:

- Individually.
- Through Group-based Licensing.
- Using automation tools.

Common Microsoft licenses include Microsoft 365 and Microsoft Entra ID Premium.

---

## Bulk Operations

Microsoft Entra ID supports bulk administration for large environments.

Examples include:

- Bulk user creation.
- Bulk updates.
- Bulk deletion.
- Bulk license assignment.

Bulk operations are commonly performed using CSV files, PowerShell, or Microsoft Graph.

---

## Deleted Users

Deleted users are temporarily retained before permanent removal.

During the retention period administrators can:

- Restore the user account.
- Recover assigned properties.
- Reassign licenses if necessary.

Permanent deletion removes the identity from Microsoft Entra ID.

---

## Enterprise Scenario

A company hires fifty new employees.

The IT department imports users using a CSV file, assigns Microsoft 365 licenses through Group-based Licensing, applies Conditional Access policies, and adds users to department-specific Security Groups.

External consultants receive Guest accounts through Microsoft Entra B2B collaboration.

---

## Best Practices

- Follow the principle of least privilege.
- Use Group-based Licensing whenever possible.
- Review Guest accounts regularly.
- Populate user properties consistently.
- Use bulk operations for large deployments.
- Remove inactive accounts promptly.

---

## Common Pitfalls

- Assigning licenses manually at scale.
- Forgetting Usage Location before licensing.
- Leaving Guest accounts unmanaged.
- Creating inconsistent naming conventions.
- Not reviewing inactive users.
- Permanently deleting users unnecessarily.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Member vs Guest users
> - User lifecycle
> - User properties
> - License assignment
> - Bulk operations
> - Deleted user recovery

---

## Key Takeaways

- Microsoft Entra ID manages organizational user identities.
- Member and Guest accounts serve different collaboration scenarios.
- Group-based Licensing simplifies license management.
- Bulk operations improve administration in large environments.
- Proper user lifecycle management improves security and governance.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| https://learn.microsoft.com/entra/identity/users/users-manage | Manage users |
| https://learn.microsoft.com/entra/external-id/what-is-b2b | Microsoft Entra B2B |
| https://learn.microsoft.com/entra/fundamentals/concept-group-based-licensing | Group-based licensing |
| https://learn.microsoft.com/entra/fundamentals/how-to-manage-user-profile-info | User properties |
| https://learn.microsoft.com/training/modules/create-users-and-groups-in-azure-active-directory/ | Microsoft Learn module |
