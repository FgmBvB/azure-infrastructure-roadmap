# Provisioning

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra ID automatically provisions, updates, and removes user accounts in integrated applications.

---

## Provisioning Overview

```text
        Microsoft Entra ID
                │
                ▼
      User / Group Changes
                │
                ▼
      Provisioning Service
                │
     ┌──────────┴──────────┐
     │                     │
     ▼                     ▼
 Create / Update      Disable / Delete
     │                     │
     └──────────┬──────────┘
                ▼
      Enterprise Application
```

---

> [!TIP]
> **Key Concepts**
>
> - Provisioning automates identity lifecycle management.
> - Users and groups can be created, updated, or removed automatically.
> - Microsoft Entra ID supports SCIM-based provisioning.
> - Provisioning reduces manual administration.
> - Automatic deprovisioning improves security.

---

## Overview

Provisioning is the process of automatically creating, updating, and removing user accounts in connected applications.

Instead of manually managing user accounts in every application, Microsoft Entra ID synchronizes identity information based on organizational changes.

Provisioning helps ensure that users always have the correct level of access throughout their lifecycle.

---

## Why Provisioning Exists

Without provisioning:

- User accounts must be created manually.
- User information becomes inconsistent.
- Departing employees may retain access.
- Administrative effort increases.

Provisioning automates these processes while improving security and compliance.

---

## Provisioning Lifecycle

```text
User Created
      │
      ▼
Provision Account
      │
      ▼
Update Attributes
      │
      ▼
Role Changes
      │
      ▼
Disable Account
      │
      ▼
Deprovision Account
```

---

## Supported Operations

Microsoft Entra ID supports several provisioning actions.

| Operation | Description |
|-----------|-------------|
| Create | Creates a new account in the application. |
| Update | Synchronizes user attribute changes. |
| Disable | Disables access when appropriate. |
| Delete | Removes the account if supported. |
| Group Assignment | Synchronizes assigned groups when supported. |

The supported operations depend on the target application.

---

## SCIM

Many Enterprise Applications support **System for Cross-domain Identity Management (SCIM)**.

SCIM is an open standard that allows Microsoft Entra ID to provision identities automatically.

Typical synchronized attributes include:

- Display Name
- User Principal Name (UPN)
- Email Address
- Department
- Job Title
- Manager

Microsoft Entra ID maps these attributes to the application's user schema.

---

## Attribute Mapping

Provisioning uses attribute mappings to determine how Microsoft Entra ID attributes correspond to application attributes.

For example:

| Microsoft Entra ID | Application |
|--------------------|-------------|
| UserPrincipalName | username |
| DisplayName | displayName |
| Mail | email |
| Department | department |

Administrators can customize attribute mappings depending on the application's schema.

---

## Matching Precedence

Provisioning must determine whether a user already exists in the target application before creating a new account.

Microsoft Entra ID uses one or more **matching attributes** to identify existing users.

Common matching attributes include:

- User Principal Name (UPN)
- Email Address
- Employee ID

When multiple matching attributes are configured, **Matching Precedence** determines the order in which they are evaluated.

If a matching account is found, Microsoft Entra ID links the existing account instead of creating a duplicate user.

Correct matching configuration helps prevent duplicate identities and provisioning errors.

---

## Scope

Provisioning can synchronize:

| Scope | Description |
|--------|-------------|
| Assigned Users | Only assigned users are provisioned. |
| Assigned Groups | Members of assigned groups are provisioned. |
| All Users | Synchronizes every supported user in the tenant. |

Most organizations provision only assigned users and groups to reduce unnecessary accounts.

---

## Scoping Filters

Scoping Filters provide an additional level of control over which users are provisioned.

These filters evaluate user attributes before synchronization occurs.

Examples include:

- Department equals **Sales**
- Country equals **United States**
- Employee Type equals **Full-Time**

Even if a user belongs to an assigned group, Microsoft Entra ID does not provision the account unless all configured Scoping Filter conditions are satisfied.

Scoping Filters help reduce unnecessary provisioning and support organizational policies.

---

## Deprovisioning

Provisioning also manages user removal.

When a user:

- Leaves the organization.
- Is removed from an assigned group.
- Is disabled.
- Loses application assignment.

Microsoft Entra ID can automatically disable or remove the corresponding account in the target application.

Automatic deprovisioning significantly reduces the risk of orphaned accounts.

---

## Provisioning Logs

Microsoft Entra ID records provisioning activity.

Administrators can review:

- Successful synchronizations.
- Failed operations.
- Attribute mapping errors.
- Account creation failures.
- Deprovisioning events.

Provisioning logs are an important troubleshooting resource.

---

## Quarantine

Microsoft Entra ID automatically protects the provisioning service when repeated synchronization failures occur.

Common causes include:

- Expired administrator credentials.
- Invalid API credentials.
- Schema or attribute mapping errors.
- Target application connectivity issues.

When excessive provisioning failures are detected, the provisioning job enters **Quarantine**.

While in this state, synchronization frequency is significantly reduced until the underlying issue is resolved.

After correcting the problem, administrators can restart the provisioning job to resume normal synchronization.

---

## Relationship with Assignments

Provisioning works together with Enterprise Application assignments.

```text
User Assigned
       │
       ▼
Provisioning Service
       │
       ▼
Application Account Created
       │
       ▼
User Signs In
```

Removing the assignment can automatically trigger deprovisioning if supported by the application.

---

## Enterprise Scenario

A company integrates Workday with Microsoft Entra ID.

When a new employee joins the organization, Microsoft Entra ID automatically provisions an account in Workday using SCIM.

If the employee changes departments, the updated information is synchronized automatically.

When the employee leaves the company, Microsoft Entra ID deprovisions the account, removing access without manual intervention.

---

## Best Practices

- Provision only assigned users and groups.
- Review attribute mappings before enabling provisioning.
- Monitor provisioning logs regularly.
- Validate synchronization with test accounts.
- Remove orphaned accounts.
- Use SCIM whenever supported.

---

## Common Pitfalls

- Incorrect attribute mappings.
- Provisioning all users unnecessarily.
- Ignoring provisioning failures.
- Forgetting to monitor synchronization logs.
- Assuming every application supports SCIM.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Provisioning
> - Deprovisioning
> - SCIM
> - Attribute Mapping
> - Provisioning Scope
> - Provisioning Logs

---

## Key Takeaways

- Provisioning automates user lifecycle management.
- SCIM is the preferred provisioning standard.
- Attribute mappings determine synchronized data.
- Deprovisioning improves security by removing unused accounts.
- Provisioning logs help troubleshoot synchronization issues.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Automatic user provisioning in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/app-provisioning/user-provisioning) | Provisioning overview |
| [SCIM provisioning with Microsoft Entra ID](https://learn.microsoft.com/entra/identity/app-provisioning/use-scim-to-provision-users-and-groups) | SCIM integration |
| [Customize application attribute mappings](https://learn.microsoft.com/entra/identity/app-provisioning/customize-application-attributes) | Attribute mapping |
| [Provisioning logs in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/monitoring-health/concept-provisioning-logs) | Monitoring and troubleshooting |
| [Microsoft Learn – Provision users to applications](https://learn.microsoft.com/training/modules/plan-user-provisioning/) | Microsoft Learn module |
