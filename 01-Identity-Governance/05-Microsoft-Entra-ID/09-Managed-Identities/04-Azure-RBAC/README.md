# Azure RBAC Integration

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Managed Identities use Azure Role-Based Access Control (Azure RBAC) to access Azure resources securely.

---

## Authentication vs Authorization

```text
        Azure Resource
     (Managed Identity)
               │
               ▼
     Microsoft Entra ID
(Authentication)
               │
               ▼
      Access Token Issued
               │
               ▼
         Azure RBAC
 (Authorization Check)
               │
       ┌───────┴────────┐
       │                │
       ▼                ▼
Access Granted    Access Denied
```

---

> [!TIP]
> **Key Concepts**
>
> - Managed Identities authenticate through Microsoft Entra ID.
> - Azure RBAC determines what the identity can access.
> - Authentication and authorization are independent processes.
> - Permissions are assigned using Azure role assignments.
> - Least privilege should always be applied.

---

## Overview

A Managed Identity provides authentication but does not automatically grant access to Azure resources.

Authorization is performed through **Azure Role-Based Access Control (Azure RBAC)**.

Administrators assign Azure roles to the Managed Identity, allowing it to access specific Azure resources according to the principle of least privilege.

---

## Authentication vs Authorization

Authentication and authorization perform different functions.

| Authentication | Authorization |
|---------------|---------------|
| Verifies the identity | Determines allowed actions |
| Microsoft Entra ID | Azure RBAC |
| Issues Access Tokens | Evaluates role assignments |
| Occurs first | Occurs after authentication |

Both processes are required before a Managed Identity can access an Azure resource.

---

## Azure Role Assignments

Access is granted by assigning Azure RBAC roles to the Managed Identity.

A role assignment consists of:

- Security principal (Managed Identity)
- Azure role
- Scope

Only after a valid role assignment exists can the Managed Identity access the target resource.

---

## Automation

Azure RBAC role assignments can be created through automation.

### Azure CLI

```bash
az role assignment create \
  --assignee-object-id <ManagedIdentity-ObjectId> \
  --role "Storage Blob Data Reader" \
  --scope "/subscriptions/<subscription-id>/resourceGroups/<resource-group>"
```

---

### Azure PowerShell

```powershell
New-AzRoleAssignment `
    -ObjectId <ManagedIdentity-ObjectId> `
    -RoleDefinitionName "Storage Blob Data Reader" `
    -Scope "/subscriptions/<subscription-id>/resourceGroups/<resource-group>"
```

These commands assign Azure RBAC permissions directly to the Managed Identity.

## RBAC Propagation

Azure RBAC role assignments are not always available immediately after creation.

It can take several minutes for new role assignments to propagate across Azure Resource Manager.

During this period, applications using a Managed Identity may receive authorization errors such as **403 Forbidden**, even though the role assignment has already been created.

When automating deployments, it is recommended to allow time for RBAC propagation before the application attempts to access protected resources.

---

## RBAC Scope

Azure RBAC permissions can be assigned at different scopes.

```text
Management Group
        │
        ▼
 Subscription
        │
        ▼
 Resource Group
        │
        ▼
    Resource
```

Permissions assigned at higher scopes are inherited by lower scopes.

---

## Common Built-in Roles

Typical Azure RBAC roles used with Managed Identities include:

| Role | Typical Use |
|------|-------------|
| Reader | Read Azure resources |
| Contributor | Manage Azure resources |
| Key Vault Secrets User | Read secrets from Azure Key Vault |
| Key Vault Crypto User | Perform cryptographic operations |
| Storage Blob Data Reader | Read blob data |
| Storage Blob Data Contributor | Read and write blob data |

The selected role should always provide only the permissions required.

---

## Control Plane vs Data Plane

Azure RBAC roles apply to different types of operations.

| Plane | Typical Roles | Purpose |
|-------|---------------|---------|
| **Control Plane** | Owner, Contributor, Reader | Manage Azure resources through Azure Resource Manager (ARM). |
| **Data Plane** | Storage Blob Data Reader, Storage Blob Data Contributor, Key Vault Secrets User | Access the data stored inside Azure resources. |

For example:

- A **Contributor** can create or delete a Storage Account but cannot automatically read blob data.
- A **Storage Blob Data Reader** can read blobs but cannot modify the Storage Account itself.

Managed Identities commonly require **Data Plane** roles to access application data securely.

---

## Authorization Flow

```text
Managed Identity
        │
        ▼
Microsoft Entra ID
(Authentication)
        │
        ▼
Access Token
        │
        ▼
Azure Resource
        │
        ▼
Azure RBAC Evaluation
        │
  Role Assigned?
     │        │
     ▼        ▼
   Yes        No
     │        │
     ▼        ▼
Access     Access
Granted    Denied
```

---

## Enterprise Scenario

An Azure Virtual Machine uses a System-Assigned Managed Identity to access Azure Storage.

The administrator assigns the **Storage Blob Data Reader** role at the Storage Account scope.

When the application requests an Access Token, Microsoft Entra ID authenticates the Managed Identity.

Azure Storage evaluates the assigned Azure RBAC role and allows read access to blob data.

---

## Best Practices

- Apply the principle of least privilege.
- Assign permissions at the lowest practical scope.
- Use built-in roles whenever possible.
- Review Azure RBAC assignments regularly.
- Remove unused role assignments.
- Audit privileged access periodically.

---

## Common Pitfalls

- Assuming a Managed Identity automatically has permissions.
- Assigning Contributor unnecessarily.
- Granting permissions at the Subscription scope without justification.
- Confusing authentication with authorization.
- Forgetting to review inherited permissions.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure RBAC
> - Authentication versus authorization
> - Role assignments
> - Azure RBAC scopes
> - Built-in roles
> - Least privilege

---

## Key Takeaways

- Managed Identities authenticate through Microsoft Entra ID.
- Azure RBAC determines resource access.
- Role assignments define permissions.
- Scope determines where permissions apply.
- Least privilege improves security.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Azure RBAC overview](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure RBAC fundamentals |
| [Assign Azure roles using the Azure portal](https://learn.microsoft.com/azure/role-based-access-control/role-assignments-portal) | Create Azure RBAC role assignments |
| [Managed Identities overview](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview) | Managed Identities overview |
| [Managed identities FAQ](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/managed-identities-faq) | Managed Identity concepts and lifecycle |
| [Microsoft Learn – Secure Azure resources with managed identities](https://learn.microsoft.com/training/modules/managed-identities-azure-resources/) | Microsoft Learn module |
