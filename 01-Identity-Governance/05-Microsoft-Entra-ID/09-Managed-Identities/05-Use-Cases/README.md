# Managed Identity Use Cases

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It presents common scenarios where Managed Identities provide secure, credential-free authentication between Azure resources.

---

## Typical Architecture

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
          OAuth 2.0 Token
                  │
                  ▼
        Azure Protected Resource
(Key Vault, Storage, SQL, ARM, Graph)
```

---

> [!TIP]
> **Key Concepts**
>
> - Managed Identities eliminate credential management.
> - Azure resources authenticate through Microsoft Entra ID.
> - Azure RBAC authorizes resource access.
> - System-Assigned identities suit single-resource workloads.
> - User-Assigned identities simplify shared access across multiple resources.

---

## Overview

Managed Identities are designed to allow Azure resources to authenticate securely without storing credentials.

Instead of embedding Client Secrets or Certificates inside applications, Azure automatically provides OAuth 2.0 Access Tokens through Microsoft Entra ID.

This model improves security, simplifies administration, and reduces operational overhead.

---

## Azure Key Vault

One of the most common scenarios is accessing Azure Key Vault.

Typical examples include:

- Retrieving application secrets.
- Reading certificates.
- Accessing encryption keys.

Applications authenticate using a Managed Identity, while Azure RBAC or Key Vault access controls determine whether access is allowed.

> [!NOTE]
>
> Azure Key Vault supports two authorization models:
>
> - **Azure RBAC** (recommended)
> - **Vault Access Policies**
>
> Only one authorization model is active for a Key Vault at a time.
>
> If the Key Vault uses **Vault Access Policies**, Azure RBAC roles such as **Key Vault Secrets User** do not grant access to secrets.
>
> In that case, the Managed Identity must be explicitly added to the Key Vault Access Policies.

---



## Azure Storage

Managed Identities can securely access Azure Storage services.

Common scenarios include:

- Reading Blob Storage.
- Uploading files.
- Processing queues.
- Accessing Azure Files.

Applications authenticate without storage account keys or Shared Access Signatures (SAS).

---

## Azure SQL Database

Applications frequently use Managed Identities to connect to Azure SQL Database.

Benefits include:

- Passwordless authentication.
- Centralized identity management.
- Elimination of SQL passwords in configuration files.

Database permissions remain independent from Azure RBAC and must be configured inside SQL when required.

> [!NOTE]
>
> Azure RBAC alone does not grant access to databases inside Azure SQL Database.
>
> The Managed Identity must also be created as a contained database user by a Microsoft Entra administrator.
>
> Example:
>
> ```sql
> CREATE USER [MyManagedIdentity] FROM EXTERNAL PROVIDER;
> ALTER ROLE db_datareader ADD MEMBER [MyManagedIdentity];
> ```
>
> Database permissions are managed independently from Azure RBAC.

---

## Azure Resource Manager

Automation services often require access to Azure Resource Manager (ARM).

Examples include:

- Creating resources.
- Updating resource properties.
- Deploying infrastructure.
- Managing virtual machines.

Azure RBAC determines which management operations are permitted.

---

## Microsoft Graph

Managed Identities can authenticate to Microsoft Graph using **Application Permissions**.

Typical scenarios include:

- Reading users.
- Managing groups.
- Querying directory information.
- Automating administrative tasks.

Administrator consent is required before Microsoft Graph permissions can be used.

---

## Azure Kubernetes Service (AKS)

Managed Identities are commonly used with Azure Kubernetes Service.

Typical scenarios include:

- Accessing Azure Key Vault.
- Pulling container images.
- Accessing Azure Storage.
- Authenticating workloads without secrets.

Azure recommends Managed Identities instead of storing credentials inside Kubernetes workloads.

---

## Automation and Serverless

Managed Identities integrate naturally with Azure automation services.

Examples include:

- Azure Functions.
- Azure Automation.
- Logic Apps.
- Container Apps.
- App Service.

Applications obtain Access Tokens automatically without storing credentials.

---

## Azure Arc-enabled Servers

Although Managed Identities are primarily designed for Azure resources, they can also be used with **Azure Arc-enabled servers**.

When a server is connected to Azure Arc, the Azure Connected Machine agent exposes a local identity endpoint that allows applications to obtain Microsoft Entra ID Access Tokens in a similar way to native Azure resources.

This enables hybrid and on-premises workloads to securely authenticate to Azure services without storing credentials.

---

## System-Assigned vs User-Assigned

| Scenario | Recommended Identity |
|----------|----------------------|
| Single Virtual Machine | System-Assigned |
| Single App Service | System-Assigned |
| Multiple App Services sharing permissions | User-Assigned |
| Shared identity across multiple workloads | User-Assigned |
| Temporary workload | System-Assigned |

Choosing the appropriate identity type simplifies administration and reduces unnecessary role assignments.

---

## Enterprise Scenario

A company hosts five Azure App Services that all require access to the same Azure Key Vault and Storage Account.

Instead of creating separate permissions for every application, the administrator deploys one User-Assigned Managed Identity.

The identity receives the required Azure RBAC roles and is attached to every App Service.

All applications authenticate through Microsoft Entra ID while sharing the same centralized authorization model.

---

## Best Practices

- Prefer Managed Identities over Client Secrets.
- Use System-Assigned identities whenever sharing is unnecessary.
- Use User-Assigned identities for shared workloads.
- Apply the principle of least privilege.
- Assign Azure RBAC roles at the lowest practical scope.
- Remove unused identities and role assignments.

---

## Common Pitfalls

- Storing credentials when Managed Identities are supported.
- Granting excessive Azure RBAC permissions.
- Using User-Assigned identities unnecessarily.
- Forgetting administrator consent for Microsoft Graph.
- Confusing Azure RBAC with application-level permissions.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Key Vault integration
> - Azure Storage authentication
> - Azure SQL authentication
> - Azure Resource Manager access
> - Microsoft Graph integration
> - Choosing between System-Assigned and User-Assigned identities

---

## Key Takeaways

- Managed Identities eliminate the need to manage credentials.
- Microsoft Entra ID authenticates Azure resources.
- Azure RBAC authorizes access to Azure resources.
- System-Assigned identities are ideal for single-resource scenarios.
- User-Assigned identities simplify permission management across multiple Azure resources.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Managed Identities overview](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview) | Managed Identities overview |
| [Authenticate to Azure resources with managed identities](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/how-to-use-vm-token) | Obtain access tokens using Managed Identities |
| [Azure RBAC overview](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure RBAC overview |
| [Microsoft Graph authentication](https://learn.microsoft.com/graph/auth/auth-concepts) | Microsoft Graph authentication concepts |
| [Microsoft Learn – Managed Identities](https://learn.microsoft.com/training/modules/managed-identities-azure-resources/) | Microsoft Learn module |
