# Managed Identities Overview

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It introduces Managed Identities, explains how they work, and describes why they are the recommended authentication mechanism for Azure resources.

---

## Identity Model

```text
        Azure Resource
   (VM, App Service, Function)
               │
               ▼
      Managed Identity
               │
               ▼
     Microsoft Entra ID
               │
               ▼
     Access Token (OAuth 2.0)
               │
               ▼
     Azure Resource
(Key Vault, Storage, SQL, etc.)
```

---

> [!TIP]
> **Key Concepts**
>
> - Managed Identities provide identities for Azure resources.
> - Microsoft Entra ID manages the identity lifecycle.
> - No credentials are stored in application code.
> - Authentication uses OAuth 2.0 Access Tokens.
> - Azure RBAC controls resource authorization.

---

## Overview

A **Managed Identity** is a Microsoft Entra ID identity that is automatically managed by Azure and assigned to an Azure resource.

Managed Identities allow Azure services to authenticate securely to other Azure resources without storing passwords, client secrets, or certificates.

Instead of managing credentials manually, Azure obtains Access Tokens from Microsoft Entra ID whenever the resource needs to access another service.

---

## Why Managed Identities

Traditional application authentication often relies on credentials such as:

- Client Secrets
- Certificates
- Stored passwords

Managing these credentials introduces operational overhead and security risks.

Managed Identities eliminate these challenges by allowing Azure to manage the identity and authentication process automatically.

---

## How Managed Identities Work

When an Azure resource with a Managed Identity requests access to another Azure service:

1. The resource requests an Access Token.
2. Microsoft Entra ID authenticates the Managed Identity.
3. An OAuth 2.0 Access Token is issued.
4. The target resource validates the token.
5. Azure RBAC determines whether access is allowed.

No credentials are exchanged or stored by the application.

---

## Azure Instance Metadata Service (IMDS)

Azure resources obtain Access Tokens through the **Azure Instance Metadata Service (IMDS)**.

Instead of communicating directly with Microsoft Entra ID, the application sends an HTTP request to the local metadata endpoint:

```text
http://169.254.169.254/metadata/identity/oauth2/token
```

The request must include the HTTP header:

```text
Metadata: true
```

IMDS authenticates the Managed Identity with Microsoft Entra ID, retrieves the OAuth 2.0 Access Token, and returns it to the application.

This process allows applications to obtain tokens without storing credentials or communicating directly with Microsoft Entra ID.

---

## Authentication Flow

```text
Azure Resource
      │
      ▼
Managed Identity
      │
      ▼
Microsoft Entra ID
      │
      ▼
Access Token
      │
      ▼
Azure Resource
(Key Vault, Storage, SQL...)
```

---

## Identity Types

Microsoft Entra ID supports two types of Managed Identities.

| Type | Description |
|------|-------------|
| **System-Assigned** | Created automatically for a single Azure resource and deleted when the resource is removed. |
| **User-Assigned** | Created as an independent Azure resource and can be assigned to multiple Azure resources. |

Both identity types authenticate through Microsoft Entra ID and use Azure RBAC for authorization.

---

## Service Principal Lifecycle

When a Managed Identity is enabled, Microsoft Entra ID automatically creates a corresponding **Service Principal**.

This Service Principal appears in **Enterprise Applications** with the type **Managed Identity**.

For a **System-Assigned Managed Identity**, the Service Principal shares the lifecycle of the Azure resource:

- Created automatically when the Managed Identity is enabled.
- Deleted automatically when the Azure resource is deleted.

Deleting the resource also removes the associated Service Principal and its Azure RBAC role assignments.

A **User-Assigned Managed Identity** has its own independent lifecycle and remains available until explicitly deleted.

---

## Identity Assignment Limits

Managed Identity assignment depends on the identity type.

- An Azure resource can have **only one System-Assigned Managed Identity**.
- A resource can have **multiple User-Assigned Managed Identities**, subject to the limits of the Azure service.
- A resource can use both a **System-Assigned** and one or more **User-Assigned Managed Identities** simultaneously.

This flexibility allows applications to use dedicated identities for different workloads while maintaining a single resource.

---

## Common Azure Services

Managed Identities are commonly used with:

- Azure Virtual Machines
- Azure App Service
- Azure Functions
- Azure Kubernetes Service (AKS)
- Azure Logic Apps
- Azure Automation
- Azure Container Apps

These services can securely access:

- Azure Key Vault
- Azure Storage
- Azure SQL Database
- Azure Resource Manager
- Microsoft Graph
- Custom APIs

---

## Benefits

Managed Identities provide several advantages.

- No credential management.
- Automatic identity lifecycle.
- Reduced risk of credential exposure.
- Native integration with Azure RBAC.
- Simplified authentication.
- Improved security posture.

---

## Enterprise Scenario

An Azure App Service needs to retrieve secrets from Azure Key Vault.

Instead of storing a Client Secret inside the application configuration, the App Service uses a System-Assigned Managed Identity.

Microsoft Entra ID issues an Access Token, Azure RBAC verifies the assigned permissions, and Azure Key Vault returns the requested secret without exposing credentials.

---

## Best Practices

- Prefer Managed Identities over Client Secrets.
- Use Azure RBAC to grant only required permissions.
- Apply the principle of least privilege.
- Monitor identity usage through Microsoft Entra ID logs.
- Use User-Assigned Managed Identities only when multiple resources require the same identity.

---

## Common Pitfalls

- Confusing authentication with authorization.
- Granting excessive Azure RBAC permissions.
- Assuming Managed Identities work outside Azure.
- Forgetting to assign Azure RBAC roles.
- Using Client Secrets when Managed Identities are supported.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Managed Identities
> - System-Assigned Managed Identities
> - User-Assigned Managed Identities
> - OAuth 2.0 authentication
> - Azure RBAC integration
> - Credential-free authentication

---

## Key Takeaways

- Managed Identities provide Azure resources with identities managed by Microsoft Entra ID.
- Applications no longer need to store credentials.
- Authentication is performed using OAuth 2.0 Access Tokens.
- Azure RBAC controls authorization after authentication.
- Managed Identities are the recommended authentication method for Azure resources.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview | Managed Identities overview |
| https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/managed-identities-faq | Managed Identities FAQ |
| https://learn.microsoft.com/azure/role-based-access-control/overview | Azure RBAC overview |
| https://learn.microsoft.com/entra/identity-platform/v2-oauth2-client-creds-grant-flow | OAuth 2.0 Client Credentials flow |
| https://learn.microsoft.com/training/modules/managed-identities-azure-resources/ | Microsoft Learn – Managed Identities |
