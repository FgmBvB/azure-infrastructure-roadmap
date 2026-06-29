# Azure Storage Data Protection and Redundancy

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains how Azure Storage protects data through redundancy, replication, backup features, versioning, soft delete, snapshots, immutable storage, and disaster recovery capabilities.

---

## Overview

Azure Storage is designed to provide extremely high durability and availability.

Every object stored in Azure Storage is automatically replicated according to the selected redundancy option. Azure also offers multiple data protection features to help prevent accidental deletion, ransomware attacks, and data corruption.

Understanding these capabilities is essential for designing resilient storage solutions.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure Storage redundancy options.
- Compare LRS, ZRS, GRS, GZRS, RA-GRS, and RA-GZRS.
- Configure data protection features.
- Understand blob versioning and snapshots.
- Protect against accidental deletion.
- Plan disaster recovery strategies.

---

## Storage Redundancy

Azure automatically replicates data according to the selected redundancy option.

| Redundancy | Description |
|------------|-------------|
| **LRS** | Three copies within a single datacenter. |
| **ZRS** | Three copies across multiple Availability Zones within the same region. |
| **GRS** | LRS in the primary region plus asynchronous replication to a secondary region. |
| **GZRS** | ZRS in the primary region plus asynchronous replication to a secondary region. |
| **RA-GRS** | GRS with read-only access to the secondary region. |
| **RA-GZRS** | GZRS with read-only access to the secondary region. |

---

## Redundancy Comparison

| Option | Zone Protection | Region Protection | Secondary Read Access |
|----------|----------------|-------------------|-----------------------|
| LRS | No | No | No |
| ZRS | Yes | No | No |
| GRS | No | Yes | No |
| GZRS | Yes | Yes | No |
| RA-GRS | No | Yes | Yes |
| RA-GZRS | Yes | Yes | Yes |

---

## Geo-Replication

Geo-redundant storage asynchronously replicates data to an Azure paired region.

Benefits include:

- Disaster recovery
- Regional resiliency
- Protection against regional outages

Replication is managed entirely by Azure.

---

## Last Sync Time

Geo-redundant replication is **asynchronous**, meaning there is always a small delay between writes to the primary region and replication to the secondary region.

Azure exposes the **Last Sync Time** property for Storage Accounts using geo-redundant replication.

Last Sync Time indicates the latest point at which Azure guarantees that all data has been successfully replicated to the secondary region.

Example:

```text
Current time:     10:30 PM
Last Sync Time:   10:15 PM
```

Potential Recovery Point Objective (RPO):

```text
15 minutes
```

If a failover occurs before newer writes are replicated, any data written after the Last Sync Time may be lost.

> [!IMPORTANT]
> Before initiating a customer-managed failover, administrators should review the **Last Sync Time** to estimate the potential amount of data loss.

---

## Account Failover

If Microsoft declares a regional disaster, a geo-redundant Storage Account can be failed over to the secondary region.

Characteristics:

- Secondary region becomes the new primary.
- Applications reconnect using the same Storage Account endpoints.
- The operation cannot be reversed automatically.
- Because replication is asynchronous, the most recent writes may not exist in the secondary region.

Failover should only be initiated when necessary because it permanently changes the account's primary region.

---

## Customer-Managed Account Failover

For supported geo-redundant Storage Accounts, administrators can initiate a **customer-managed failover** without waiting for Microsoft to declare a regional disaster.

During the failover:

- The secondary region becomes the new primary region.
- Storage service endpoints continue using the same account name.
- Azure updates the underlying DNS resolution to direct traffic to the new primary region.
- Because replication is one-way, the redundancy configuration is reduced to **Locally Redundant Storage (LRS)** in the new primary region.

After the original region becomes available again, administrators must reconfigure geo-redundant replication if regional protection is still required.

> [!TIP]
> Customer-managed failover should only be performed when business requirements outweigh the potential loss of data that has not yet been replicated.

---

## Soft Delete

Soft Delete protects against accidental deletion.

Supported resources include:

- Blob Storage
- Azure Files
- Blob Containers

Deleted objects remain recoverable during the configured retention period.

---

## Blob Versioning

Blob Versioning automatically creates a new version whenever a blob is modified.

Benefits include:

- Recovery from accidental overwrites.
- Protection against application errors.
- Simplified rollback.

Older versions remain available until deleted according to lifecycle policies.

---

## Blob Snapshots

Snapshots create read-only copies of blobs at a specific point in time.

Snapshots are useful for:

