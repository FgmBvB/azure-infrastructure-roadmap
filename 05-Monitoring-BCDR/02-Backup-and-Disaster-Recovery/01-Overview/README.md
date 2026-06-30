# Azure Backup and Disaster Recovery Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Microsoft's Business Continuity and Disaster Recovery (BCDR) services, focusing on Azure Backup, Azure Site Recovery, Recovery Services Vaults, Backup Vaults, replication, failover, and recovery planning.

---

# Overview

Business Continuity and Disaster Recovery (BCDR) ensures that workloads remain available and recoverable during failures, accidental deletions, cyberattacks, or regional outages.

Azure provides fully managed services that help organizations:

- Protect business-critical data
- Recover deleted resources
- Restore applications after disasters
- Replicate workloads across regions
- Meet Recovery Time Objectives (RTO)
- Meet Recovery Point Objectives (RPO)

Azure separates backup and disaster recovery into complementary services.

---

# Azure BCDR Architecture

```text
Production Resources
        │
        ├──────── Azure Backup
        │              │
        │              ▼
        │      Recovery Services Vault
        │
        └──────── Azure Site Recovery
                       │
                       ▼
              Replicated Workloads
                       │
                       ▼
                Secondary Region
```

Azure Backup protects data.

Azure Site Recovery protects workload availability.

---

# Business Continuity vs Disaster Recovery

Although often used together, they solve different problems.

| Business Continuity | Disaster Recovery |
|--------------------|-------------------|
| Protects business operations | Restores services after major failures |
| Focuses on minimizing downtime | Focuses on recovering workloads |
| Includes backup strategies | Includes replication and failover |
| Prevents data loss | Restores infrastructure |

A complete BCDR strategy requires both.

---

# Azure Backup

Azure Backup is Microsoft's managed backup solution.

Supported workloads include:

- Azure Virtual Machines
- Azure Files
- Azure SQL
- Azure Database for PostgreSQL
- Azure Blobs (selected scenarios)
- On-premises Windows Servers
- Hyper-V
- VMware

Azure Backup provides:

- Automated backups
- Policy-based scheduling
- Encryption
- Long-term retention
- Soft Delete
- Instant Restore

---

# Recovery Services Vault

Recovery Services Vault is the central management resource for Azure Backup and Azure Site Recovery.

It stores:

- Backup metadata
- Recovery points
- Replication configuration
- Backup policies
- Recovery information

One vault can protect multiple workloads.

---

# Backup Vault

Backup Vault is Microsoft's newer vault type designed primarily for modern backup workloads.

It supports:

- Operational Backup
- Vaulted Backup
- Enhanced backup management

Azure continues expanding Backup Vault capabilities across Azure services.

---

# Backup Policies

Backup Policies define how backups are performed.

Policies include:

- Backup schedule
- Backup frequency
- Retention period
- Recovery point retention

Multiple resources can share the same policy.

---

# Recovery Points

Each successful backup creates a recovery point.

Recovery points allow administrators to restore:

- Entire Virtual Machines
- Individual files
- Individual disks
- Databases
- Azure Files

The number of available recovery points depends on the configured retention policy.

---

# Azure Site Recovery (ASR)

Azure Site Recovery provides disaster recovery through workload replication.

Supported scenarios include:

- Azure-to-Azure replication
- VMware-to-Azure
- Hyper-V-to-Azure
- Physical server-to-Azure

ASR continuously replicates workloads to a secondary location.

---

# Replication

Replication transfers workload changes to a secondary region.

Characteristics include:

- Continuous replication
- Incremental updates
- Automated synchronization
- Recovery point creation

Replication minimizes potential data loss.

---

# Failover Types

Azure Site Recovery supports several failover scenarios.

### Test Failover

Creates an isolated recovery environment.

Purpose:

- Validate recovery plans.
- Test disaster recovery procedures.
- No production impact.

---

### Planned Failover

Used when downtime is expected.

Characteristics:

- Minimal data loss.
- Graceful shutdown.
- Final synchronization before failover.

---

### Unplanned Failover

Used during unexpected outages.

Examples:

- Regional failures
- Hardware failures
- Natural disasters

Recovery occurs using the most recent replicated recovery point.

---

### Failback

After the primary site becomes available, workloads can return to the original location.

