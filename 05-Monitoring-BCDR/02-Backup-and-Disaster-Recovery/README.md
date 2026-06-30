# Azure Backup and Disaster Recovery

> [!NOTE]
> This section is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Microsoft's Business Continuity and Disaster Recovery (BCDR) services, including Azure Backup, Azure Site Recovery, Recovery Services Vaults, backup policies, replication, failover strategies, and production best practices.

---

# Overview

Business Continuity and Disaster Recovery (BCDR) ensures that applications, services, and data remain available when failures occur.

Azure provides two complementary services that address different aspects of resilience:

- **Azure Backup** protects data.
- **Azure Site Recovery (ASR)** protects application availability.

Together they help organizations recover from:

- Accidental deletion
- Hardware failures
- Software corruption
- Ransomware attacks
- Regional outages
- Disaster scenarios

A complete Azure BCDR strategy combines backup, replication, recovery planning, monitoring, and regular testing.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure Backup architecture.
- Configure Recovery Services Vaults.
- Understand Backup Vault.
- Configure Backup Policies.
- Understand Recovery Points.
- Understand Azure Site Recovery.
- Configure workload replication.
- Understand Planned, Unplanned and Test Failover.
- Understand Failback.
- Calculate RPO and RTO.
- Understand Soft Delete.
- Configure Cross Region Restore.
- Understand Backup Center.
- Apply Microsoft's BCDR best practices.

---

# Section Structure

| Document | Description |
|----------|-------------|
| **01 - Overview** | Azure Backup, Recovery Services Vault, Backup Vault, Backup Policies, Recovery Points, Azure Site Recovery, replication, failover, Soft Delete, Cross Region Restore, Backup Center, RPO, RTO, and BCDR fundamentals. |
| **02 - Best Practices** | Backup strategy, vault redundancy, application-consistent backups, Instant Restore, Resource Guard (MUA), Azure Site Recovery planning, ransomware protection, monitoring, recovery testing, governance, and Microsoft's production recommendations. |

---

# Azure BCDR Architecture

```text
                    Production Environment
                            │
        ┌───────────────────┴───────────────────┐
        │                                       │
        ▼                                       ▼
 Azure Backup                         Azure Site Recovery
        │                                       │
        ▼                                       ▼
Recovery Services Vault              Continuous Replication
        │                                       │
        ▼                                       ▼
 Recovery Points                   Secondary Azure Region
        │                                       │
        └───────────────┬───────────────────────┘
                        ▼
               Restore / Failover
                        │
                        ▼
              Business Continuity
```

Azure Backup protects **data**, while Azure Site Recovery protects **running workloads**.

---

# Core Services Covered

This section includes:

## Backup Services

- Azure Backup
- Recovery Services Vault
- Backup Vault
- Backup Policies
- Recovery Points
- Instant Restore
- Soft Delete
- Cross Region Restore
- Backup Center

---

## Disaster Recovery

- Azure Site Recovery (ASR)
- Replication
- Planned Failover
- Unplanned Failover
- Test Failover
- Failback
- Network Mapping

---

## Business Continuity

- Recovery Point Objective (RPO)
- Recovery Time Objective (RTO)
- Backup Strategy
- Disaster Recovery Planning
- Recovery Validation
- Restore Testing

---

## Security

- Azure RBAC
- Resource Guard
- Multi-User Authorization (MUA)
- Ransomware Protection
- Backup Governance

---

# Typical Recovery Workflow

```text
Production Workload

↓

Azure Backup / Azure Site Recovery

↓

Recovery Services Vault

↓

Failure Detected

↓

Recovery Point Selection

↓

Restore or Failover

↓

Business Recovery

↓

Failback (if required)
```

A successful recovery depends on planning, testing, and continuous validation.

---

# Design Principles

Microsoft recommends following these principles:

- Define Recovery Point Objective (RPO) before deployment.
- Define Recovery Time Objective (RTO) before deployment.
- Choose Recovery Services Vault redundancy carefully.
- Standardize Backup Policies.
- Prefer application-consistent backups.
- Protect critical workloads with Azure Site Recovery.
- Test restores and failovers regularly.
- Enable Soft Delete.
- Protect backup infrastructure using Azure RBAC and Resource Guard.
- Monitor backup jobs continuously.

---

# AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Azure Backup
- Recovery Services Vault
- Backup Vault
- Backup Policies
- Recovery Points
- Azure Site Recovery
- Replication
- Planned Failover
- Test Failover
- Unplanned Failover
- Failback
- Soft Delete
- Cross Region Restore
- Backup Center
- RPO
- RTO

---

# Key Takeaways

- Azure Backup and Azure Site Recovery provide complementary capabilities that together form Microsoft's Business Continuity and Disaster Recovery solution.
- Recovery Services Vaults centralize backup management, while Azure Site Recovery enables workload replication and regional failover.
- Recovery objectives (RPO and RTO), backup policies, vault redundancy, and recovery testing should be defined before production deployment.
- Security features such as Soft Delete, Azure RBAC, and Resource Guard help protect backup infrastructure from accidental deletion and ransomware attacks.
- Following Microsoft's BCDR best practices improves resilience, reduces downtime, and ensures workloads can be recovered quickly and reliably.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Backup documentation | https://learn.microsoft.com/azure/backup/backup-overview |
| Azure Site Recovery documentation | https://learn.microsoft.com/azure/site-recovery/site-recovery-overview |
| Recovery Services Vault | https://learn.microsoft.com/azure/backup/backup-azure-recovery-services-vault-overview |
| Backup Vault | https://learn.microsoft.com/azure/backup/backup-vault-overview |
| Backup Center | https://learn.microsoft.com/azure/backup/backup-center-overview |
| Azure Backup best practices | https://learn.microsoft.com/azure/backup/guidance-best-practices |
| Azure Site Recovery failover | https://learn.microsoft.com/azure/site-recovery/site-recovery-failover |
| Azure Well-Architected Framework – Reliability | https://learn.microsoft.com/azure/well-architected/reliability/ |
| Microsoft Learn – Protect Azure resources with Azure Backup | https://learn.microsoft.com/training/modules/protect-vms-with-azure-backup/ |
| Microsoft Learn – Implement disaster recovery with Azure Site Recovery | https://learn.microsoft.com/training/modules/disaster-recovery-site-recovery/ |
