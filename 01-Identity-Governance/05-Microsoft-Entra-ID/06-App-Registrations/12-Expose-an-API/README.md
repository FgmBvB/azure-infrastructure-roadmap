# Expose an API

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra ID allows applications to expose APIs that can be securely accessed by other applications using OAuth 2.0 permissions.

---

## API Exposure Flow

```text
        API Application
               │
               ▼
      App Registration
               │
               ▼
       Expose an API
               │
     Define Scopes & Roles
               │
               ▼
     Client Application
               │
     Requests Permission
               │
               ▼
      Microsoft Entra ID
               │
      Access Token Issued
               │
               ▼
        Protected API
```

---

> [!TIP]
> **Key Concepts**
>
> - Applications can expose their own APIs.
> - APIs define delegated permissions through Scopes.
> - APIs can define Application Permissions using App Roles.
> - Client applications request permissions before accessing the API.
> - Microsoft Entra ID issues Access Tokens containing the granted permissions.

---

## Overview

Applications can expose their own APIs through Microsoft Entra ID.

Instead of protecting only Microsoft services such as Microsoft Graph, organizations can register custom APIs and control who can access them.

Microsoft Entra ID manages authentication and permission issuance, while the API itself performs authorization.

---

## Why Expose an API

Many enterprise applications provide services that need to be consumed by other applications.

Examples include:

- Internal REST APIs
- Microservices
- Business applications
- Partner integrations
- SaaS platforms

Exposing an API allows organizations to use Microsoft Entra ID as a centralized identity provider.

---

## Application ID URI

Every exposed API requires an **Application ID URI**.

This URI uniquely identifies the API within Microsoft Entra ID.

Typical formats include:

- `api://<client-id>`
- `https://contoso.com/api`

The Application ID URI must be unique.

---

## Permission Types

An exposed API can define two authorization models.

| Permission | Purpose |
|------------|---------|
| Delegated Permissions (Scopes) | Used when a signed-in user is present. |
| Application Permissions (App Roles) | Used when applications authenticate without users. |

---

## Scopes

Scopes define the delegated permissions that client applications can request.

Examples include:

- `Employees.Read`
- `Employees.ReadWrite`
- `Orders.Read`

After administrator or user consent, these scopes appear inside the Access Token.

Applications evaluate these scopes before granting access.

---

## App Roles

Exposed APIs can also define **Application Permissions** using App Roles.

These permissions are intended for application-to-application communication where no interactive user exists.

App Roles are commonly used by:

- Background services
- Azure Functions
- Automation
- Daemon applications

Application Permissions typically require administrator consent.

---

## Client Applications

Before calling the API, a client application must request permission.

Administrators or users grant consent according to organizational policies.

After consent is granted, Microsoft Entra ID includes the approved permissions inside the Access Token.

---

## Authorization

Microsoft Entra ID authenticates identities and issues Access Tokens.

The API is responsible for evaluating the received token.

Typical authorization checks include:

- Token signature
- Token expiration
- Audience
- Scopes (`scp`)
- App Roles (`roles`)

Only authorized requests are processed.

---

## Enterprise Scenario

A company develops an internal Human Resources API.

The API exposes:

- `Employees.Read`
- `Employees.ReadWrite`

A web application requests the `Employees.Read` delegated permission.

After administrator consent, Microsoft Entra ID issues an Access Token containing the approved scope.

The API validates the token before returning employee information.

---

## Best Practices

- Use meaningful scope names.
- Apply least privilege.
- Define App Roles only when application permissions are required.
- Protect APIs using Access Tokens.
- Review exposed permissions regularly.

---

## Common Pitfalls

- Confusing Scopes with App Roles.
- Exposing unnecessary permissions.
- Forgetting administrator consent.
- Not validating Access Tokens.
- Using overly broad permissions.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Expose an API
> - Application ID URI
> - Scopes
> - App Roles
> - Delegated Permissions
> - Application Permissions
> - Access Tokens

---

## Key Takeaways

- Applications can expose custom APIs through Microsoft Entra ID.
- APIs define delegated permissions using Scopes.
- APIs define application permissions using App Roles.
- Client applications request permissions through Microsoft Entra ID.
- APIs authorize requests by validating Access Tokens.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Configure an application to expose a web API](https://learn.microsoft.com/entra/identity-platform/quickstart-configure-app-expose-web-apis) | Expose an API |
| [Microsoft identity platform permissions and consent overview](https://learn.microsoft.com/entra/identity-platform/permissions-consent-overview) | Permissions and consent |
| [Application Objects and Service Principals](https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals) | Identity model |
| [Access tokens](https://learn.microsoft.com/entra/identity-platform/access-tokens) | Access Tokens |
| [Microsoft Learn – Build applications that authenticate users](https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/) | Microsoft Learn module |
