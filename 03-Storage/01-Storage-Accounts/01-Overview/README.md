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

## Performance Tiers

Storage Accounts are available with different performance characteristics.

| Tier | Characteristics |
|------|-----------------|
| **Standard** | HDD-backed storage for most workloads. |
| **Premium** | SSD-backed storage for low latency and high IOPS workloads. |

Premium Storage is available only for selected storage services.

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
