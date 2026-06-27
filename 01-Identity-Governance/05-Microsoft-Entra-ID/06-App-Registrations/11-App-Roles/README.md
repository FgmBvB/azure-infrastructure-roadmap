# App Roles

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how App Roles allow applications to implement their own authorization model independently of Azure RBAC.

---

## Authorization Model

```text
             Application
                   │
                   ▼
        Application Object
                   │
          Defines App Roles
                   │
                   ▼
        Service Principal
                   │
     Assign Users or Groups
                   │
                   ▼
         Access Application
                   │
                   ▼
   Application Evaluates Role
```

---

> [!TIP]
> **Key Concepts**
>
> * App Roles define application-specific authorization.
> * App Roles are configured in the Application Object.
> * Users, groups, or Service Principals can be assigned App Roles.
> * App Roles are different from Azure RBAC roles.
> * Applications evaluate App Roles after authentication.

---

## Overview

App Roles allow developers to define authorization roles that are specific to an application.

Unlike Azure RBAC, which controls access to Azure resources, App Roles control what authenticated identities can do inside an application.

Applications evaluate these roles after Microsoft Entra ID successfully authenticates the user or application.

---

## Why App Roles Exist

Authentication confirms the identity of a user or application.

Authorization determines what that identity is allowed to do.

App Roles allow applications to implement their own authorization model without relying on Azure RBAC.

This enables consistent access control regardless of where the application is hosted.

---

## Where App Roles Are Defined

App Roles are defined in the **Application Object**.

The role definitions become available to every Service Principal created from that Application Object.

Each tenant can then assign those App Roles to users, groups, or other applications according to its own administrative requirements.

---

## App Role Definition

App Roles are defined in the `appRoles` section of the Application Object manifest.

Each App Role includes several properties:

| Property | Purpose |
|----------|---------|
| `id` | Globally unique identifier (GUID) of the App Role. |
| `value` | String value that applications use for authorization (for example, `Expense.Manager`). |
| `displayName` | Human-readable name displayed to administrators. |
| `description` | Explains the purpose of the App Role. |
| `allowedMemberTypes` | Specifies whether the role can be assigned to `User`, `Application`, or both. |

These properties define how Microsoft Entra ID exposes App Roles to administrators and applications.

---

## Supported Assignments

Microsoft Entra ID allows App Roles to be assigned to different identity types.

| Identity           | Supported |
| ------------------ | --------- |
| Users              | Yes       |
| Groups             | Yes       |
| Service Principals | Yes       |

This flexibility supports both interactive users and application-to-application authorization.

> [!NOTE]
>
> Assigning App Roles directly to groups for enterprise applications requires Microsoft Entra ID Premium (P1 or P2).
>
> Organizations using Microsoft Entra ID Free may need to assign App Roles directly to individual users, depending on the application and assignment scenario.

---

## App Roles vs Azure RBAC

Although both use the term "role", they control different authorization models.

| App Roles                                    | Azure RBAC                              |
| -------------------------------------------- | --------------------------------------- |
| Control authorization inside an application. | Control access to Azure resources.      |
| Defined by application developers.           | Defined by Microsoft or administrators. |
| Stored in the Application Object.            | Stored as Azure Role Definitions.       |
| Evaluated by the application.                | Evaluated by Azure Resource Manager.    |

---

## App Roles in Tokens

When an App Role is assigned, Microsoft Entra ID includes it in the Access Token inside the `roles` claim.

The `roles` claim is returned as an array, allowing multiple App Roles to be assigned to the same identity.

Applications evaluate these values to determine which operations the authenticated identity is authorized to perform.

---

## Enterprise Scenario

A company develops an internal expense management application.

The application defines three App Roles:

* Employee
* Manager
* Finance Administrator

After users authenticate with Microsoft Entra ID, the application reads the assigned App Role from the Access Token.

Managers can approve expenses, while Finance Administrators can generate financial reports.

---

## Best Practices

* Keep App Roles focused on business functions.
* Apply the principle of least privilege.
* Assign App Roles to groups whenever possible.
* Avoid assigning roles directly to individual users.
* Review App Role assignments regularly.

---

## Common Pitfalls

* Confusing App Roles with Azure RBAC roles.
* Using App Roles to manage Azure resources.
* Creating too many overlapping roles.
* Assigning excessive permissions.
* Ignoring regular access reviews.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> * App Roles
> * Application authorization
> * App Role assignments
> * App Roles vs Azure RBAC
> * Application Object
> * Service Principal

---

## Key Takeaways

* App Roles define authorization inside an application.
* App Roles are stored in the Application Object.
* Users, groups, and Service Principals can receive App Roles.
* Applications evaluate App Roles after authentication.
* App Roles are independent of Azure RBAC.

---

## References

| Microsoft Documentation                                                                                                                          | Purpose                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------- |
| [Add app roles to your application](https://learn.microsoft.com/entra/identity-platform/howto-add-app-roles-in-apps)                             | Configure App Roles        |
| [Application Objects and Service Principals](https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals)             | Identity model             |
| [Permissions and consent overview](https://learn.microsoft.com/entra/identity-platform/permissions-consent-overview)                             | Application permissions    |
| [Microsoft identity platform](https://learn.microsoft.com/entra/identity-platform/)                                                              | Identity platform overview |
| [Microsoft Learn – Build applications that authenticate users](https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/) | Microsoft Learn module     |

