# App Registrations Overview

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It introduces Microsoft Entra ID App Registrations and explains their purpose within modern identity and application authentication.

---

## Concept Overview

```text
                Application
                     │
                     ▼
          App Registration
                     │
                     ▼
          Application Object
                     │
                     ▼
        Microsoft Entra ID
                     │
             Creates
                     ▼
          Service Principal
                     │
                     ▼
          Security Tokens
                     │
                     ▼
      Azure Resources / APIs
```

---

> [!TIP]
> **Key Concepts**
>
> - An App Registration represents an application in Microsoft Entra ID.
> - Every App Registration creates an Application Object.
> - Microsoft Entra ID creates a Service Principal to represent the application inside a tenant.
> - Applications authenticate using Microsoft Entra ID.
> - App Registrations enable secure access to Azure resources and APIs.
> - App Registrations are the foundation of modern authentication.

---

## Overview

An App Registration represents an application that needs to authenticate with Microsoft Entra ID.

Rather than authenticating only users, Microsoft Entra ID can also authenticate applications, APIs, web services, background jobs, mobile applications, desktop software, automation scripts, and many other workloads.

An App Registration establishes a trust relationship between an application and Microsoft Entra ID.

Once registered, the application can securely request security tokens that are later used to access Azure resources, Microsoft services, or third-party APIs.

---

## Why App Registrations Exist

Modern applications frequently need to access protected resources such as:

- Microsoft Graph
- Azure Resource Manager
- Azure Key Vault
- Azure Storage
- Azure SQL
- Custom APIs
- Third-party APIs

Embedding usernames and passwords directly into application code is insecure and difficult to manage.

Instead, Microsoft Entra ID provides a dedicated identity for the application.

Applications authenticate using this identity and receive short-lived security tokens instead of storing permanent credentials.

This architecture significantly improves security while supporting modern authentication standards such as OAuth 2.0 and OpenID Connect.

---

## Application Identity

When an application is registered, Microsoft Entra ID creates an **Application Object** inside the tenant.

The Application Object represents the global definition of the application and stores its configuration throughout its lifecycle.

Important identifiers include:

| Property | Description |
|----------|-------------|
| Application (Client) ID | Globally unique identifier of the application. |
| Object ID | Unique identifier of the Application Object inside the home tenant. |
| Directory (Tenant) ID | Identifies the Microsoft Entra ID tenant where the application is registered. |

These identifiers are commonly required when configuring authentication, APIs, automation, infrastructure as code, or Microsoft Graph integrations.

The Application Object exists only in its **home tenant** and represents the application's global definition.

---

## Supported Account Types

During registration, administrators choose which identities are allowed to authenticate with the application.

| Account Type | Description |
|--------------|-------------|
| Single-Tenant | Only identities from the application's home Microsoft Entra ID tenant can authenticate. |
| Multi-Tenant | Identities from other Microsoft Entra ID tenants can authenticate after the required consent process. |

For multi-tenant applications, Microsoft Entra ID automatically creates a Service Principal inside external tenants after administrator or user consent is granted.

The differences between Single-Tenant and Multi-Tenant applications are covered later in this roadmap.

---

## Common Application Types

Many different workloads use App Registrations.

| Application Type | Example |
|------------------|---------|
| Web Application | Internal HR Portal |
| Web API | REST API |
| Mobile Application | Android or iOS application |
| Desktop Application | Windows client |
| Background Service | Scheduled automation |
| Daemon Application | Unattended service |
| CLI Tool | Internal administration utility |

All of these application types can authenticate through Microsoft Entra ID.

---

## Authentication Model

Applications authenticate differently from users.

Instead of interactive usernames and passwords, applications typically authenticate using one of the following mechanisms:

- Client Secrets
- Certificates
- Managed Identities (Azure resources)
- Federated Credentials

After successful authentication, Microsoft Entra ID issues security tokens that applications use to access protected resources securely.

Depending on the scenario, applications may authenticate on behalf of a signed-in user or independently without any user interaction.

Authentication mechanisms, permission models, and security tokens are explored in the following sections of this roadmap.

---

## API Permission Models

Applications request permissions depending on how they access protected resources.

Microsoft Entra ID supports two primary permission models.

| Permission Type | Description |
|-----------------|-------------|
| Delegated Permissions | The application acts on behalf of a signed-in user. The effective permissions depend on both the application's granted permissions and the user's own permissions. |
| Application Permissions | The application runs without user interaction, such as automation scripts or daemon services. These permissions require administrator consent because they grant direct access to resources. |

API permissions and consent are explored in dedicated sections later in this roadmap.

---

## Relationship with Other Components

An App Registration is only one part of the Microsoft Entra ID application identity model.

