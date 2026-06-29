# Azure Storage Accounts Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for designing, securing, monitoring, and optimizing Azure Storage Accounts used in production environments.

---

## Overview

Azure Storage Accounts are the foundation of nearly every Azure workload.

Choosing the correct account type, redundancy option, authentication method, and networking configuration significantly improves security, availability, performance, and cost efficiency.

Microsoft recommends following a Zero Trust approach while leveraging Azure-native management and monitoring services.

---

## Storage Design Lifecycle

```text
Plan
 │
 ▼
Deploy
 │
 ▼
Secure
 │
 ▼
Protect
 │
 ▼
Monitor
 │
 ▼
Optimize
```

---

> [!TIP]
> **Key Concepts**
>
> - Use General-purpose v2 (StorageV2) for most workloads.
> - Protect data with appropriate redundancy.
> - Authenticate with Microsoft Entra ID whenever possible.
> - Restrict network access.
> - Monitor storage continuously.

---

## Choose the Right Storage Account

Microsoft recommends selecting the Storage Account based on workload requirements.

| Scenario | Recommended Account |
|----------|---------------------|
| General workloads | StorageV2 |
| High-performance Blob Storage | Premium BlockBlobStorage |
| High-performance Azure Files | Premium FileStorage |
| Virtual Machine page blobs | Premium PageBlobStorage |

Avoid Premium Storage unless the workload requires low latency or high IOPS.

---

## Redundancy

Choose redundancy according to business requirements.

| Requirement | Recommended Option |
|-------------|--------------------|
| Lowest cost | LRS |
| Datacenter protection | ZRS |
| Regional disaster recovery | GRS |
| Zone and regional protection | GZRS |
| Read access during regional outage | RA-GRS / RA-GZRS |

Remember that geo-replication is asynchronous and may result in a small amount of data loss during failover.

---

## Security

Microsoft recommends:

- Authenticate using Microsoft Entra ID.
- Assign permissions using Azure RBAC.
- Prefer User Delegation SAS over Shared Keys.
- Disable Shared Key authorization whenever possible.
- Rotate Storage Account keys regularly.
- Store Customer-managed Keys (CMKs) in Azure Key Vault.
- Apply the principle of least privilege.

---

## Network Security

Protect Storage Accounts by:

- Restricting public network access.
- Using Private Endpoints for production workloads.
- Using Service Endpoints when Private Link is unnecessary.
- Allowing only trusted IP addresses and VNets.
- Enabling **Allow trusted Microsoft services** only when required.

Never expose production Storage Accounts to unrestricted public access unless explicitly required.

---

## Data Protection

Enable data protection features appropriate to the workload.

Recommended features include:

- Soft Delete
- Blob Versioning
- Change Feed
- Point-in-Time Restore
- Immutable Storage

Regularly validate backup and recovery procedures.

---

## Performance

Optimize performance by:

- Selecting the correct storage performance tier.
- Choosing the appropriate redundancy option.
- Monitoring latency and throughput.
- Separating high-performance workloads into dedicated Storage Accounts.
- Reviewing scalability limits before large deployments.

---

## Cost Optimization

Reduce storage costs by:

- Using Standard Storage whenever possible.
- Applying Lifecycle Management policies.
- Moving infrequently accessed data to Cool or Archive tiers.
- Removing unused snapshots and blob versions.
- Deleting unused Storage Accounts and orphaned resources.
- Monitoring storage consumption with Azure Cost Management.

---

## Access Tier Cost Considerations

Azure Blob Storage supports multiple access tiers for cost optimization.

| Access Tier | Minimum Retention Period | Typical Use |
|------------|---------------------------|-------------|
| **Hot** | None | Frequently accessed data |
| **Cool** | 30 days | Infrequently accessed data |
| **Cold** | 90 days | Rarely accessed data |
| **Archive** | 180 days | Long-term offline archive |

Important cost considerations:

- Moving data to cheaper tiers reduces storage cost but can increase access costs.
- Deleting or moving blobs before the minimum retention period may trigger early deletion charges.
- Archive tier is offline and requires rehydration before data can be read.
- Archive rehydration can take several hours depending on the selected priority.

> [!IMPORTANT]
> Archive tier is not suitable for data that must be accessed immediately.

---

## Monitoring

Monitor Storage Accounts using:

- Azure Monitor
- Storage Insights
- Azure Advisor
- Activity Log
- Diagnostic Settings
- Log Analytics

Configure alerts for:

- Capacity growth
- Availability
- Replication health
- Unauthorized access attempts
- High latency

---

## Lifecycle Management Rules

Azure Storage Lifecycle Management automates blob tiering and deletion.

