# Azure Storage Services Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for selecting, securing, monitoring, and optimizing Azure Storage services, including Blob Storage, Azure Files, Queue Storage, Table Storage, and Azure Data Lake Storage Gen2.

---

## Overview

Each Azure Storage service is optimized for a specific workload.

Selecting the correct service improves performance, scalability, availability, security, and cost efficiency while reducing operational complexity.

Microsoft recommends understanding each service's strengths instead of using a single storage service for every scenario.

---

## Storage Service Selection

```text
Need object storage?
        │
   ┌────┴────┐
   │         │
  Yes       No
   │         │
   ▼         ▼
Blob Storage   Need shared files?
                    │
             ┌──────┴──────┐
             │             │
            Yes           No
             │             │
             ▼             ▼
        Azure Files   Need messaging?
                             │
                      ┌──────┴──────┐
                      │             │
                     Yes           No
                      │             │
                      ▼             ▼
               Queue Storage   Need NoSQL?
                                     │
                              ┌──────┴──────┐
                              │             │
                             Yes          Analytics?
                              │             │
                              ▼             ▼
                      Table Storage   Data Lake Gen2
```

---

> [!TIP]
> **Key Concepts**
>
> - Select the storage service based on workload requirements.
> - Store only persistent data.
> - Apply identity-based security whenever possible.
> - Use lifecycle management for Blob Storage.
> - Monitor capacity and performance continuously.

---

## Blob Storage

Microsoft recommends:

- Use Block Blobs for general-purpose object storage.
- Use Append Blobs for logging workloads.
- Use Page Blobs only when required for unmanaged VHD scenarios.
- Select the appropriate Access Tier.
- Enable Versioning and Soft Delete for critical data.
- Use Lifecycle Management to automate tier transitions.

---

## Azure Files

Best practices include:

- Use SMB for Windows file-sharing scenarios.
- Use NFS 4.1 for supported Linux workloads requiring high performance.
- Integrate SMB shares with Microsoft Entra ID, Microsoft Entra Domain Services, or Active Directory Domain Services where appropriate.
- Apply Azure RBAC together with NTFS permissions.
- Restrict access using Private Endpoints for production workloads.

---

## Azure File Sync

Azure File Sync extends Azure Files to on-premises Windows Servers.

It allows organizations to centralize file storage in Azure while maintaining local access through Windows Server file shares.

Benefits include:

- Centralized file storage.
- Hybrid file access.
- Simplified backup.
- Multi-office synchronization.
- Reduced on-premises storage requirements.

With **Cloud Tiering** enabled:

- Frequently accessed files remain cached locally.
- Less frequently used files are stored in Azure Files.
- Placeholder files allow users to access cloud data transparently when needed.

This enables organizations to provide access to datasets that are much larger than the available local storage capacity.

> [!IMPORTANT]
> Azure File Sync is a hybrid storage solution that integrates on-premises Windows Servers with Azure Files.

---

## Queue Storage

Recommendations include:

- Keep messages small.
- Design applications to process messages asynchronously.
- Implement retry logic.
- Handle duplicate message processing safely.
- Delete processed messages promptly.

Applications should always assume that a message may be delivered more than once.

---

## Queue Storage Message Size

Azure Queue Storage is intended for lightweight asynchronous messaging.

Important considerations:

- Individual messages have a maximum size of **64 KiB**.
- Messages should contain only the information required to process the workload.

For large payloads, Microsoft recommends the **Claim Check pattern**:

1. Store the file or large object in Azure Blob Storage.
2. Store only the Blob URL or identifier in the queue message.

Applications requiring advanced messaging capabilities such as larger messages, transactions, sessions, or ordered delivery should consider **Azure Service Bus** instead of Queue Storage.

---

## Table Storage

Microsoft recommends:

- Design efficient Partition Keys.
- Select Row Keys carefully.
- Minimize full table scans.
- Optimize queries using PartitionKey and RowKey.
- Use Table Storage only for simple NoSQL workloads.

For advanced querying requirements, evaluate Azure Cosmos DB.

---

## Table Storage Query Design

Azure Table Storage is optimized for key-based lookups.