```text
                Application
                     │
                     ▼
          App Registration
                     │
                     ▼
          Application Object
                     │
        ┌────────────┴────────────┐
        │                         │
        ▼                         ▼
 Service Principal         Authentication
        │                         │
        └────────────┬────────────┘
                     ▼
            Security Tokens
                     │
                     ▼
        Azure Resources / APIs
```

These components work together to provide secure authentication and authorization across Microsoft cloud services.

Each component is explored in detail throughout this roadmap.

---

## Application Object and Service Principal

When an application is registered, Microsoft Entra ID creates an **Application Object** inside the application's home tenant.

The Application Object contains the global definition of the application, including authentication settings, redirect URIs, API permissions, credentials, branding, and other configuration.

Whenever the application needs to operate inside a Microsoft Entra ID tenant, Microsoft Entra ID creates a **Service Principal**.

The Service Principal represents the application's local identity inside that tenant.

Azure RBAC assignments, Conditional Access policies, API permissions, and administrative controls are applied to the Service Principal rather than to the Application Object.

```text
Application Object
(Home Tenant)
        │
Creates
        ▼
Service Principal
(Local Identity)
        │
Authenticates
        ▼
Azure Resources
```

This separation allows one Application Object to be used across multiple Microsoft Entra ID tenants while each tenant maintains its own independent Service Principal.

---

---

## Enterprise Scenario

A development team creates a web application that needs to read user information from Microsoft Graph.

Instead of embedding administrator credentials inside the application, the developers register the application in Microsoft Entra ID.

The application authenticates using its own identity, requests the appropriate API permissions, receives security tokens from Microsoft Entra ID, and securely accesses Microsoft Graph according to the permissions granted by administrators.

If the application is later deployed to multiple organizations, Microsoft Entra ID creates a Service Principal inside each customer tenant after the required consent process, allowing the same application definition to operate securely across multiple tenants.

---

## Best Practices

- Register each application separately.
- Follow the principle of least privilege.
- Request only the API permissions required by the application.
- Prefer certificates over client secrets whenever possible.
- Prefer Managed Identities for Azure-hosted workloads.
- Rotate secrets and certificates regularly.
- Store credentials securely using Azure Key Vault.
- Remove unused App Registrations to reduce the attack surface.
- Periodically review granted API permissions and administrator consent.

---

## Common Pitfalls

- Confusing App Registrations with Enterprise Applications.
- Confusing the Application Object with the Service Principal.
- Embedding credentials directly into application code.
- Granting excessive API permissions.
- Forgetting to rotate client secrets or certificates.
- Registering multiple unrelated applications under a single App Registration.
- Using long-lived credentials when more secure authentication methods are available.
- Assuming an App Registration automatically has access to Azure resources without explicit permissions.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Purpose of App Registrations
> - Application Object
> - Service Principal
> - Client ID
> - Object ID
> - Tenant ID
> - Supported Account Types
> - Authentication methods
> - API Permission models
> - Relationship with Enterprise Applications
> - Modern application authentication

---

## Key Takeaways

- App Registrations provide identities for applications.
- Every App Registration creates an Application Object.
- Microsoft Entra ID creates a Service Principal for each tenant where the application operates.
- Applications authenticate using Microsoft Entra ID instead of embedded credentials.
- Security tokens are issued after successful authentication.
- API permissions determine which resources an application can access.
- App Registrations are the foundation of modern authentication in Microsoft Entra ID.

---

## Related Topics

This overview introduces the Microsoft Entra ID application model.

The following sections explore each component in detail:

- Application Registration Process
- Application Object
- Authentication
- API Permissions
- Consent
- Certificates and Secrets
- Redirect URIs
- Tokens
- Single-Tenant vs. Multi-Tenant Applications
- App Roles
- Expose an API
- Manifest
- Best Practices

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Register an application](https://learn.microsoft.com/entra/identity-platform/quickstart-register-app) | Creating an App Registration |
| [Application Objects and Service Principals](https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals) | Microsoft Entra ID application model |
| [Authentication and authorization basics](https://learn.microsoft.com/entra/identity-platform/authentication-vs-authorization) | Identity fundamentals |
| [Microsoft identity platform](https://learn.microsoft.com/entra/identity-platform/) | Identity platform overview |
| [OAuth 2.0 and OpenID Connect](https://learn.microsoft.com/entra/identity-platform/v2-protocols) | Authentication protocols |
| [Microsoft Graph permissions reference](https://learn.microsoft.com/graph/permissions-reference) | Microsoft Graph API permissions |
| [Microsoft Learn – Build applications that authenticate users](https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/) | Microsoft Learn module |
