# Application Object

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains the purpose of the Application Object and its role within the Microsoft Entra ID application model.

---

## Concept Overview

```text
        App Registration
              │
              ▼
     Application Object
              │
    Global Definition
              │
     ┌────────┴────────┐
     │                 │
     ▼                 ▼
Authentication     Configuration
     │                 │
     └────────┬────────┘
              ▼
     Service Principals
              │
              ▼
     Azure Resources / APIs
```

---

> [!TIP]
> **Key Concepts**
>
> - Every App Registration creates one Application Object.
> - The Application Object exists only in its home tenant.
> - It represents the global definition of the application.
> - Service Principals are created from the Application Object.
> - Configuration changes are stored in the Application Object.

---

## Overview

The Application Object is the global definition of an application registered in Microsoft Entra ID.

It contains the application's configuration, identity settings, authentication parameters, API permissions, branding, redirect URIs, credentials, and other metadata.

Every App Registration creates exactly one Application Object.

The Application Object exists only inside the application's home Microsoft Entra ID tenant.

---

## Purpose

The Application Object acts as the blueprint for the application.

Rather than representing a running instance of the application, it defines how the application should behave whenever Microsoft Entra ID authenticates it.

Whenever the application is used inside a tenant, Microsoft Entra ID relies on this definition to create a corresponding Service Principal.

---

## Home Tenant

An Application Object always belongs to a single Microsoft Entra ID tenant known as its Home Tenant.

```text
Home Tenant
      │
      ▼
Application Object
      │
Creates
      ▼
Service Principals
```

The Application Object never leaves its home tenant.

Even when a multi-tenant application is used by other organizations, the Application Object remains in its original tenant.

External tenants receive their own Service Principal instead.

---

## Information Stored

The Application Object stores the application's global configuration.

Examples include:

- Application (Client) ID
- Display Name
- Supported Account Types
- Redirect URIs
- Certificates
- Client Secrets
- Federated Credentials
- API Permissions
- App Roles
- Optional Claims
- Branding
- Manifest Configuration

This information defines how Microsoft Entra ID interacts with the application.

---

## Relationship with Service Principals

The Application Object and the Service Principal have different responsibilities.

| Application Object | Service Principal |
|--------------------|-------------------|
| Global definition | Local identity |
| Exists only in the Home Tenant | Exists in every tenant where the application operates |
| Stores configuration | Stores local assignments |
| Defines authentication settings | Receives permissions and policies |
| One per application | One per tenant |

Although closely related, they are separate Microsoft Entra ID objects.

---

## Multi-Tenant Applications

For multi-tenant applications, the Application Object remains unchanged inside the Home Tenant.

When another organization grants consent to the application, Microsoft Entra ID creates a new Service Principal inside that organization's tenant.

```text
Application Object
(Home Tenant)
        │
        ├────────► Tenant A Service Principal
        │
        ├────────► Tenant B Service Principal
        │
        └────────► Tenant C Service Principal
```

Each tenant manages its own Service Principal independently while sharing the same global application definition.

---

## Application Manifest

The Application Object is internally represented as a JSON document known as the **Application Manifest**.

The manifest stores the application's configuration in a structured format.

Many settings configured through the Microsoft Entra admin center are ultimately written to the manifest.

Infrastructure as Code tools, Microsoft Graph, and automation scripts interact with the same underlying object model.

---

## Common Identifiers

The Application Object contains multiple identifiers.

| Property | Description |
|----------|-------------|
| `appId` | Globally unique Application (Client) ID used during authentication. |
| `id` | Object ID of the Application Object inside the Home Tenant. |

Different Microsoft Graph operations may require either the **Application (Client) ID** or the **Object ID**, depending on the API being used.

Understanding this distinction helps avoid common automation mistakes.

---

## signInAudience

The supported account type selected during application registration is stored in the Application Object as the `signInAudience` property.

Common values include:

| Value | Description |
|-------|-------------|
| `AzureADMyOrg` | Single-Tenant application |
| `AzureADMultipleOrgs` | Multi-Tenant application |
| `AzureADandPersonalMicrosoftAccount` | Multi-Tenant including personal Microsoft accounts |
| `PersonalMicrosoftAccount` | Personal Microsoft accounts only |

This property is part of the Application Manifest and determines which identities are allowed to authenticate with the application.

---

## Application Capabilities

The Application Object defines the security capabilities that an application exposes.

Examples include:

| Capability | Purpose |
|------------|---------|
| `appRoles` | Defines application roles that can be assigned to users, groups, or applications. |
| `oauth2PermissionScopes` | Defines delegated permission scopes that client applications can request during OAuth 2.0 authorization. |

These capabilities are declared by the Application Object.

When the application is used inside a tenant, the corresponding Service Principal becomes the object that receives assignments and enforces access.

---

## Application Lifecycle

Application Objects support soft deletion.

When an Application Object is deleted, it enters a recoverable state for a limited retention period before being permanently removed.

If restored during the retention period, the Application Object and its configuration can be recovered.

Permanent deletion removes the application's global definition from Microsoft Entra ID.

---

## Enterprise Scenario

A software company develops a SaaS application.

The application is registered once inside the company's Microsoft Entra ID tenant.

The Application Object stores the application's global configuration.

As customers adopt the application, Microsoft Entra ID creates a separate Service Principal inside each customer's tenant while continuing to use the same Application Object as the master definition.

---

## Best Practices

- Register one Application Object per application.
- Follow the principle of least privilege.
- Prefer certificates or federated credentials over long-lived secrets.
- Review API permissions regularly.
- Remove unused Application Objects.
- Keep application ownership up to date.
- Document the purpose of every application.

---

## Common Pitfalls

- Confusing the Application Object with the Service Principal.
- Assuming the Application Object exists in every tenant.
- Using the wrong identifier (`appId` vs `id`) during automation.
- Granting excessive API permissions.
- Forgetting to review application credentials.
- Treating the Application Object as a user account.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Purpose of the Application Object
> - Home Tenant
> - Relationship with Service Principals
> - Application Manifest
> - Global application configuration
> - Common identifiers
> - Multi-tenant behavior

---

## Key Takeaways

- Every App Registration creates one Application Object.
- The Application Object is the global definition of an application.
- It exists only inside the Home Tenant.
- Service Principals are created from the Application Object.
- Configuration changes are stored in the Application Object.
- Multi-tenant applications share one Application Object but create multiple Service Principals.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Application and Service Principal Objects in Microsoft Entra ID](https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals) | Relationship between Application Objects and Service Principals |
| [Register an application with the Microsoft identity platform](https://learn.microsoft.com/entra/identity-platform/quickstart-register-app) | Application registration process |
| [Application Manifest](https://learn.microsoft.com/entra/identity-platform/reference-app-manifest) | JSON structure of the Application Object |
| [Microsoft Graph Application resource type](https://learn.microsoft.com/graph/api/resources/application) | Application Object properties (`id`, `appId`, manifest) |
| [Microsoft identity platform documentation](https://learn.microsoft.com/entra/identity-platform/) | Identity platform architecture |
| [Microsoft Learn – Build applications that authenticate users](https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/) | Microsoft Learn module |