- Backup
- Recovery
- Auditing
- Testing

Unlike Versioning, snapshots are created manually or by automation.

---

## Change Feed

Change Feed records every change made to blobs in chronological order.

Typical use cases include:

- Auditing
- Synchronization
- Event processing
- Compliance

The Change Feed is append-only and immutable.

---

## Point-in-Time Restore

Point-in-Time Restore enables restoring Blob Storage to a previous point within the configured retention period.

It works together with:

- Blob Versioning
- Change Feed
- Soft Delete

This feature simplifies recovery after accidental deletion or ransomware incidents.

---

## Point-in-Time Restore Requirements

Point-in-Time Restore (PITR) depends on several Blob Storage protection features working together.

Before PITR can be enabled, the following features must already be configured:

- **Blob Versioning**
- **Blob Change Feed**
- **Blob Soft Delete**

These services work together to provide complete recovery capability:

| Feature | Purpose |
|----------|---------|
| **Blob Versioning** | Maintains previous blob versions. |
| **Blob Change Feed** | Records all blob operations in chronological order. |
| **Blob Soft Delete** | Prevents immediate permanent deletion. |

If any required feature is disabled, Point-in-Time Restore cannot be enabled.

> [!IMPORTANT]
> Point-in-Time Restore is available only for Blob Storage and depends on these underlying protection mechanisms.

---

## Immutable Storage

Immutable Storage prevents modification or deletion of stored data.

Supported policies include:

| Policy | Description |
|----------|-------------|
| **Time-based retention** | Data remains immutable until the retention period expires. |
| **Legal Hold** | Data remains protected until the legal hold is removed. |

Immutable Storage is commonly used for regulatory compliance.

---

## Enterprise Scenario

A healthcare organization stores medical records in Azure Blob Storage using **RA-GZRS**.

Blob Versioning, Soft Delete, and Immutable Storage protect against accidental deletion and ransomware.

During a regional outage, applications continue reading data from the secondary region until Microsoft performs a failover.

---

## Best Practices

- Use **ZRS** or **GZRS** for production workloads requiring high availability.
- Enable Soft Delete for Blob Storage and Azure Files.
- Enable Blob Versioning for critical data.
- Use Immutable Storage for compliance workloads.
- Test failover procedures regularly.
- Use Lifecycle Management to control storage costs associated with multiple blob versions.

---

## Common Pitfalls

- Assuming GRS provides automatic failover.
- Forgetting that geo-replication is asynchronous.
- Disabling Soft Delete on production Storage Accounts.
- Confusing Blob Snapshots with Blob Versioning.
- Ignoring storage costs associated with retained versions and snapshots.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - LRS
> - ZRS
> - GRS
> - GZRS
> - RA-GRS
> - RA-GZRS
> - Soft Delete
> - Blob Versioning
> - Blob Snapshots
> - Change Feed
> - Point-in-Time Restore
> - Immutable Storage
> - Account Failover

---

## Key Takeaways

- Azure Storage automatically replicates data according to the selected redundancy option.
- ZRS and GZRS provide higher availability than LRS and GRS by protecting against datacenter failures.
- Blob Versioning, Soft Delete, and Point-in-Time Restore provide powerful recovery capabilities.
- Immutable Storage helps organizations meet regulatory and legal compliance requirements.
- Understanding redundancy and protection features is essential for designing resilient Azure Storage solutions.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Storage redundancy | https://learn.microsoft.com/azure/storage/common/storage-redundancy |
| Azure Storage disaster recovery | https://learn.microsoft.com/azure/storage/common/storage-disaster-recovery-guidance |
| Blob versioning | https://learn.microsoft.com/azure/storage/blobs/versioning-overview |
| Blob snapshots | https://learn.microsoft.com/azure/storage/blobs/snapshots-overview |
| Soft delete for blobs | https://learn.microsoft.com/azure/storage/blobs/soft-delete-blob-overview |
| Soft delete for Azure Files | https://learn.microsoft.com/azure/storage/files/storage-files-prevent-file-share-deletion |
| Change Feed | https://learn.microsoft.com/azure/storage/blobs/storage-blob-change-feed |
| Point-in-Time Restore | https://learn.microsoft.com/azure/storage/blobs/point-in-time-restore-overview |
| Immutable Storage | https://learn.microsoft.com/azure/storage/blobs/immutable-storage-overview |
| Microsoft Learn – Explore Azure Storage | https://learn.microsoft.com/training/modules/explore-azure-storage/ |
