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
             ▼
 Issues Security Tokens
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
> - Applications authenticate using Microsoft Entra ID.
> - App Registrations enable secure access to Azure resources and APIs.
> - App Registrations are the foundation of modern authentication.

---

## Overview

An App Registration represents an application that needs to authenticate with Microsoft Entra ID.

Rather than authenticating users only, Microsoft Entra ID can also authenticate applications, web services, APIs, background processes, mobile apps, and other workloads.

An App Registration establishes a trust relationship between an application and Microsoft Entra ID.

Once registered, the application can request security tokens that allow it to securely authenticate and access protected resources.

---

## Why App Registrations Exist

Applications frequently need to access protected resources such as:

- Microsoft Graph
- Azure Resource Manager
- Azure Key Vault
- Azure Storage
- Custom APIs
- Third-party APIs

Instead of storing usernames and passwords inside application code, Microsoft Entra ID provides a secure identity for the application.

Applications authenticate using this identity and receive security tokens instead of relying on embedded credentials.

This significantly improves security and supports modern authentication standards.

---

## Application Identity

When an application is registered, Microsoft Entra ID creates an **Application Object** inside the tenant.

This object defines the application's identity and configuration.

Important identifiers include:

| Property | Description |
|----------|-------------|
| Application (Client) ID | Globally unique identifier of the application. |
| Object ID | Unique identifier of the Application Object within the tenant. |
| Directory (Tenant) ID | Identifies the Microsoft Entra ID tenant where the application is registered. |

These identifiers are frequently required when configuring authentication, APIs, or automation.
The Application Object exists only in its home tenant and serves as the global definition of the application throughout its lifecycle.

---

## Common Application Types

Many different workloads can use App Registrations.

| Application Type | Example |
|------------------|---------|
| Web Application | Internal HR portal |
| Web API | REST API |
| Mobile Application | Android or iOS app |
| Desktop Application | Windows client |
| Background Service | Scheduled automation |
| Daemon Application | Unattended service |
| CLI Tool | Internal administration utility |

All of these applications can authenticate through Microsoft Entra ID.

---

## Authentication Model

Applications do not authenticate in the same way as users.

Instead of entering passwords interactively, applications typically authenticate using:

- Client Secrets
- Certificates
- Managed Identities (Azure resources)
- Federated Credentials

After successful authentication, Microsoft Entra ID issues security tokens that the application uses to access protected resources. Depending on the scenario, applications may authenticate on behalf of a signed-in user or independently without user interaction.

These authentication models are explored later in this roadmap.

The authentication mechanisms themselves are covered in later sections of this roadmap.

---

## Relationship with Other Components

An App Registration is only one part of the Microsoft Entra ID application model.

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

The following documents explain each component in detail.

---

## Application Object and Service Principal

When an application is registered, Microsoft Entra ID creates an **Application Object** in the home tenant.

The Application Object represents the global definition of the application, including its authentication settings, permissions, redirect URIs, and credentials.

When the application needs to operate within a tenant, Microsoft Entra ID creates a **Service Principal**.

The Service Principal represents the local identity of the application and is the object that receives permissions, Azure RBAC assignments, and Conditional Access policies.

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

This separation allows the same application to exist in multiple Microsoft Entra ID tenants while maintaining a single application definition.

---

## Enterprise Scenario

A development team creates a web application that needs to read information from Microsoft Graph.

Instead of embedding administrator credentials inside the application, the developers register the application in Microsoft Entra ID.

The application authenticates using its own identity, receives security tokens from Microsoft Entra ID, and securely accesses Microsoft Graph according to the permissions granted by administrators.

---

## Best Practices

- Register each application separately.
- Follow the principle of least privilege.
- Prefer certificates over client secrets when possible.
- Rotate credentials regularly.
- Store secrets securely using Azure Key Vault.
- Review unused App Registrations periodically.

---

## Common Pitfalls

- Confusing App Registrations with Enterprise Applications.
- Embedding credentials directly into application code.
- Granting excessive API permissions.
- Forgetting to rotate client secrets.
- Registering multiple unrelated applications under a single App Registration.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Purpose of App Registrations
> - Application Object
> - Client ID
> - Object ID
> - Tenant ID
> - Relationship with Service Principals
> - Relationship with Enterprise Applications
> - Modern application authentication

---

## Key Takeaways

- App Registrations provide identities for applications.
- Every App Registration creates an Application Object.
- Microsoft Entra ID authenticates applications as well as users.
- Applications receive security tokens instead of using embedded credentials.
- App Registrations are the foundation of modern authentication in Azure.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| https://learn.microsoft.com/entra/identity-platform/quickstart-register-app | Register an application |
| https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals | Application Objects and Service Principals |
| https://learn.microsoft.com/entra/identity-platform/v2-protocols | OAuth 2.0 and OpenID Connect |
| https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/ | Microsoft Learn – App Registration fundamentals |
