# Azure Storage Access and Security

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains how Azure Storage secures access to data using Microsoft Entra ID, Azure RBAC, Shared Access Signatures (SAS), Shared Keys, network controls, encryption, and customer-managed keys.

---

## Overview

Azure Storage provides multiple authentication, authorization, networking, and encryption mechanisms to protect stored data.

Microsoft recommends using identity-based authentication whenever possible and limiting the use of shared secrets.

Understanding these security mechanisms is essential for the AZ-104 certification and for securing production Storage Accounts.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure Storage authentication methods.
- Differentiate authentication from authorization.
- Compare Shared Keys and Shared Access Signatures (SAS).
- Configure Microsoft Entra ID authentication.
- Understand Azure RBAC for Storage.
- Secure Storage Accounts using networking features.
- Understand Azure Storage encryption.

---

## Azure Storage Security Model

```text
                Azure Storage Account
                         │
      ┌──────────────────┼──────────────────┐
      │                  │                  │
      ▼                  ▼                  ▼
Authentication     Network Security     Encryption
      │                  │                  │
      ▼                  ▼                  ▼
 Entra ID          Firewall           Microsoft-managed Keys
 Shared Keys       Private Endpoint   Customer-managed Keys
 SAS Tokens        Service Endpoint   Infrastructure Encryption
```

---

## Authentication Methods

Azure Storage supports multiple authentication mechanisms.

| Method | Typical Use |
|---------|-------------|
| **Microsoft Entra ID** | Recommended for users and applications. |
| **Shared Key** | Storage Account access key authentication. |
| **Shared Access Signature (SAS)** | Temporary delegated access. |
| **Anonymous Access** | Public Blob access (when enabled). |

Microsoft recommends using **Microsoft Entra ID** whenever possible.

---

## Azure RBAC

Azure RBAC provides authorization for Azure Storage.

Common built-in roles include:

| Role | Permissions |
|------|-------------|
| **Storage Blob Data Reader** | Read blob data. |
| **Storage Blob Data Contributor** | Read, write, and delete blob data. |
| **Storage Blob Data Owner** | Full blob data management. |
| **Storage Queue Data Contributor** | Manage Queue Storage data. |
| **Storage File Data SMB Share Contributor** | Manage Azure Files data. |

Azure RBAC supports the principle of least privilege.

---

## Shared Access Signatures (SAS)

A Shared Access Signature (SAS) grants temporary access to Azure Storage resources.

Types of SAS include:

| SAS Type | Description |
|----------|-------------|
| **User Delegation SAS** | Signed using Microsoft Entra ID credentials. Recommended for Blob Storage. |
| **Service SAS** | Grants access to a single storage service. |
| **Account SAS** | Grants access across multiple storage services. |

SAS tokens can define:

- Expiration time
- Allowed permissions
- Allowed IP addresses
- HTTPS-only access

---

## Shared Keys

Every Storage Account contains two access keys.

Characteristics:

- Full administrative access.
- Can authenticate applications.
- Support key rotation.
- Should be protected carefully.

Microsoft recommends avoiding Shared Keys whenever Microsoft Entra ID authentication is supported.

---

## Network Security

Storage Accounts can restrict network access.

Supported options include:

- Storage Firewall
- Virtual Network Rules
- IP Network Rules
- Service Endpoints
- Private Endpoints

By default, Storage Accounts are accessible through public endpoints unless network restrictions are configured.

---

## Private Endpoints

Private Endpoints assign a private IP address to the Storage Account inside a Virtual Network.

Benefits include:

- Private network connectivity
- No Internet exposure
- Improved security
- Integration with Azure Private DNS

Private Endpoints are recommended for production environments.

---

## Service Endpoints

Service Endpoints extend Virtual Network identities to Azure Storage.

Unlike Private Endpoints:

- Storage still uses its public endpoint.
- Traffic remains on the Microsoft backbone network.
- Simpler deployment.
- Lower isolation than Private Link.

---

## Encryption

Azure Storage encrypts all data at rest by default.

Supported encryption options include:

| Encryption | Description |
|------------|-------------|
| **Microsoft-managed Keys (MMK)** | Default encryption managed by Azure. |
| **Customer-managed Keys (CMK)** | Encryption keys stored in Azure Key Vault. |

Encryption is transparent to applications.

---

## Infrastructure Encryption

Infrastructure Encryption provides an additional encryption layer below standard Storage Service Encryption.

Benefits include:

- Double encryption.
- Increased protection for sensitive workloads.
- Compliance with strict regulatory requirements.

---

## Enterprise Scenario

A financial organization stores customer documents in Azure Blob Storage.

Users authenticate with Microsoft Entra ID and receive Azure RBAC permissions.

External auditors receive temporary read-only access through User Delegation SAS tokens.

The Storage Account is accessible only through Private Endpoints and uses Customer-managed Keys stored in Azure Key Vault.

---

## Best Practices

- Use Microsoft Entra ID authentication whenever possible.
- Assign permissions using Azure RBAC.
- Prefer User Delegation SAS over Shared Keys.
- Rotate Storage Account access keys regularly.
- Disable Shared Key authorization if not required.
- Restrict public network access.
- Use Private Endpoints for production Storage Accounts.
- Protect encryption keys using Azure Key Vault.

---

## Common Pitfalls

- Using Shared Keys instead of Microsoft Entra ID.
- Creating SAS tokens without expiration dates.
- Leaving Storage Accounts publicly accessible.
- Assigning excessive Azure RBAC permissions.
- Forgetting to rotate Storage Account keys.
- Confusing authentication with authorization.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Microsoft Entra ID authentication
> - Azure RBAC
> - Shared Keys
> - User Delegation SAS
> - Service SAS
> - Account SAS
> - Storage Firewall
> - Private Endpoints
> - Service Endpoints
> - Encryption
> - Customer-managed Keys

---

## Key Takeaways

- Microsoft Entra ID is the recommended authentication mechanism for Azure Storage.
- Azure RBAC provides fine-grained authorization using built-in roles.
- SAS tokens allow secure temporary delegated access without exposing Storage Account keys.
- Private Endpoints provide the highest level of network isolation.
- Azure Storage encrypts all data at rest and supports both Microsoft-managed and customer-managed encryption keys.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Storage security guide | https://learn.microsoft.com/azure/storage/common/storage-security-guide |
| Authorize access to Azure Storage | https://learn.microsoft.com/azure/storage/common/authorize-data-access |
| Azure RBAC for Blob Storage | https://learn.microsoft.com/azure/storage/blobs/assign-azure-role-data-access |
| Shared Access Signatures (SAS) | https://learn.microsoft.com/azure/storage/common/storage-sas-overview |
| Azure Private Link for Storage | https://learn.microsoft.com/azure/storage/common/storage-private-endpoints |
| Azure Storage firewall and virtual networks | https://learn.microsoft.com/azure/storage/common/storage-network-security |
| Azure Storage encryption | https://learn.microsoft.com/azure/storage/common/storage-service-encryption |
| Customer-managed keys for Azure Storage | https://learn.microsoft.com/azure/storage/common/customer-managed-keys-overview |
| Microsoft Learn – Secure Azure Storage | https://learn.microsoft.com/training/modules/secure-azure-storage/ |