Lifecycle rules run automatically in the background and can move or delete blobs based on conditions such as:

- Blob age
- Last modified date
- Last access time
- Blob type
- Blob prefix
- Blob index tags

Prefix filters allow administrators to apply lifecycle actions only to specific containers or virtual folder paths.

Example use cases:

- Move `logs/archive/` blobs to Archive after 180 days.
- Delete temporary files under `tmp/` after 30 days.
- Move infrequently accessed backup files to Cool or Cold tiers.

Using filters prevents lifecycle policies from affecting unrelated or sensitive data.

---

## Governance

Microsoft recommends:

- Apply Azure Policy to enforce storage standards.
- Protect critical Storage Accounts with Resource Locks.
- Use consistent resource tags.
- Standardize naming conventions.
- Separate production, development, and testing environments.

---

## Resource Locks and Storage Data

Resource Locks protect the Storage Account resource at the Azure Resource Manager control plane.

For example, a **CanNotDelete** lock can prevent administrators from deleting the Storage Account itself.

However, Resource Locks do **not** protect the data stored inside the account.

A user or application with sufficient data-plane permissions can still:

- Delete blobs.
- Delete containers.
- Modify files.
- Run lifecycle management policies.
- Change blob versions where permitted.

To protect storage data, use data-plane protection features such as:

- Blob Soft Delete
- Container Soft Delete
- Blob Versioning
- Immutable Storage
- Azure RBAC for data access

> [!IMPORTANT]
> Resource Locks protect the Storage Account resource, not the individual blobs, files, queues, or tables stored inside it.

---

## Enterprise Scenario

A multinational company stores business-critical documents in Azure Storage.

The Storage Accounts use **StorageV2**, **RA-GZRS**, **Microsoft Entra ID**, **Azure RBAC**, **Private Endpoints**, and **Customer-managed Keys**.

Lifecycle Management automatically moves inactive data to the Cool tier, while Azure Monitor continuously tracks storage health and generates alerts for abnormal activity.

---

## Best Practices Checklist

- Use StorageV2 for most workloads.
- Select the appropriate redundancy option.
- Authenticate with Microsoft Entra ID.
- Prefer Azure RBAC over Shared Keys.
- Use User Delegation SAS whenever possible.
- Restrict public network access.
- Enable Private Endpoints for production.
- Protect data with Soft Delete and Versioning.
- Configure monitoring and alerts.
- Apply Lifecycle Management policies.
- Review Azure Advisor recommendations regularly.

---

## Common Pitfalls

- Using Premium Storage unnecessarily.
- Leaving Storage Accounts publicly accessible.
- Relying on Shared Keys instead of Microsoft Entra ID.
- Assuming geo-replication is synchronous.
- Ignoring Storage Account scalability limits.
- Forgetting to rotate Storage Account keys.
- Storing critical data without versioning or Soft Delete.
- Allowing storage costs to grow due to unmanaged snapshots or blob versions.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Storage Account types
> - Redundancy options
> - Microsoft Entra ID authentication
> - Azure RBAC
> - Shared Keys
> - User Delegation SAS
> - Private Endpoints
> - Soft Delete
> - Blob Versioning
> - Lifecycle Management
> - Cost optimization

---

## Key Takeaways

- StorageV2 is Microsoft's recommended Storage Account type for most Azure workloads.
- Security should prioritize Microsoft Entra ID, Azure RBAC, Private Endpoints, and least privilege.
- Data protection features such as Soft Delete, Versioning, and Immutable Storage improve resilience against accidental deletion and ransomware.
- Monitoring, governance, and Lifecycle Management reduce operational risk and optimize storage costs.
- Choosing the correct Storage Account architecture improves availability, performance, security, and long-term maintainability.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Storage documentation | https://learn.microsoft.com/azure/storage/ |
| Azure Storage accounts overview | https://learn.microsoft.com/azure/storage/common/storage-account-overview |
| Azure Storage redundancy | https://learn.microsoft.com/azure/storage/common/storage-redundancy |
| Azure Storage security guide | https://learn.microsoft.com/azure/storage/common/storage-security-guide |
| Azure Storage networking | https://learn.microsoft.com/azure/storage/common/storage-network-security |
| Azure Storage lifecycle management | https://learn.microsoft.com/azure/storage/blobs/lifecycle-management-overview |
| Azure Monitor for Storage | https://learn.microsoft.com/azure/azure-monitor/insights/storage-insights-overview |
| Azure Advisor | https://learn.microsoft.com/azure/advisor/advisor-overview |
| Microsoft Learn – Explore Azure Storage | https://learn.microsoft.com/training/modules/explore-azure-storage/ |
