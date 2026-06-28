# User-Assigned Managed Identity

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how User-Assigned Managed Identities work, their lifecycle, and when they should be used in Azure environments.

---

## Architecture

```text
             Microsoft Entra ID
                     │
                     ▼
     User-Assigned Managed Identity
                     │
        ┌────────────┼────────────┐
        │            │            │
        ▼            ▼            ▼
 Azure VM      App Service    Azure Function
        │            │            │
        └────────────┼────────────┘
                     ▼
               Azure Resources
        (Key Vault, Storage, SQL)
```

---

> [!TIP]
> **Key Concepts**
>
> - A User-Assigned Managed Identity is an independent Azure resource.
> - It can be assigned to multiple Azure resources.
> - Its lifecycle is independent of the resources using it.
> - Authentication is managed by Microsoft Entra ID.
> - Azure RBAC controls resource authorization.

---

## Overview

A **User-Assigned Managed Identity** is a standalone identity created as an Azure resource.

Unlike a System-Assigned Managed Identity, it is not tied to the lifecycle of a single Azure resource.

The same identity can be assigned to multiple Azure resources that require identical permissions.

---

## Lifecycle

User-Assigned Managed Identities exist independently of the resources that use them.

```text
Create Managed Identity
          │
          ▼
Service Principal Created
          │
          ▼
Assign to Azure Resources
          │
          ▼
Azure RBAC Assignments
          │
          ▼
Azure Resources Deleted
          │
          ▼
Managed Identity Remains
          │
          ▼
Delete Managed Identity
          │
          ▼
Service Principal Deleted
```

Deleting an Azure resource does not delete the User-Assigned Managed Identity.

---

## Identity Characteristics

| Property | User-Assigned |
|----------|---------------|
| Azure managed | Yes |
| Credentials managed automatically | Yes |
| Independent lifecycle | Yes |
| Can be shared by multiple resources | Yes |
| Exists as an Azure resource | Yes |

---

## Authentication

Azure resources authenticate using the assigned User-Assigned Managed Identity.

The application requests an OAuth 2.0 Access Token through the Azure Instance Metadata Service (IMDS).

Microsoft Entra ID validates the identity and issues an Access Token for the requested Azure service.

When multiple User-Assigned Managed Identities are attached to the same Azure resource, the application must specify which identity should be used when requesting the token.

---

## Authorization

User-Assigned Managed Identities have no permissions by default.

Administrators grant access by assigning Azure RBAC roles to the Managed Identity.

Common examples include:

- Key Vault Secrets User
- Storage Blob Data Reader
- Storage Blob Data Contributor
- Reader
- Contributor

Authorization is always evaluated through Azure RBAC.

---

## Common Use Cases

User-Assigned Managed Identities are ideal when multiple Azure resources require the same permissions.

Typical scenarios include:

- Multiple Azure Virtual Machines accessing the same Key Vault.
- Azure Functions sharing access to Azure Storage.
- Several App Services connecting to the same Azure SQL Database.
- Shared identities for microservices.

---

## Advantages

User-Assigned Managed Identities provide several benefits.

- Reusable across multiple Azure resources.
- Independent lifecycle.
- Simplified permission management.
- Reduced credential management.
- Native Microsoft Entra ID integration.

---

## Limitations

User-Assigned Managed Identities also have some limitations.

- Must be created separately before use.
- Azure RBAC assignments require manual configuration.
- Unused identities should be removed to reduce administrative overhead.
- Applications must explicitly select the identity when multiple User-Assigned identities are attached.

---

## Enterprise Scenario

A company deploys several Azure App Services that all require access to the same Azure Key Vault.

Instead of assigning identical permissions to each application individually, the administrator creates one User-Assigned Managed Identity.

The identity receives the required Azure RBAC role and is attached to every App Service.

This centralizes permission management while eliminating duplicated role assignments.

---

## Best Practices

- Use User-Assigned Managed Identities when multiple resources require the same permissions.
- Apply the principle of least privilege.
- Grant only the required Azure RBAC roles.
- Remove unused identities.
- Monitor role assignments regularly.
- Document identity ownership.

---

## Common Pitfalls

- Using User-Assigned identities when a System-Assigned identity is sufficient.
- Forgetting Azure RBAC assignments.
- Leaving unused identities in the subscription.
- Assigning excessive permissions.
- Forgetting to specify the correct identity when multiple User-Assigned identities exist.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - User-Assigned Managed Identities
> - Independent lifecycle
> - Identity sharing
> - Azure RBAC integration
> - Authentication without credentials
> - Typical enterprise scenarios

---

## Key Takeaways

- User-Assigned Managed Identities are independent Azure resources.
- One identity can be shared by multiple Azure resources.
- Authentication is managed by Microsoft Entra ID.
- Authorization is controlled through Azure RBAC.
- They simplify permission management across multiple workloads.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Managed Identities overview](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview) | Managed Identities overview |
| [Managed Identities FAQ](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/managed-identities-faq) | Managed Identities concepts and lifecycle |
| [Assign a user-assigned managed identity to an Azure VM](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/how-to-configure-managed-identities) | Configure and use User-Assigned Managed Identities |
| [Azure RBAC overview](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure RBAC overview |
| [Microsoft Learn – Managed Identities](https://learn.microsoft.com/training/modules/managed-identities-azure-resources/) | Microsoft Learn module |
