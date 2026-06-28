# Managed Identities

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Managed Identities, including identity lifecycle, authentication, Azure RBAC integration, common use cases, and security best practices.

---

## Overview

Managed Identities provide Azure resources with automatically managed identities in Microsoft Entra ID.

They eliminate the need to store credentials, secrets, or certificates inside applications while allowing workloads to authenticate securely to Azure services.

Managed Identities are commonly used with Virtual Machines, App Services, Azure Functions, Logic Apps, Azure Kubernetes Service (AKS), Azure SQL Database, Azure Key Vault, and Azure Storage.

---

## Learning Objectives

After completing this section you should be able to:

- Understand how Managed Identities work.
- Differentiate between System-Assigned and User-Assigned identities.
- Configure Azure RBAC permissions.
- Authenticate Azure workloads securely.
- Implement Managed Identities in common Azure services.
- Troubleshoot authentication and authorization issues.
- Apply Microsoft security recommendations.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Managed Identity architecture, authentication flow, IMDS, and identity lifecycle. |
| **02 - System Assigned** | System-assigned Managed Identities, lifecycle, authentication, and Azure CLI examples. |
| **03 - User Assigned** | User-assigned Managed Identities, shared identities, lifecycle, and multi-resource scenarios. |
| **04 - Azure RBAC** | Role assignments, authorization flow, control plane vs data plane, and RBAC integration. |
| **05 - Use Cases** | Azure Key Vault, Storage, SQL Database, Azure Arc, and real-world scenarios. |
| **06 - Best Practices** | Security recommendations, governance, least privilege, and operational guidance. |

---

## Architecture

```text
               Azure Resource
                      │
                      ▼
            Managed Identity
                      │
                      ▼
      Microsoft Entra ID (Identity)
                      │
                      ▼
         OAuth 2.0 Access Token
                      │
                      ▼
              Azure Resource
       (Key Vault, Storage, SQL...)
```

---

## Skills Covered

This section includes:

- Managed Identities
- System-Assigned Identity
- User-Assigned Identity
- Azure Instance Metadata Service (IMDS)
- OAuth 2.0 Token Authentication
- Microsoft Entra ID
- Azure RBAC
- Service Principals
- Azure Key Vault
- Azure Storage
- Azure SQL Database
- Azure Arc-enabled Servers
- Identity Lifecycle
- Least Privilege

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Configure Managed Identities.
- Configure Azure RBAC permissions.
- Authenticate Azure resources securely.
- Implement secretless authentication.
- Manage identity lifecycle.
- Troubleshoot Managed Identity authentication.

---

## Key Takeaways

- Managed Identities eliminate the need to store credentials in applications.
- Microsoft Entra ID automatically manages identity lifecycle.
- Azure RBAC determines resource authorization.
- System-Assigned and User-Assigned identities support different architectural scenarios.
- Managed Identities are a core component of secure Azure workload authentication.
