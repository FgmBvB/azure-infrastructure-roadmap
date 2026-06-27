# Application Authentication

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how applications authenticate with Microsoft Entra ID to obtain security tokens and securely access protected resources.

---

## Authentication Flow

```text
      Application
            │
            ▼
Authentication Request
            │
            ▼
Microsoft Entra ID
            │
Authenticate Application
            │
            ▼
Issue Security Token
            │
            ▼
Protected Resource
(Azure / Microsoft Graph / API)
```

---

> [!TIP]
> **Key Concepts**
>
> - Applications authenticate differently from users.
> - Authentication establishes the application's identity.
> - Microsoft Entra ID issues security tokens after successful authentication.
> - Applications can authenticate using multiple credential types.
> - Authentication occurs before authorization.

---

## Overview

Applications frequently need to access Azure resources, Microsoft Graph, or custom APIs without embedding usernames and passwords.

Microsoft Entra ID provides secure authentication mechanisms that allow applications to prove their identity and obtain security tokens.

After successful authentication, the application can request access to protected resources according to the permissions granted by administrators.

Authentication identifies the application.

Authorization determines what the application is allowed to access.

---

## Authentication Process

The application authentication process generally follows these steps:

1. The application sends an authentication request to Microsoft Entra ID.
2. Microsoft Entra ID validates the application's identity.
3. The configured authentication credential is verified.
4. Microsoft Entra ID issues a security token.
5. The application presents the token to the target resource.
6. The resource validates the token before processing the request.

Authentication alone does not grant permissions.

Authorization occurs separately when the resource evaluates the application's permissions.

---

## Authentication Methods

Microsoft Entra ID supports multiple authentication methods for applications.

| Method | Typical Scenario |
|---------|------------------|
| Client Secret | Development or smaller applications |
| Certificate | Production workloads |
| Managed Identity | Azure-hosted resources |
| Federated Credential | External workloads (GitHub Actions, Kubernetes, CI/CD) |

Each method provides a different balance between security, administration, and operational complexity.

---

## Client Secrets

Client Secrets are shared secrets generated during application registration.

The application presents the secret together with its Client ID when requesting authentication.

Although simple to configure, Client Secrets require secure storage and regular rotation.

Microsoft recommends avoiding long-lived secrets whenever possible.

---

## Certificates

Certificates provide stronger authentication than Client Secrets.

Instead of a shared secret, Microsoft Entra ID validates the application's certificate.

Certificates reduce the risk associated with credential leakage and are recommended for production environments.

Certificate lifecycle management remains the responsibility of administrators.

---

## Managed Identities

Managed Identities provide passwordless authentication for Azure resources.

Azure automatically creates and manages the application's identity.

No Client Secret or certificate needs to be stored inside the application.

Azure also manages credential rotation automatically.

Managed Identities are available only for supported Azure resources.

---

## Federated Credentials

Federated Credentials enable applications running outside Azure to authenticate without storing long-lived credentials.

Instead of using Client Secrets or certificates, Microsoft Entra ID trusts an external identity provider that issues OpenID Connect (OIDC) tokens.

Common scenarios include:

- GitHub Actions
- Kubernetes workloads
- External CI/CD platforms

This approach significantly reduces credential management and improves security.

---

## Security Tokens

After successful authentication, Microsoft Entra ID issues security tokens.

Depending on the authentication flow, applications may receive:

| Token | Purpose |
|--------|---------|
| Access Token | Access protected APIs and Azure resources |
| ID Token | Identify the authenticated identity in OpenID Connect scenarios |
| Refresh Token | Request new Access Tokens without requiring another authentication |

Applications use these tokens instead of repeatedly sending credentials.

---

## Enterprise Scenario

A GitHub Actions pipeline deploys Azure infrastructure.

Instead of storing a Client Secret inside GitHub, the pipeline authenticates using Workload Identity Federation.

Microsoft Entra ID validates the external identity, issues an Access Token, and Azure Resource Manager authorizes the deployment according to the assigned permissions.

---

## Best Practices

- Prefer Managed Identities for Azure resources.
- Use Federated Credentials for external workloads.
- Prefer certificates over Client Secrets.
- Rotate credentials regularly.
- Store secrets securely using Azure Key Vault.
- Monitor application sign-in logs.
- Apply the principle of least privilege.

---

## Common Pitfalls

- Embedding secrets directly in source code.
- Using long-lived Client Secrets.
- Forgetting to rotate certificates.
- Confusing authentication with authorization.
- Granting unnecessary API permissions.
- Assuming authentication automatically grants access.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Application authentication
> - Authentication methods
> - Client Secrets
> - Certificates
> - Managed Identities
> - Federated Credentials
> - Security Tokens
> - Authentication versus authorization

---

## Key Takeaways

- Applications authenticate using Microsoft Entra ID.
- Authentication establishes application identity.
- Microsoft Entra ID issues security tokens after successful authentication.
- Managed Identities eliminate credential management for Azure resources.
- Federated Credentials enable passwordless authentication for external workloads.
- Authentication always occurs before authorization.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Application authentication with the Microsoft identity platform](https://learn.microsoft.com/entra/identity-platform/authentication-flows-app-scenarios) | Authentication flows for applications |
| [Microsoft identity platform authentication libraries](https://learn.microsoft.com/entra/identity-platform/msal-overview) | Microsoft Authentication Library (MSAL) |
| [Certificates and secrets](https://learn.microsoft.com/entra/identity-platform/how-to-add-credentials) | Configure Client Secrets and Certificates |
| [Managed identities for Azure resources](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview) | Managed Identity overview |
| [Workload identity federation](https://learn.microsoft.com/entra/workload-id/workload-identity-federation) | Passwordless authentication for external workloads |
| [Access tokens](https://learn.microsoft.com/entra/identity-platform/access-tokens) | Microsoft Entra ID security tokens |
| [Microsoft Learn – Build applications that authenticate users](https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/) | Microsoft Learn module |
