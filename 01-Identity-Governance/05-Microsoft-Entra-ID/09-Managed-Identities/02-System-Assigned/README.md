# System-Assigned Managed Identity

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how System-Assigned Managed Identities work, their lifecycle, and their integration with Microsoft Entra ID and Azure RBAC.

---

## Architecture

```text
       Azure Resource
 (VM, App Service, Function)
               │
               ▼
 System-Assigned Managed Identity
               │
               ▼
     Microsoft Entra ID
               │
               ▼
      Service Principal
               │
               ▼
         Azure RBAC
               │
               ▼
      Azure Resources
```

---

> [!TIP]
> **Key Concepts**
>
> - A System-Assigned Managed Identity belongs to a single Azure resource.
> - Azure automatically creates and manages the identity.
> - The identity shares the lifecycle of the resource.
> - Authentication is performed through Microsoft Entra ID.
> - Authorization is controlled through Azure RBAC.

---

## Overview

A **System-Assigned Managed Identity** is an identity automatically created and managed by Azure for an individual Azure resource.

Unlike traditional service principals, administrators do not manage credentials manually.

Azure automatically provisions the identity in Microsoft Entra ID and removes it when the Azure resource is deleted.

---

## Lifecycle

A System-Assigned Managed Identity always shares the lifecycle of its Azure resource.

```text
Create Azure Resource
          │
          ▼
Managed Identity Created
          │
          ▼
Service Principal Created
          │
          ▼
Azure RBAC Assignments
          │
          ▼
Resource Deleted
          │
          ▼
Managed Identity Deleted
          │
          ▼
Service Principal Deleted
```

No manual cleanup is required.

---

## Identity Characteristics

| Property | System-Assigned |
|----------|-----------------|
| Azure managed | Yes |
| Credentials managed automatically | Yes |
| Shares resource lifecycle | Yes |
| Can be reused by multiple resources | No |
| Maximum per resource | One |

---

## Authentication

Applications authenticate without storing credentials.

The Azure resource requests an OAuth 2.0 Access Token through the Azure Instance Metadata Service (IMDS).

Microsoft Entra ID validates the identity and issues an Access Token for the requested Azure resource.

---

## Authorization

A Managed Identity has no permissions by default.

Administrators must assign Azure RBAC roles to the corresponding Service Principal.

Typical roles include:

- Key Vault Secrets User
- Storage Blob Data Reader
- Storage Blob Data Contributor
- Reader
- Contributor

Azure RBAC determines which Azure resources the identity can access.

---

## Common Use Cases

System-Assigned Managed Identities are commonly used when only one Azure resource requires the identity.

Typical scenarios include:

- Azure Virtual Machine accessing Azure Key Vault.
- Azure Function reading Azure Storage.
- Azure App Service connecting to Azure SQL Database.
- Azure Automation accessing Azure Resource Manager.

---

## Advantages

System-Assigned Managed Identities provide several benefits.

- No credential storage.
- Automatic lifecycle management.
- Native Microsoft Entra ID integration.
- Azure RBAC authorization.
- Reduced operational overhead.
- Improved security.

---

## Limitations

System-Assigned Managed Identities also have some limitations.

- Cannot be shared between Azure resources.
- Deleted automatically with the Azure resource.
- Cannot exist independently.
- Only one System-Assigned Managed Identity is supported per Azure resource.

---

## Enterprise Scenario

A company hosts an internal API in Azure App Service.

The application needs to retrieve secrets from Azure Key Vault.

Instead of storing a Client Secret, the App Service uses a System-Assigned Managed Identity.

The administrator grants the **Key Vault Secrets User** Azure RBAC role to the Managed Identity.

When the application requests a secret, Microsoft Entra ID issues an Access Token and Azure Key Vault authorizes the request without exposing credentials.

---

## Best Practices

- Prefer System-Assigned Managed Identities for single-resource workloads.
- Apply the principle of least privilege.
- Grant only required Azure RBAC roles.
- Monitor Managed Identity sign-ins.
- Remove unused role assignments.
- Use User-Assigned Managed Identities only when identity sharing is required.

---

## Common Pitfalls

- Assuming the identity has permissions automatically.
- Assigning excessive Azure RBAC roles.
- Confusing authentication with authorization.
- Expecting the identity to survive resource deletion.
- Using Client Secrets when a Managed Identity is supported.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - System-Assigned Managed Identities
> - Identity lifecycle
> - Microsoft Entra ID integration
> - Azure RBAC assignments
> - Authentication without credentials
> - Typical enterprise use cases

---

## Key Takeaways

- A System-Assigned Managed Identity belongs to one Azure resource.
- Azure manages the complete identity lifecycle.
- No credentials are stored by the application.
- Authentication is handled by Microsoft Entra ID.
- Azure RBAC determines what the identity can access.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Managed Identities overview](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview) | Managed Identities overview |
| [Managed Identities FAQ](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/managed-identities-faq) | Managed Identities concepts and lifecycle |
| [Managed Identities for Azure VMs](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/how-managed-identities-work-vm) | System-Assigned Managed Identity and IMDS |
| [Azure RBAC overview](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure RBAC overview |
| [Microsoft Learn – Managed Identities](https://learn.microsoft.com/training/modules/managed-identities-azure-resources/) | Microsoft Learn module |
