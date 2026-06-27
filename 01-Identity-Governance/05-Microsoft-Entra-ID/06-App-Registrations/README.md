# App Registrations

> [!NOTE]
> This section is part of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
>
> It covers how Microsoft Entra ID provides identities for applications, APIs, services, and automated workloads through App Registrations.

---

## Learning Path

```text
                  App Registrations
                         │
      ┌──────────────────┼──────────────────┐
      ▼                  ▼                  ▼
 Registration      Authentication     Authorization
      │                  │                  │
      ▼                  ▼                  ▼
 Certificates      Redirect URIs      Permissions
      │                  │                  │
      ▼                  ▼                  ▼
 Tokens          Single vs Multi      App Roles
      │                  │                  │
      └──────────────────┼──────────────────┘
                         ▼
                  Application Manifest
                         │
                         ▼
                  Best Practices
```

---

## Overview

Microsoft Entra ID allows applications to authenticate securely without embedding usernames and passwords.

Every application registered in Microsoft Entra ID receives an identity that can authenticate users, request security tokens, consume APIs, or expose its own APIs.

App Registrations are the foundation of modern authentication across Azure, Microsoft 365, and custom enterprise applications.

---

## Why App Registrations Matter

App Registrations enable:

- Modern authentication
- OAuth 2.0 and OpenID Connect
- Secure API access
- Microsoft Graph integration
- Azure automation
- Identity for applications
- Application-to-application authentication

Without App Registrations, applications would require embedded credentials, significantly increasing security risks.

---

## What You Will Learn

This section covers the complete lifecycle of an App Registration.

| Topic | Description |
|--------|-------------|
| Overview | What an App Registration is |
| Registration Process | Creating application identities |
| Application Object | Global application definition |
| Authentication | How applications authenticate |
| Authorization | API permissions and access control |
| Consent | User and administrator approval |
| Certificates and Secrets | Authentication credentials |
| Redirect URIs | Secure authentication callbacks |
| Tokens | ID, Access and Refresh Tokens |
| Single vs Multi-Tenant | Tenant scope |
| App Roles | Application authorization |
| Expose an API | Publishing custom APIs |
| Manifest | JSON configuration |
| Best Practices | Security and governance |

---

## Key Concepts

Throughout this section you will encounter several core Microsoft Entra ID concepts.

| Concept | Purpose |
|----------|---------|
| Application Object | Global definition of an application |
| Service Principal | Local identity inside a tenant |
| Access Token | Grants access to protected resources |
| App Roles | Application authorization |
| Scopes | Delegated permissions |
| Redirect URI | Authentication response endpoint |
| Manifest | JSON configuration |
| Client Secret / Certificate | Application credentials |

---

## Learning Objectives

After completing this section you should understand how to:

- Register applications.
- Configure authentication.
- Configure authorization.
- Manage application credentials.
- Secure application identities.
- Expose APIs.
- Consume Microsoft Graph.
- Understand the Application Object and Service Principal relationship.
- Apply Microsoft security best practices.

---

## Related Sections

This module connects with:

- Microsoft Entra ID
- Enterprise Applications
- Managed Identities
- Azure RBAC
- Microsoft Graph
- Conditional Access
- Identity Governance

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Microsoft identity platform documentation](https://learn.microsoft.com/entra/identity-platform/) | Microsoft identity platform overview |
| [Register an application](https://learn.microsoft.com/entra/identity-platform/quickstart-register-app) | Create an App Registration |
| [Application Objects and Service Principals](https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals) | Identity model |
| [Permissions and consent overview](https://learn.microsoft.com/entra/identity-platform/permissions-consent-overview) | Permissions and consent |
| [Microsoft Learn – Build applications that authenticate users](https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/) | Microsoft Learn module |
