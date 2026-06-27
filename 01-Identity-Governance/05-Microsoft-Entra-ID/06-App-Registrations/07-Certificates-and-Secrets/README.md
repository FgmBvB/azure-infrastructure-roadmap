# Certificates and Secrets

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains the authentication credentials that applications use to prove their identity to Microsoft Entra ID.

---

## Authentication Credentials

```text
              Application
                    │
                    ▼
      Authentication Credential
                    │
      ┌─────────────┼─────────────┐
      │             │             │
      ▼             ▼             ▼
Client Secret  Certificate  Federated Credential
                    │
                    ▼
        Microsoft Entra ID
                    │
                    ▼
          Security Token Issued
```

---

> [!TIP]
> **Key Concepts**
>
> * Applications must authenticate before requesting tokens.
> * Microsoft Entra ID supports multiple authentication methods.
> * Certificates provide stronger security than Client Secrets.
> * Managed Identities eliminate credential management for Azure resources.
> * Workload Identity Federation enables passwordless authentication for external workloads.

---

## Overview

Applications must prove their identity before Microsoft Entra ID issues security tokens.

Unlike users, applications cannot authenticate interactively.

Instead, they authenticate using credentials configured in the App Registration.

Microsoft Entra ID supports several authentication methods designed for different security and operational requirements.

---

## Authentication Methods

| Method               | Description                                                                        |
| -------------------- | ---------------------------------------------------------------------------------- |
| Client Secret        | Shared secret known by the application and Microsoft Entra ID.                     |
| Certificate          | Public/private key pair used for cryptographic authentication.                     |
| Federated Credential | Trust relationship with an external identity provider using OpenID Connect (OIDC). |
| Managed Identity     | Azure-managed identity for Azure resources without stored credentials.             |

---

## Client Secrets

A Client Secret is a shared credential generated in the App Registration.

The application stores the secret securely and presents it when requesting an Access Token.

Client Secrets are simple to configure but require secure storage and periodic rotation.

Because they are shared secrets, they present a higher security risk than certificate-based authentication.

---

## Certificates

Certificates authenticate applications using asymmetric cryptography.

Administrators upload the public certificate to Microsoft Entra ID, while the application securely stores the corresponding private key.

During authentication, the application signs a request using its private key.

Microsoft Entra ID validates the signature using the stored public certificate before issuing an Access Token.

Certificates are generally recommended over Client Secrets for production environments.

---

## Managed Identities

Managed Identities provide passwordless authentication for Azure resources.

Azure automatically creates and manages the identity, eliminating the need to store Client Secrets or certificates.

Microsoft Entra ID supports two types of Managed Identities.

| Type            | Description                                                                              |
| --------------- | ---------------------------------------------------------------------------------------- |
| System-assigned | Bound to a single Azure resource and automatically deleted when the resource is removed. |
| User-assigned   | Independent Azure resource that can be associated with multiple Azure resources.         |

Managed Identities automatically rotate credentials and are Microsoft's recommended authentication method for Azure-hosted workloads.

---

## Federated Credentials

Federated Credentials enable applications running outside Azure to authenticate without storing secrets or certificates.

Instead of presenting a shared credential, Microsoft Entra ID trusts an external OpenID Connect (OIDC) identity provider.

Common scenarios include:

* GitHub Actions
* Kubernetes workloads
* GitLab CI/CD
* Other trusted OIDC providers

This authentication model is known as **Workload Identity Federation** and is Microsoft's recommended approach for modern DevOps environments.

---

## Credential Rotation

Authentication credentials should be rotated regularly.

Expired or compromised credentials can prevent applications from authenticating or expose sensitive resources.

Managed Identities eliminate this operational task because Azure automatically manages credential rotation.

---

## Enterprise Scenario

A company deploys an Azure Function that accesses Azure Key Vault.

Instead of storing a Client Secret, the Azure Function uses a System-assigned Managed Identity.

Microsoft Entra ID authenticates the Managed Identity, Azure Resource Manager authorizes the request through Azure RBAC, and Azure Key Vault grants access according to the assigned permissions.

---

## Best Practices

* Prefer Managed Identities for Azure resources.
* Use Certificates instead of Client Secrets whenever possible.
* Rotate Client Secrets regularly.
* Store private keys securely.
* Use Azure Key Vault to protect credentials.
* Prefer Workload Identity Federation for external workloads.
* Remove unused credentials.

---

## Common Pitfalls

* Hardcoding Client Secrets in application code.
* Using long-lived secrets.
* Forgetting to rotate credentials.
* Losing private certificate keys.
* Using Client Secrets when Managed Identities are available.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> * Client Secrets
> * Certificates
> * Managed Identities
> * Federated Credentials
> * Workload Identity Federation
> * Credential rotation
> * Security best practices

---

## Key Takeaways

* Applications authenticate using credentials instead of passwords.
* Client Secrets are simple but require secure management.
* Certificates provide stronger authentication through asymmetric cryptography.
* Managed Identities eliminate credential management for Azure resources.
* Federated Credentials enable passwordless authentication for external workloads.
* Microsoft recommends minimizing the use of long-lived secrets.

---

## References

| Microsoft Documentation                                                                                                                                                 | Purpose                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| [Certificates and secrets](https://learn.microsoft.com/entra/identity-platform/how-to-add-credentials)                                                                  | Configure client secrets and certificates |
| [Managed identities for Azure resources](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview)                                        | Managed Identity overview                 |
| [Workload identity federation](https://learn.microsoft.com/entra/workload-id/workload-identity-federation)                                                              | Federated Credentials and OIDC            |
| [Microsoft identity platform authentication](https://learn.microsoft.com/entra/identity-platform/)                                                                      | Microsoft identity platform               |
| [Microsoft Learn – Secure application authentication](https://learn.microsoft.com/training/modules/implement-authentication-by-using-microsoft-authentication-library/) | Microsoft Learn module                    |

