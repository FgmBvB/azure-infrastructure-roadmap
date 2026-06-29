# Azure Storage Services Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces the storage services available within Azure Storage Accounts, explains their architecture, capabilities, access tiers, and common enterprise use cases.

---

## Overview

Azure Storage provides several storage services designed for different types of data and workloads.

Each service is optimized for a specific purpose while sharing the same Storage Account management features, including authentication, networking, encryption, monitoring, and redundancy.

Choosing the appropriate storage service is a fundamental Azure administration skill and a common objective of the AZ-104 certification.

---

## Learning Objectives

After completing this section you should be able to:

- Differentiate Azure Storage services.
- Understand Blob Storage.
- Understand Azure Files.
- Understand Queue Storage.
- Understand Table Storage.
- Understand Azure Data Lake Storage Gen2.
- Select the appropriate storage service for different workloads.

---

## Azure Storage Services

```text
                 Azure Storage Account
                          │
      ┌──────────┬─────────┬─────────┬─────────┐
      │          │         │         │
      ▼          ▼         ▼         ▼
 Blob Storage  Files    Queues    Tables
      │
      ▼
Azure Data Lake
 Storage Gen2
```

---

## Blob Storage

Azure Blob Storage stores unstructured object data.

Typical workloads include:

- Images
- Videos
- Documents
- Backups
- Application packages
- Log files

Blob Storage supports:

- Block Blobs
- Append Blobs
- Page Blobs

It also supports lifecycle management, versioning, snapshots, immutable storage, and multiple access tiers.

---

## Azure Files

Azure Files provides fully managed file shares using standard file-sharing protocols.

Supported protocols include:

- SMB
- NFS

Common use cases include:

- Shared folders
- Lift-and-shift applications
- Home directories
- Configuration repositories

Azure Files can be mounted simultaneously by multiple virtual machines.

---

## Queue Storage

Azure Queue Storage provides reliable message storage for asynchronous communication between applications.

Characteristics:

- Simple messaging service
- Highly scalable
- Durable message storage
- Decouples application components

Typical scenarios include background processing and workload distribution.

---

## Table Storage

Azure Table Storage is a NoSQL key-value datastore.

Characteristics:

- Schema-less design
- Massive scalability
- Low cost
- Fast key-based lookups

Typical scenarios include application metadata, IoT data, and logging.

---

## Azure Data Lake Storage Gen2

Azure Data Lake Storage Gen2 extends Blob Storage by enabling the **Hierarchical Namespace (HNS)** feature.

It is optimized for:

- Big data analytics
- Hadoop-compatible workloads
- Azure Synapse Analytics
- Azure Databricks

It combines Blob Storage scalability with filesystem semantics.

---

## Blob Types

Azure Blob Storage supports three blob types.

| Blob Type | Typical Use |
|------------|-------------|
| **Block Blob** | Documents, images, videos, backups |
| **Append Blob** | Log files and append-only workloads |
| **Page Blob** | Virtual Machine disks (VHDs) |

Selecting the correct blob type improves performance and efficiency.

---

## Access Tiers

Blob Storage supports multiple access tiers.

| Tier | Typical Workload |
|------|------------------|
| **Hot** | Frequently accessed data |
| **Cool** | Infrequently accessed data |
| **Cold** | Rarely accessed data |
| **Archive** | Long-term archival storage |

The appropriate access tier depends on access frequency, retention requirements, and cost considerations.

---

## Service Comparison

| Service | Best For |
|----------|----------|
| **Blob Storage** | Unstructured object storage |
| **Azure Files** | Shared file systems |
| **Queue Storage** | Application messaging |
| **Table Storage** | NoSQL key-value data |
| **Data Lake Storage Gen2** | Analytics and big data |

---

## Enterprise Scenario

A manufacturing company stores product images in Blob Storage, department documents in Azure Files, processing tasks in Queue Storage, device telemetry in Table Storage, and analytical datasets in Azure Data Lake Storage Gen2.

All services operate within Azure Storage Accounts while sharing centralized security, monitoring, redundancy, and networking configurations.

---

## Best Practices

- Use Blob Storage for unstructured data.
- Use Azure Files for shared file access.
- Use Queue Storage for asynchronous messaging.
- Use Table Storage for simple NoSQL datasets.
- Use Data Lake Storage Gen2 for analytics workloads.
- Select the appropriate Blob access tier to optimize costs.

---

## Common Pitfalls

- Using Azure Files as object storage.
- Using Blob Storage instead of Queue Storage for messaging.
- Selecting Archive tier for frequently accessed data.
- Storing relational data in Table Storage.
- Enabling Data Lake Storage Gen2 when hierarchical filesystem features are unnecessary.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Blob Storage
> - Azure Files
> - Queue Storage
> - Table Storage
> - Azure Data Lake Storage Gen2
> - Block Blobs
> - Append Blobs
> - Page Blobs
> - Access Tiers
> - Common storage scenarios

---

## Key Takeaways

- Azure Storage provides specialized services for object storage, file sharing, messaging, NoSQL data, and analytics.
- Blob Storage is the most versatile storage service and supports multiple blob types and access tiers.
- Azure Files provides managed SMB and NFS file shares.
- Queue Storage enables reliable asynchronous communication between distributed applications.
- Choosing the correct storage service improves scalability, performance, availability, and cost optimization.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Blob Storage | https://learn.microsoft.com/azure/storage/blobs/storage-blobs-introduction |
| Azure Files | https://learn.microsoft.com/azure/storage/files/storage-files-introduction |
| Azure Queue Storage | https://learn.microsoft.com/azure/storage/queues/storage-queues-introduction |
| Azure Table Storage | https://learn.microsoft.com/azure/storage/tables/table-storage-overview |
| Azure Data Lake Storage Gen2 | https://learn.microsoft.com/azure/storage/blobs/data-lake-storage-introduction |
| Azure Blob access tiers | https://learn.microsoft.com/azure/storage/blobs/access-tiers-overview |
| Microsoft Learn – Explore Azure Storage | https://learn.microsoft.com/training/modules/explore-azure-storage/ |
