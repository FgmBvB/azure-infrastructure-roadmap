# Authorization

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra ID authorizes applications to access protected APIs and Azure resources after successful authentication.

---

## Authorization Flow

```text
      Application
            │
            ▼
Authentication
(Successful)
            │
            ▼
 Access Token
            │
            ▼
 Protected API
(Microsoft Graph / ARM)
            │
            ▼
Permission Evaluation
            │
      ┌─────┴─────┐
      │           │
 Authorized   Not Authorized
      │           │
      ▼           ▼
 Access      Access Denied
 Granted
```

---

> [!TIP]
> **Key Concepts**
>
> * Authorization determines what an authenticated application can access.
> * Authentication always occurs before authorization.
> * Applications access resources through API permissions.
> * Microsoft Entra ID issues tokens, but target resources evaluate permissions.
> * Least privilege should always be applied.

---

## Overview

After an application successfully authenticates with Microsoft Entra ID, it must still be authorized before accessing protected resources.

Authorization determines which APIs, Azure resources, or services an application is allowed to access.

Authentication answers:

> **Who is the application?**

Authorization answers:

> **What is the application allowed to do?**

---

## Authentication vs Authorization

| Authentication                      | Authorization                              |
| ----------------------------------- | ------------------------------------------ |
| Verifies the application's identity | Determines what the application can access |
| Performed by Microsoft Entra ID     | Evaluated by the target resource           |
| Issues security tokens              | Evaluates API permissions                  |
| Happens first                       | Happens after authentication               |

Authentication alone never grants access.

---

## API Permissions

Applications access protected resources through API permissions.

Typical resources include:

* Microsoft Graph
* Azure Resource Manager
* Azure Key Vault
* Azure Storage
* Custom APIs

Permissions are granted during application configuration and evaluated whenever the application presents an Access Token.

---

## Permission Types

Microsoft Entra ID supports two primary permission models.

| Permission Type         | Description                                                  |
| ----------------------- | ------------------------------------------------------------ |
| Delegated Permissions   | The application acts on behalf of a signed-in user.          |
| Application Permissions | The application acts independently without a signed-in user. |

The selected permission model depends on how the application is designed.

---

## Delegated Permissions

Delegated permissions are used when a user is signed in.

The application receives only the permissions that are allowed both by:

* The user's own permissions.
* The permissions granted to the application.

The effective permissions are therefore limited by both identities.

Typical examples include:

* Microsoft Teams
* Outlook
* Microsoft 365 applications
* Internal business applications

---

## Application Permissions

Application permissions are used when no user is present.

The application authenticates using its own identity and receives permissions directly.

This model is commonly used for:

* Background services
* Scheduled automation
* Azure Functions
* Daemons
* CI/CD pipelines

Because these permissions can provide broad access, they often require administrator approval.

---

## Admin Consent

Some API permissions require administrator approval before applications can use them.

Administrator consent is commonly required for high-privilege permissions such as directory-wide access or operations affecting multiple users.

Once granted, the application can request those permissions without requiring individual user consent.

---

## Permission Evaluation

Authorization is evaluated by the resource receiving the Access Token.

The resource validates:

* Token signature
* Token expiration
* Requested permission
* Granted permission
* Tenant policies

Only after successful validation is access granted.

---

## Enterprise Scenario

A scheduled Azure Automation job needs to read all users from Microsoft Graph every night.

Because no interactive user is present, the application authenticates using its own identity and requests **Application Permissions**.

Microsoft Entra ID issues an Access Token, and Microsoft Graph authorizes the request according to the permissions previously granted through administrator consent.

---

## Best Practices

* Apply the principle of least privilege.
* Grant only the permissions required.
* Prefer Delegated Permissions whenever possible.
* Grant Application Permissions only when necessary.
* Review administrator consent regularly.
* Remove unused API permissions.
* Audit application permissions periodically.

---

## Common Pitfalls

* Confusing authentication with authorization.
* Assuming an Access Token automatically grants access.
* Granting excessive Application Permissions.
* Forgetting to review administrator consent.
* Ignoring the principle of least privilege.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> * Application authorization
> * API permissions
> * Delegated Permissions
> * Application Permissions
> * Admin Consent
> * Least privilege
> * Authentication versus authorization

---

## Key Takeaways

* Authentication identifies the application.
* Authorization determines what the application can access.
* API permissions control access to protected resources.
* Delegated Permissions require a signed-in user.
* Application Permissions are used without user interaction.
* Administrator consent is required for many high-privilege permissions.
* Least privilege reduces security risks.

---

## References

| Microsoft Documentation                                                                                                                                    | Purpose                               |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------- |
| [Configure API permissions](https://learn.microsoft.com/entra/identity-platform/howto-add-app-roles-in-apps)                                               | API permissions overview              |
| [Microsoft identity platform permissions and consent](https://learn.microsoft.com/entra/identity-platform/permissions-consent-overview)                    | Delegated and Application permissions |
| [Microsoft Graph permissions reference](https://learn.microsoft.com/graph/permissions-reference)                                                           | Microsoft Graph permission catalog    |
| [Microsoft identity platform authentication and authorization basics](https://learn.microsoft.com/entra/identity-platform/authentication-vs-authorization) | Authentication vs Authorization       |
| [Microsoft Learn – Microsoft identity platform](https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/)                          | Microsoft Learn module                |