The only native index is the combination of:

- **PartitionKey**
- **RowKey**

Queries that use both values are highly efficient.

Example:

```text
PartitionKey = "Sales"
RowKey = "10025"
```

Queries that filter only on non-indexed properties require scanning large portions of the table.

Example:

```text
CustomerEmail = "user@contoso.com"
```

Such queries are significantly slower and consume more transactions.

> [!TIP]
> Design the data model so that the most common queries use **PartitionKey** and **RowKey** whenever possible.

---

## Azure Data Lake Storage Gen2

Best practices include:

- Enable Hierarchical Namespace only when analytics capabilities are required.
- Organize directory structures logically.
- Use Microsoft Entra ID authentication.
- Apply Azure RBAC using least privilege.
- Store analytical datasets separately from operational application data.

---

## Security

Across all Azure Storage services:

- Authenticate using Microsoft Entra ID whenever possible.
- Use Azure RBAC instead of Shared Keys.
- Prefer User Delegation SAS over Account SAS.
- Restrict network access.
- Use Private Endpoints for production.
- Store encryption keys in Azure Key Vault when using Customer-managed Keys.

---

## Monitoring

Monitor storage services using:

- Azure Monitor
- Storage Insights
- Azure Advisor
- Activity Log
- Diagnostic Settings
- Log Analytics

Configure alerts for:

- Capacity growth
- High latency
- Availability
- Authorization failures
- Replication health

---

## Cost Optimization

Reduce storage costs by:

- Choose the appropriate Blob Access Tier.
- Use Lifecycle Management policies.
- Delete obsolete blobs, snapshots, and versions.
- Remove unused file shares.
- Archive infrequently accessed data.
- Monitor storage growth regularly.

Review Azure Cost Management and Azure Advisor recommendations.

---

## Enterprise Scenario

A software company stores application images in Blob Storage, departmental documents in Azure Files, asynchronous processing requests in Queue Storage, configuration metadata in Table Storage, and business analytics data in Azure Data Lake Storage Gen2.

Lifecycle Management automatically moves inactive blobs to lower-cost tiers, while Microsoft Entra ID and Azure RBAC secure access across all services.

---

## Best Practices Checklist

- Select the correct storage service.
- Use Block Blobs for general object storage.
- Use Azure Files for shared file access.
- Use Queue Storage for asynchronous messaging.
- Design efficient Partition Keys for Table Storage.
- Enable Versioning and Soft Delete for critical blobs.
- Automate tiering with Lifecycle Management.
- Secure storage using Microsoft Entra ID and Azure RBAC.
- Enable monitoring and alerts.
- Review Azure Advisor recommendations regularly.

---

## Common Pitfalls

- Using Blob Storage as a file server.
- Using Azure Files for object storage.
- Designing poor Partition Keys in Table Storage.
- Selecting Archive tier for frequently accessed data.
- Ignoring Lifecycle Management.
- Leaving storage services publicly accessible.
- Storing sensitive data without encryption or identity-based access control.

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
> - Access Tiers
> - Lifecycle Management
> - Azure RBAC
> - Microsoft Entra ID
> - Cost optimization
> - Storage monitoring

---

## Key Takeaways

- Each Azure Storage service is designed for a specific workload and should be selected accordingly.
- Blob Storage is the preferred service for unstructured object storage and supports lifecycle management and multiple access tiers.
- Azure Files provides managed file shares with identity integration and enterprise file-sharing capabilities.
- Queue Storage and Table Storage support scalable messaging and NoSQL scenarios.
- Security, monitoring, lifecycle automation, and cost optimization are essential for production-ready Azure Storage deployments.

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
| Azure Storage lifecycle management | https://learn.microsoft.com/azure/storage/blobs/lifecycle-management-overview |
| Azure Storage security guide | https://learn.microsoft.com/azure/storage/common/storage-security-guide |
| Azure Monitor for Storage | https://learn.microsoft.com/azure/azure-monitor/insights/storage-insights-overview |
| Microsoft Learn – Explore Azure Storage | https://learn.microsoft.com/training/modules/explore-azure-storage/ |
