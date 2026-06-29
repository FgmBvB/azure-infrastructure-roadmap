# Azure Storage Services

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers the Azure Storage services available within a Storage Account, including Blob Storage, Azure Files, Queue Storage, Table Storage, and Azure Data Lake Storage Gen2. It also explains their architecture, use cases, security considerations, and Microsoft's recommended operational best practices.

---

## Overview

Azure Storage provides multiple specialized storage services, each designed to solve different data storage requirements.

Although these services share the same Storage Account management features—such as authentication, networking, redundancy, monitoring, and encryption—they are optimized for different workloads, access patterns, and performance characteristics.

Understanding when to use each service is a fundamental skill for Azure administrators and a core objective of the AZ-104 certification.

---

## Learning Objectives

After completing this section you should be able to:

- Differentiate Azure Storage services.
- Select the appropriate storage service for different workloads.
- Understand Blob Storage, Azure Files, Queue Storage, Table Storage, and Azure Data Lake Storage Gen2.
- Understand Blob types and Access Tiers.
- Apply Microsoft's recommended operational best practices.
- Optimize storage performance, scalability, and cost.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Blob Storage, Azure Files, Queue Storage, Table Storage, Azure Data Lake Storage Gen2, Blob types, Access Tiers, Azure File Sync, and service selection guidance. |
| **02 - Best Practices** | Security, lifecycle management, monitoring, cost optimization, performance recommendations, storage service selection, and operational best practices. |

---

## Azure Storage Services Architecture

```text
                    Azure Storage Account
                             │
      ┌────────────┬──────────┬──────────┬──────────┐
      │            │          │          │
      ▼            ▼          ▼          ▼
 Blob Storage   Azure Files  Queues    Tables
      │
      ▼
Azure Data Lake
 Storage Gen2
```

---

## Skills Covered

This section includes:

- Blob Storage
- Block Blobs
- Append Blobs
- Page Blobs
- Blob Access Tiers
- Azure Files
- SMB
- NFS 4.1
- Azure File Sync
- Queue Storage
- Table Storage
- PartitionKey
- RowKey
- Azure Data Lake Storage Gen2
- Hierarchical Namespace (HNS)
- Lifecycle Management
- Cloud Tiering
- Storage Service Selection

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Configure Blob Storage.
- Configure Azure Files.
- Configure Queue Storage.
- Configure Table Storage.
- Configure Azure Data Lake Storage Gen2.
- Select appropriate storage services.
- Configure Blob Access Tiers.
- Understand Azure File Sync.
- Optimize storage performance and costs.

---

## Key Takeaways

- Azure Storage provides specialized services for object storage, file sharing, messaging, NoSQL data, and analytics workloads.
- Blob Storage is the primary service for unstructured data and supports multiple blob types and access tiers.
- Azure Files delivers fully managed SMB and NFS file shares and supports hybrid scenarios through Azure File Sync.
- Queue Storage and Table Storage provide lightweight messaging and NoSQL storage for scalable cloud applications.
- Azure Data Lake Storage Gen2 extends Blob Storage with a hierarchical namespace for analytics workloads.
- Selecting the correct storage service improves performance, scalability, security, and cost optimization.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Blob Storage | https://learn.microsoft.com/azure/storage/blobs/storage-blobs-introduction |
| Azure Files | https://learn.microsoft.com/azure/storage/files/storage-files-introduction |
| Azure File Sync | https://learn.microsoft.com/azure/storage/file-sync/file-sync-planning |
| Azure Queue Storage | https://learn.microsoft.com/azure/storage/queues/storage-queues-introduction |
| Azure Table Storage | https://learn.microsoft.com/azure/storage/tables/table-storage-overview |
| Azure Data Lake Storage Gen2 | https://learn.microsoft.com/azure/storage/blobs/data-lake-storage-introduction |
| Azure Blob access tiers | https://learn.microsoft.com/azure/storage/blobs/access-tiers-overview |
| Azure Storage lifecycle management | https://learn.microsoft.com/azure/storage/blobs/lifecycle-management-overview |
| Microsoft Learn – Explore Azure Storage | https://learn.microsoft.com/training/modules/explore-azure-storage/ |
