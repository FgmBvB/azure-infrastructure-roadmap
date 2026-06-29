# Azure Storage Accounts

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Storage Accounts, including account architecture, storage services, redundancy, data protection, security, networking, encryption, authentication, and Microsoft's recommended operational best practices.

---

## Overview

An **Azure Storage Account** is the foundational resource for Azure Storage services.

It provides a globally unique namespace for storing data and acts as the management boundary for authentication, authorization, networking, encryption, redundancy, monitoring, and billing.

A Storage Account can host multiple storage services while offering enterprise-grade durability, scalability, and availability.

Understanding Storage Accounts is fundamental for the AZ-104 certification because almost every Azure workload depends on them.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure Storage Account architecture.
- Differentiate Storage Account types.
- Understand storage redundancy and replication.
- Configure data protection features.
- Secure Storage Accounts using identity, networking, and encryption.
- Apply Microsoft's operational best practices.
- Select the appropriate Storage Account configuration for different workloads.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Storage Account architecture, account types, storage services, performance tiers, naming rules, endpoints, and Hierarchical Namespace (HNS). |
| **02 - Data Protection and Redundancy** | LRS, ZRS, GRS, GZRS, RA-GRS, RA-GZRS, Soft Delete, Blob Versioning, Snapshots, Change Feed, Point-in-Time Restore, Immutable Storage, geo-replication, failover, and disaster recovery. |
| **03 - Access and Security** | Microsoft Entra ID, Azure RBAC, Shared Keys, Shared Access Signatures (SAS), Storage Firewall, Private Endpoints, Service Endpoints, encryption, Customer-managed Keys (CMKs), and Infrastructure Encryption. |
| **04 - Best Practices** | Storage architecture recommendations, lifecycle management, cost optimization, governance, monitoring, security, and operational best practices. |

---

## Azure Storage Account Architecture

```text
                    Azure Storage Account
                             │
        ┌──────────┬──────────┬──────────┬──────────┐
        │          │          │          │
        ▼          ▼          ▼          ▼
      Blobs      Files      Queues     Tables
        │
        ▼
Data Lake Storage Gen2
(Hierarchical Namespace)
```

---

## Skills Covered

This section includes:

- Storage Accounts
- StorageV2
- Premium Storage Accounts
- Blob Storage
- Azure Files
- Queue Storage
- Table Storage
- Data Lake Storage Gen2
- Hierarchical Namespace (HNS)
- Standard vs Premium
- LRS
- ZRS
- GRS
- GZRS
- RA-GRS
- RA-GZRS
- Account Failover
- Blob Versioning
- Blob Snapshots
- Change Feed
- Point-in-Time Restore (PITR)
- Immutable Storage
- Microsoft Entra ID
- Azure RBAC
- Shared Keys
- Shared Access Signatures (SAS)
- Private Endpoints
- Service Endpoints
- Customer-managed Keys (CMKs)
- Lifecycle Management

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Create and configure Storage Accounts.
- Select appropriate redundancy options.
- Configure Storage Account security.
- Configure authentication and authorization.
- Protect data using Azure Storage features.
- Secure Storage Accounts using networking.
- Implement lifecycle management.
- Optimize storage performance and costs.

---

## Key Takeaways

- Azure Storage Accounts provide the management boundary for Azure Storage services.
- StorageV2 is Microsoft's recommended account type for most workloads.
- Redundancy, replication, and data protection features improve resilience and disaster recovery capabilities.
- Microsoft Entra ID, Azure RBAC, Private Endpoints, and encryption provide layered security for Storage Accounts.
- Proper planning of storage architecture, lifecycle management, and governance improves scalability, operational efficiency, security, and cost optimization.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Storage documentation | https://learn.microsoft.com/azure/storage/ |
| Azure Storage accounts overview | https://learn.microsoft.com/azure/storage/common/storage-account-overview |
| Azure Storage redundancy | https://learn.microsoft.com/azure/storage/common/storage-redundancy |
| Azure Storage disaster recovery guidance | https://learn.microsoft.com/azure/storage/common/storage-disaster-recovery-guidance |
| Azure Storage security guide | https://learn.microsoft.com/azure/storage/common/storage-security-guide |
| Authorize access to Azure Storage | https://learn.microsoft.com/azure/storage/common/authorize-data-access |
| Azure Storage networking | https://learn.microsoft.com/azure/storage/common/storage-network-security |
| Azure Storage encryption | https://learn.microsoft.com/azure/storage/common/storage-service-encryption |
| Azure Storage lifecycle management | https://learn.microsoft.com/azure/storage/blobs/lifecycle-management-overview |
| Azure Data Lake Storage Gen2 | https://learn.microsoft.com/azure/storage/blobs/data-lake-storage-introduction |
| Microsoft Learn – Explore Azure Storage | https://learn.microsoft.com/training/modules/explore-azure-storage/ |