Failback synchronizes changes made during disaster recovery operations.

---

# Recovery Objectives

Every disaster recovery strategy is built around two objectives.

## Recovery Point Objective (RPO)

RPO defines the maximum acceptable amount of data loss.

Lower RPO requires more frequent replication.

---

## Recovery Time Objective (RTO)

RTO defines the maximum acceptable recovery time.

Lower RTO requires faster recovery procedures.

---

# Soft Delete

Azure Backup protects deleted backup data using Soft Delete.

Benefits include:

- Protection against accidental deletion.
- Protection against malicious deletion.
- Additional recovery window.

Soft Delete is enabled by default for supported backup workloads.

---

# Cross Region Restore

Cross Region Restore allows backups stored in geo-redundant vaults to be restored in the paired Azure region.

Benefits include:

- Regional disaster recovery.
- Faster recovery during large-scale outages.
- Improved business continuity.

Cross Region Restore requires appropriate vault redundancy.

---

# Backup Center

Azure Backup Center provides centralized management for backup resources.

Administrators can:

- View protected resources.
- Monitor backup jobs.
- Review recovery points.
- Manage policies.
- Track compliance.

---

# Typical Recovery Workflow

```text
Production Workload

↓

Backup / Replication

↓

Recovery Services Vault

↓

Incident

↓

Recovery Point Selection

↓

Restore / Failover

↓

Business Recovery
```

---

# Enterprise Scenario

A company operates:

- Virtual Machines
- Azure SQL
- Azure Files
- Storage Accounts

Azure Backup performs daily backups using centralized Backup Policies.

Recovery Services Vault stores backup metadata and recovery points.

Azure Site Recovery continuously replicates production Virtual Machines to another Azure region.

During a regional outage:

- Planned workloads use Test Failover procedures.
- Critical systems execute Unplanned Failover.
- Operations resume in the secondary region.
- Failback occurs after the primary region becomes available.

---

# Common Pitfalls

- Not testing recovery procedures.
- Using only backups without disaster recovery planning.
- Ignoring RPO and RTO requirements.
- Forgetting Soft Delete.
- Using inconsistent backup policies.
- Not monitoring backup jobs.
- Choosing insufficient retention periods.
- Assuming backup equals high availability.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure Backup
> - Recovery Services Vault
> - Backup Vault
> - Backup Policies
> - Recovery Points
> - Azure Site Recovery
> - Replication
> - Planned Failover
> - Unplanned Failover
> - Test Failover
> - Failback
> - Soft Delete
> - Cross Region Restore
> - Backup Center
> - RPO
> - RTO

---

# Key Takeaways

- Azure Backup and Azure Site Recovery provide complementary capabilities for business continuity and disaster recovery.
- Recovery Services Vault centralizes backup and replication management, while Backup Policies automate protection and retention.
- Azure Site Recovery enables continuous replication and multiple failover options to minimize downtime during disasters.
- Recovery Point Objective (RPO) and Recovery Time Objective (RTO) are fundamental metrics for designing recovery strategies.
- Regular testing, appropriate retention policies, and centralized management are essential for a reliable BCDR implementation.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Backup documentation | https://learn.microsoft.com/azure/backup/backup-overview |
| Azure Site Recovery documentation | https://learn.microsoft.com/azure/site-recovery/site-recovery-overview |
| Recovery Services Vault | https://learn.microsoft.com/azure/backup/backup-azure-recovery-services-vault-overview |
| Backup Center | https://learn.microsoft.com/azure/backup/backup-center-overview |
| Backup Vault | https://learn.microsoft.com/azure/backup/backup-vault-overview |
| Azure Backup support matrix | https://learn.microsoft.com/azure/backup/backup-support-matrix |
| Azure Site Recovery failover | https://learn.microsoft.com/azure/site-recovery/site-recovery-failover |
| Azure Well-Architected Framework – Reliability | https://learn.microsoft.com/azure/well-architected/reliability/ |
| Microsoft Learn – Protect Azure resources with Azure Backup | https://learn.microsoft.com/training/modules/protect-vms-with-azure-backup/ |
| Microsoft Learn – Implement disaster recovery with Azure Site Recovery | https://learn.microsoft.com/training/modules/disaster-recovery-site-recovery/ |
