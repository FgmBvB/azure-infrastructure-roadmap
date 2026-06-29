# Azure Storage

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Storage services, including Storage Accounts, Blob Storage, Azure Files, Queue Storage, Table Storage, Azure Data Lake Storage Gen2, security, redundancy, data protection, lifecycle management, and Microsoft's recommended operational best practices.

---

## Overview

Azure Storage is Microsoft's massively scalable, highly available, durable, and secure cloud storage platform.

It provides multiple storage services designed for different workloads, including object storage, file sharing, messaging, NoSQL databases, and analytics.

Azure Storage is one of the most important Azure services because it is used by virtual machines, backups, containers, databases, applications, monitoring solutions, and disaster recovery services.

Understanding Azure Storage architecture, security, redundancy, and cost optimization is a core objective of the AZ-104 certification.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure Storage architecture.
- Configure Azure Storage Accounts.
- Select the appropriate storage service.
- Configure redundancy and disaster recovery.
- Secure Azure Storage using identity and networking.
- Protect data against accidental deletion and ransomware.
- Optimize performance and storage costs.
- Apply Microsoft's operational best practices.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Storage Accounts** | Storage Account architecture, account types, redundancy, data protection, security, authentication, networking, encryption, lifecycle management, and operational best practices. |
| **02 - Storage Services** | Blob Storage, Azure Files, Queue Storage, Table Storage, Azure Data Lake Storage Gen2, Blob types, Access Tiers, Azure File Sync, workload selection, and service best practices. |
| **03 - Best Practices** | Cross-service architecture recommendations, governance, monitoring, performance optimization, security, lifecycle management, and cost optimization. |

---

## Azure Storage Architecture

```text
                        Azure Storage
                              │
        ┌─────────────────────┴─────────────────────┐
        │                                           │
        ▼                                           ▼
 Storage Accounts                         Storage Services
        │                                           │
        │                    ┌──────────┬──────────┬──────────┬──────────┐
        │                    │          │          │          │
        ▼                    ▼          ▼          ▼          ▼
Authentication          Blob Storage  Azure Files Queues   Tables
Networking                    │
Encryption                    ▼
Redundancy            Data Lake Storage Gen2
Lifecycle
Monitoring
```

---

## Skills Covered

This section includes:

- Azure Storage Accounts
- StorageV2
- Premium Storage Accounts
- Blob Storage
- Azure Files
- Azure File Sync
- Queue Storage
- Table Storage
- Azure Data Lake Storage Gen2
- Hierarchical Namespace (HNS)
- Block Blobs
- Append Blobs
- Page Blobs
- Blob Access Tiers
- LRS
- ZRS
- GRS
- GZRS
- RA-GRS
- RA-GZRS
- Geo-replication
- Account Failover
- Blob Versioning
- Blob Snapshots
- Soft Delete
- Change Feed
- Point-in-Time Restore (PITR)
- Immutable Storage
- Microsoft Entra ID authentication
- Azure RBAC
- Shared Access Signatures (SAS)
- Shared Keys
- Private Endpoints
- Service Endpoints
- Storage Firewall
- Customer-managed Keys (CMKs)
- Lifecycle Management
- Monitoring
- Cost Optimization

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Create and configure Storage Accounts.
- Configure Blob Storage and Azure Files.
- Configure Queue Storage and Table Storage.
- Configure Azure Data Lake Storage Gen2.
- Configure authentication and authorization.
- Configure network access.
- Configure redundancy and disaster recovery.
- Configure data protection features.
- Implement Lifecycle Management.
- Monitor Azure Storage.
- Optimize storage performance and costs.

---

## Key Takeaways

- Azure Storage provides multiple specialized services optimized for different data storage scenarios.
- Storage Accounts are the management boundary for security, networking, redundancy, monitoring, and billing.
- Blob Storage, Azure Files, Queue Storage, Table Storage, and Azure Data Lake Storage Gen2 each serve distinct workload requirements.
- Redundancy, data protection, identity-based security, and lifecycle management are essential for production-ready storage architectures.
- Choosing the appropriate storage service and configuration improves availability, scalability, security, operational efficiency, and cost optimization.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Storage documentation | https://learn.microsoft.com/azure/storage/ |
| Azure Storage accounts overview | https://learn.microsoft.com/azure/storage/common/storage-account-overview |
| Azure Blob Storage | https://learn.microsoft.com/azure/storage/blobs/storage-blobs-introduction |
| Azure Files | https://learn.microsoft.com/azure/storage/files/storage-files-introduction |
| Azure File Sync | https://learn.microsoft.com/azure/storage/file-sync/file-sync-planning |
| Azure Queue Storage | https://learn.microsoft.com/azure/storage/queues/storage-queues-introduction |
| Azure Table Storage | https://learn.microsoft.com/azure/storage/tables/table-storage-overview |
| Azure Data Lake Storage Gen2 | https://learn.microsoft.com/azure/storage/blobs/data-lake-storage-introduction |
| Azure Storage redundancy | https://learn.microsoft.com/azure/storage/common/storage-redundancy |
| Azure Storage security guide | https://learn.microsoft.com/azure/storage/common/storage-security-guide |
| Azure Storage lifecycle management | https://learn.microsoft.com/azure/storage/blobs/lifecycle-management-overview |
| Microsoft Learn – Explore Azure Storage | https://learn.microsoft.com/training/modules/explore-azure-storage/ |
