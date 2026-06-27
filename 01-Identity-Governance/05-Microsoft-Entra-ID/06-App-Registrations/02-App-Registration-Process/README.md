# App Registration Process

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains what happens when an application is registered in Microsoft Entra ID and how the registration process creates the application's identity.

---

## Registration Process

```text
Developer / Administrator
            │
            ▼
   Create App Registration
            │
            ▼
  Microsoft Entra ID
            │
            ▼
Creates Application Object
            │
            ▼
Generates Application (Client) ID
            │
            ▼
Stores Application Configuration
            │
            ▼
Application Ready for Authentication
```

---

> [!TIP]
> **Key Concepts**
>
> - Registering an application creates its identity in Microsoft Entra ID.
> - Every registration creates one Application Object.
> - Microsoft Entra ID generates unique identifiers automatically.
> - Additional configuration is typically required before the application can authenticate.
> - The registration process does not automatically grant permissions.

---

## Overview

An App Registration is the first step in enabling an application to use Microsoft Entra ID for authentication.

During registration, Microsoft Entra ID creates the application's identity and stores its configuration inside the tenant.

At this stage, the application exists as an identity object but has not yet been granted permissions to access protected resources.

---

## Registration Workflow

The registration process typically consists of the following steps.

1. An administrator or developer creates a new App Registration.
2. Microsoft Entra ID creates an Application Object.
3. Microsoft Entra ID generates a unique Application (Client) ID.
4. The application is associated with its home tenant.
5. Initial authentication settings are stored.
6. The application becomes available for further configuration.

Additional configuration such as certificates, secrets, API permissions, redirect URIs, or authentication methods can be added afterwards.

---

## Information Collected During Registration

When creating an App Registration, administrators provide several configuration options.

| Setting | Purpose |
|---------|---------|
| Name | Friendly application name |
| Supported Account Types | Defines which identities may authenticate |
| Redirect URI (optional) | Used by interactive authentication flows |
| Platform (optional) | Web, SPA, Mobile, Desktop or other supported application type |

Most settings can be modified later after the registration has been created.

---

## Objects Created

Registering an application immediately creates an Application Object.

```text
App Registration
        │
        ▼
Application Object
        │
        ▼
Global Definition
```

The Application Object becomes the application's permanent definition inside its home tenant.

Additional Service Principals are created later when the application is used inside one or more tenants.

---

## Home Tenant

Every App Registration belongs to a single Microsoft Entra ID tenant known as its **Home Tenant**.

The Home Tenant owns the Application Object and stores the application's configuration.

For multi-tenant applications, external organizations do not receive a copy of the Application Object.

Instead, Microsoft Entra ID creates a Service Principal inside each external tenant after the required consent process.

---

## What Is Not Created Yet

Registering an application does **not** automatically create everything required for production use.

Immediately after registration:

- No client secret exists.
- No certificate exists.
- No API permissions have been granted.
- No administrator consent has been provided.
- No Azure RBAC permissions exist.
- No Conditional Access policies are applied.

These configurations are performed separately according to the application's requirements.

---

## Supported Account Types

The Supported Account Types setting defines who can sign in to the application.

| Supported Account Type | Description |
|------------------------|-------------|
| Single-Tenant | Only accounts from the application's home Microsoft Entra ID tenant can sign in. |
| Multi-Tenant | Accounts from any Microsoft Entra ID tenant can sign in after consent is granted. |
| Multi-Tenant and Personal Microsoft Accounts | Organizational accounts from any Microsoft Entra ID tenant and personal Microsoft accounts can sign in. |
| Personal Microsoft Accounts Only | Only personal Microsoft accounts such as Outlook.com or Xbox accounts can sign in. |

This decision affects the application's identity boundary, consent model, and Service Principal creation behavior.

For enterprise applications, the account type should be selected carefully during registration because changing it later may require additional configuration and review.

---

## Tenant App Registration Policy

Microsoft Entra ID tenants can control who is allowed to register applications.

In many tenants, users may be allowed to register applications by default.

In enterprise environments, this setting is often restricted to reduce Shadow IT and improve governance.

When app registration is restricted, only authorized roles such as **Application Administrator**, **Cloud Application Administrator**, or other privileged identities can create App Registrations.

This helps organizations control which applications are trusted by the tenant.

---

## Application Manifest

The Application Manifest is the JSON representation of an App Registration.

Many settings configured through the Microsoft Entra admin center are stored in the manifest.

The manifest can be used to review or modify advanced application configuration that may not be visible directly in the portal.

Automation tools such as Microsoft Graph, Terraform, and Infrastructure as Code workflows interact with the same underlying application configuration model.

The manifest is covered in detail later in this roadmap.

---

### Common Identifiers in the Manifest

The Application Manifest contains multiple identifiers for the application.

| Property | Description |
|----------|-------------|
| `appId` | The globally unique **Application (Client) ID** used by applications during authentication. |
| `id` | The unique **Object ID** of the Application Object within its home Microsoft Entra ID tenant. |

When using Microsoft Graph, PowerShell, or Infrastructure as Code tools, different operations may require either the **Application (Client) ID** (`appId`) or the **Object ID** (`id`), depending on the API or resource being managed.

Understanding the distinction between these identifiers helps avoid common automation and scripting errors.

---

## Enterprise Scenario

A software development team creates a new internal web application.

The first step is registering the application in Microsoft Entra ID.

After registration, the developers configure redirect URIs, create a certificate, request Microsoft Graph permissions, and authenticate users using Microsoft Entra ID.

The registration itself only establishes the application's identity.

---

## Best Practices

- Register each application independently.
- Use meaningful application names.
- Choose the correct Supported Account Type.
- Review application ownership regularly.
- Remove unused App Registrations.
- Document the purpose of each registration.

---

## Common Pitfalls

- Assuming registration automatically grants permissions.
- Forgetting to configure authentication settings.
- Using overly broad Supported Account Types.
- Creating duplicate App Registrations.
- Confusing App Registration with Enterprise Application.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Registration process
> - Application Object creation
> - Home Tenant
> - Supported Account Types
> - Application identifiers
> - Initial application configuration

---

## Key Takeaways

- Registering an application creates its identity.
- Every registration creates one Application Object.
- Microsoft Entra ID generates a unique Client ID automatically.
- Registration alone does not grant permissions.
- Additional configuration is required before production use.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Register an application with the Microsoft identity platform](https://learn.microsoft.com/entra/identity-platform/quickstart-register-app) | Create and configure App Registrations |
| [Application and Service Principal Objects in Microsoft Entra ID](https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals) | Relationship between Application Objects and Service Principals |
| [Supported account types](https://learn.microsoft.com/entra/identity-platform/supported-accounts-validation) | Supported Account Types and tenant audience |
| [Application Manifest](https://learn.microsoft.com/entra/identity-platform/reference-app-manifest) | JSON configuration of an App Registration |
| [Restrict who can create applications](https://learn.microsoft.com/entra/identity/role-based-access-control/delegate-app-roles#restrict-who-can-create-applications) | Tenant App Registration Policy and governance |
| [Microsoft Graph Application resource type](https://learn.microsoft.com/graph/api/resources/application) | Application properties, including `id` and `appId` |
| [Microsoft Learn – Build applications that authenticate users](https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/) | Microsoft Learn module covering App Registration fundamentals |
