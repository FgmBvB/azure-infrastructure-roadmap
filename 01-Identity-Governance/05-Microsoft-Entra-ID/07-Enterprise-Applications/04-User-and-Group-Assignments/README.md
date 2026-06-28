# User and Group Assignments

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra ID controls access to Enterprise Applications through user and group assignments.

---

## Assignment Model

```text
          Enterprise Application
                    │
                    ▼
          User Assignment Required?
                    │
         ┌──────────┴──────────┐
         │                     │
         ▼                     ▼
      Enabled             Not Enabled
         │                     │
         ▼                     ▼
 Assigned Users        Any Tenant User
   and Groups          (if permitted)
         │
         ▼
 Authentication
         │
         ▼
 Authorization
         │
         ▼
 Application Access
```

---

> [!TIP]
> **Key Concepts**
>
> - Enterprise Applications can restrict access through assignments.
> - Users and groups can be assigned to applications.
> - Group assignments simplify administration.
> - App Roles can be assigned during user or group assignment.
> - Assignment policies work together with Conditional Access and API permissions.

---

## Overview

User and Group Assignments determine which users are allowed to access an Enterprise Application.

Assignments provide centralized access management and help organizations implement the principle of least privilege.

Instead of granting access individually, administrators can assign Microsoft Entra ID groups to simplify administration.

---

## Assignment Required

Enterprise Applications include the **Assignment required?** setting.

| Setting | Behavior |
|----------|----------|
| **Yes** | Only assigned users or groups can sign in. |
| **No** | Any user in the tenant can authenticate, provided other access requirements are satisfied. |

Enabling assignments is recommended for most enterprise applications because it limits access to authorized users only.

---

## Supported Assignments

Microsoft Entra ID supports different assignment types.

| Assignment | Supported |
|------------|-----------|
| Individual Users | Yes |
| Groups | Yes |
| App Roles | Yes |
| Dynamic Groups | Yes (through group membership) |

Groups significantly reduce administrative effort in large organizations.

---

## User Assignments

Individual users can be assigned directly to an Enterprise Application.

This approach is appropriate for:

- Small environments.
- Testing.
- Temporary access.

For large organizations, Microsoft recommends assigning groups instead of individual users.

---

## Group Assignments

Groups allow administrators to grant application access to multiple users simultaneously.

When a user becomes a member of an assigned group, access is inherited automatically.

Removing the user from the group immediately removes access to the Enterprise Application.

This simplifies lifecycle management and reduces administrative overhead.

> [!NOTE]
>
> Assigning App Roles directly to groups for Enterprise Applications requires Microsoft Entra ID Premium (P1 or P2).
>
> Organizations using Microsoft Entra ID Free may need to assign App Roles directly to individual users, depending on the application and assignment scenario.

---

## Nested Groups

Microsoft Entra ID does **not** support nested group evaluation for Enterprise Application assignments.

Only **direct members** of an assigned group receive access to the application.

For example:

```text
Group A
   │
Assigned to Application
   │
   ▼
Group B
   │
   ▼
User
```

In this scenario, the user in **Group B** does **not** inherit access through the nested group relationship.

Administrators should assign users directly or use groups with direct membership when controlling application access.

---

## App Role Assignments

Enterprise Applications can expose one or more **App Roles**.

During assignment, administrators may assign users or groups directly to one of these roles.

Examples include:

| App Role | Example |
|----------|---------|
| Reader | Read-only access |
| Contributor | Standard user |
| Administrator | Full application management |

Assigned App Roles are included in the Access Token and can be used by the application to implement authorization.

---

## Default Access

If an Enterprise Application does not define custom **App Roles**, Microsoft Entra ID assigns users or groups the built-in **Default Access** role.

This role allows users to authenticate to the application but does not provide application-specific authorization.

As a result, the Access Token typically does not contain application role values in the `roles` claim, and authorization decisions are handled by the application itself.

---

## Assignment Evaluation

When a user attempts to sign in:

```text
User
   │
   ▼
Microsoft Entra ID
   │
   ▼
Enterprise Application
   │
Assignment Required?
   │
   ▼
User or Group Assigned?
   │
 ┌─┴───────────────┐
 │                 │
 ▼                 ▼
Yes               No
 │                 │
 ▼                 ▼
Authentication   Access Denied
 │
 ▼
Conditional Access
 │
 ▼
Application Access
```

Assignments are evaluated before access to the application is granted.

> [!NOTE]
>
> If **Assignment required?** is enabled and a user who has not been assigned attempts to sign in, Microsoft Entra ID blocks the authentication request and returns the error:
>
> **AADSTS50105**
>
> *The signed in user is not assigned to a role for the application.*
>
> This is one of the most common troubleshooting scenarios for Enterprise Applications.

---

## Relationship with Conditional Access

Assignments determine **who may access** the application.

Conditional Access determines **under which conditions** access is allowed.

For example:

- User is assigned.
- MFA is required.
- Device must be compliant.
- Sign-in risk must be acceptable.

Both mechanisms work together to protect Enterprise Applications.

---

## Enterprise Scenario

A company deploys an internal HR application.

The Enterprise Application is configured with **Assignment required? = Yes**.

Instead of assigning employees individually, the administrator assigns the **HR Employees** group.

When new employees join the HR department, they automatically receive access through group membership.

If an employee leaves the department, removing them from the group immediately revokes access.

---

## Best Practices

- Enable **Assignment required?** whenever possible.
- Assign groups instead of individual users.
- Use App Roles for application authorization.
- Review assignments regularly.
- Remove unused assignments.
- Combine assignments with Conditional Access policies.

---

## Common Pitfalls

- Leaving **Assignment required?** disabled unnecessarily.
- Assigning users individually in large environments.
- Forgetting to remove inactive users.
- Ignoring App Roles.
- Assuming assignments replace Azure RBAC or API permissions.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - User assignments
> - Group assignments
> - Assignment required
> - App Roles
> - Conditional Access integration
> - Least privilege

---

## Key Takeaways

- Assignments control who can access Enterprise Applications.
- Groups simplify access management.
- App Roles provide application-level authorization.
- Conditional Access evaluates how users authenticate.
- Assignments should follow the principle of least privilege.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Assign users and groups to an application](https://learn.microsoft.com/entra/identity/enterprise-apps/assign-user-or-group-access-portal) | User and Group assignments |
| [Manage users and groups assignment to an application](https://learn.microsoft.com/entra/identity/enterprise-apps/assign-user-or-group-access-portal) | Assignment management |
| [Application Objects and Service Principals](https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals) | Service Principals |
| [Application roles](https://learn.microsoft.com/entra/identity-platform/howto-add-app-roles-in-apps) | App Roles |
| [Microsoft Learn – Manage application access](https://learn.microsoft.com/training/modules/manage-users-and-groups-in-aad/) | Microsoft Learn module |
