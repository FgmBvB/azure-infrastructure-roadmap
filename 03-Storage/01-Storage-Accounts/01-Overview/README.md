# Azure Storage Accounts Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Storage Accounts, explains their architecture, account types, performance tiers, redundancy options, and their role as the foundation of Azure Storage services.

---

## Overview

An **Azure Storage Account** is the top-level resource that provides a unique namespace for storing data in Azure.

It acts as a logical container for Azure Storage services, allowing applications to securely store and retrieve highly available, scalable, and durable data.

A single Storage Account can host multiple storage services depending on its configuration.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure Storage Accounts.
- Identify the different storage services.
- Differentiate Storage Account types.
- Understand performance tiers.
- Understand redundancy options.
- Select the appropriate Storage Account for different workloads.

---

## Storage Account Architecture

```text
                Azure Subscription
                       │
                       ▼
                Resource Group
                       │
                       ▼
                Storage Account
        ┌────────┬────────┬────────┬────────┐
        │        │        │        │
        ▼        ▼        ▼        ▼
      Blobs    Files    Queues   Tables
                     │
                     ▼
             Data Lake Gen2
```

---

## What is a Storage Account?

A Storage Account provides:

- A globally unique name.
- Authentication and authorization.
- Replication and redundancy.
- Encryption at rest.
- Network access control.
- A management boundary for Azure Storage services.

Every object stored in Azure Storage belongs to a Storage Account.

---

## Storage Services

Azure Storage supports several services.

| Service | Purpose |
|----------|---------|
| **Blob Storage** | Object storage for unstructured data. |
| **Azure Files** | Managed SMB and NFS file shares. |
| **Queue Storage** | Reliable messaging between applications. |
| **Table Storage** | NoSQL key-value data store. |
| **Data Lake Storage Gen2** | Big data analytics and hierarchical namespaces. |

Each service is covered in detail later in this roadmap.

---

## Storage Account Types

Azure supports several Storage Account types.

| Account Type | Typical Use |
|--------------|-------------|
| **StorageV2 (General-purpose v2)** | Recommended for most workloads. |
| **Premium BlockBlobStorage** | High-performance block blobs. |
| **Premium FileStorage** | High-performance Azure Files. |
| **Premium PageBlobStorage** | Page blobs for Virtual Machine disks. |

For most deployments, Microsoft recommends **General-purpose v2 (StorageV2)**.

---

## Hierarchical Namespace (HNS)

Azure Data Lake Storage Gen2 is built on top of Azure Blob Storage by enabling the **Hierarchical Namespace (HNS)** feature.

Without HNS:

- Blob Storage uses a **flat namespace**.
- Folder structures are virtual and represented as part of the blob name.

With HNS enabled:

- Directories become first-class filesystem objects.
- File and directory operations are optimized.
- Rename and move operations become atomic metadata operations instead of copy-and-delete operations.

```text
Without HNS
photos/
   image1.jpg
   image2.jpg

→ "photos/" is only part of the blob name.

With HNS

photos/
   ├── image1.jpg
   └── image2.jpg

→ "photos" is an actual directory object.
```

Hierarchical Namespace is required for:

- Azure Data Lake Storage Gen2
- Hadoop-compatible analytics workloads
- Azure Synapse Analytics
- Azure Databricks

> [!IMPORTANT]
> HNS significantly improves performance for analytics workloads that frequently rename, move, or reorganize large directory structures.

---

## Performance Tiers

Storage Accounts are available with different performance characteristics.

| Tier | Characteristics |
|------|-----------------|
| **Standard** | HDD-backed storage for most workloads. |
| **Premium** | SSD-backed storage for low latency and high IOPS workloads. |

Premium Storage is available only for selected storage services.

---

## Premium Storage Account Limitations

Premium Storage Accounts are specialized for specific Azure Storage services.

Unlike **General-purpose v2 (StorageV2)** accounts, Premium accounts do not support every storage service.

Examples include:

| Account Type | Supported Service |
|---------------|------------------|
| **BlockBlobStorage** | Block Blobs only |
| **FileStorage** | Azure Files only |
| **PageBlobStorage** | Page Blobs only |

Because each Premium account supports only its corresponding service, organizations often deploy multiple Storage Accounts when different Premium workloads are required.

> [!IMPORTANT]
> General-purpose v2 (StorageV2) remains Microsoft's recommended Storage Account type for most Azure workloads because it supports multiple storage services within a single account.

---

## Storage Endpoints

Every Storage Account exposes service-specific endpoints.

Example:

```text
https://contosostorage.blob.core.windows.net
https://contosostorage.file.core.windows.net
https://contosostorage.queue.core.windows.net
https://contosostorage.table.core.windows.net
```

Applications use these endpoints to access Azure Storage resources.

---

## Secondary Endpoints

When a Storage Account uses **Read-Access Geo-Redundant Storage (RA-GRS)** or **Read-Access Geo-Zone-Redundant Storage (RA-GZRS)**, Azure automatically creates secondary read-only endpoints.

Example:

Primary endpoint

```text
https://contosostorage.blob.core.windows.net
```

Secondary endpoint

```text
https://contosostorage-secondary.blob.core.windows.net
```

Applications can use the secondary endpoint to read replicated data from the paired Azure region.

This allows read-only access even if the primary region becomes unavailable, provided the account uses a read-access geo-redundant replication option.

> [!TIP]
> The secondary endpoint is read-only. Write operations continue to target the primary region until Microsoft performs an official account failover.

---

## Naming Requirements

Storage Account names must:

- Be globally unique.
- Contain between **3 and 24 characters**.
- Use only lowercase letters and numbers.
- Not contain spaces or special characters.

Because the name becomes part of the public endpoint, it cannot conflict with any existing Storage Account in Azure.

---

## Enterprise Scenario

A multinational company deploys a General-purpose v2 Storage Account.

The same account stores:

- Website images in Blob Storage.
- Shared documents in Azure Files.
- Background processing messages in Queue Storage.
- Application metadata in Table Storage.

The company centralizes security, replication, monitoring, and billing within a single Storage Account.

---

## Best Practices

- Use **General-purpose v2** unless a specialized account is required.
- Select Premium Storage only when workloads require high performance.
- Plan Storage Account names carefully because they must be globally unique.
- Separate production and development workloads into different Storage Accounts.
- Monitor capacity and performance using Azure Monitor.

---

## Common Pitfalls

- Creating multiple Storage Accounts unnecessarily.
- Choosing Premium Storage without performance requirements.
- Assuming all storage services support every account type.
- Forgetting that Storage Account names are globally unique.
- Mixing production and testing workloads in the same Storage Account.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Storage Accounts
> - Storage Account types
> - Storage services
> - Standard vs Premium
> - Storage endpoints
> - Naming rules
> - General-purpose v2 accounts

---

## Key Takeaways

- A Storage Account is the management boundary for Azure Storage services.
- General-purpose v2 is the recommended account type for most scenarios.
- Storage Accounts provide authentication, encryption, redundancy, and networking capabilities.
- Different storage services support different workloads.
- Proper Storage Account planning improves security, scalability, and operational efficiency.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Storage documentation | https://learn.microsoft.com/azure/storage/ |
| Azure Storage accounts overview | https://learn.microsoft.com/azure/storage/common/storage-account-overview |
| Types of storage accounts | https://learn.microsoft.com/azure/storage/common/storage-account-overview#types-of-storage-accounts |
| Azure Storage scalability and performance targets | https://learn.microsoft.com/azure/storage/common/scalability-targets-standard-account |
| Azure Storage naming rules | https://learn.microsoft.com/azure/azure-resource-manager/management/resource-name-rules#microsoftstorage |
| Microsoft Learn – Explore Azure Storage | https://learn.microsoft.com/training/modules/explore-azure-storage/
