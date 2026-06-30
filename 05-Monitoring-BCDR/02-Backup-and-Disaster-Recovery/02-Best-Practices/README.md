# Azure Backup and Disaster Recovery Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended best practices for designing, operating, securing, and validating Azure Backup and Azure Site Recovery in production environments.

---

# Overview

Business Continuity and Disaster Recovery (BCDR) is more than creating backups.

A successful BCDR strategy ensures that organizations can:

- Recover data
- Restore applications
- Minimize downtime
- Meet compliance requirements
- Continue business operations during disasters

Microsoft recommends combining Azure Backup and Azure Site Recovery as complementary services.

---

# Define Business Requirements First

Technology should follow business requirements.

Before configuring backups or replication, define:

- Recovery Point Objective (RPO)
- Recovery Time Objective (RTO)
- Critical workloads
- Compliance requirements
- Data retention policies

Different workloads often require different protection strategies.

---

# Choose the Appropriate Vault Redundancy

Recovery Services Vault supports multiple redundancy options.

Available choices include:

- Locally Redundant Storage (LRS)
- Zone-Redundant Storage (ZRS)
- Geo-Redundant Storage (GRS)

Choose the redundancy level according to business continuity requirements and budget.

> [!IMPORTANT]
> The storage redundancy option can only be changed while the Recovery Services Vault contains no protected items. Plan redundancy before protecting production resources.

---

# Standardize Backup Policies

Use centralized Backup Policies whenever possible.

Recommendations:

- Reuse policies across similar workloads.
- Standardize schedules.
- Standardize retention periods.
- Separate production and development policies.
- Review policies periodically.

Consistent policies simplify administration.

---

# Protect Critical Workloads

Not all resources require the same level of protection.

Prioritize:

- Domain Controllers
- SQL Servers
- Business-critical Virtual Machines
- Azure Files
- Application servers

Protection should match business impact.

---

# Prefer Application-Consistent Backups

Application-consistent recovery points provide the highest recovery quality.

Whenever supported:

- Use application-consistent backups.
- Validate application integrity after restore.
- Protect transactional workloads with VSS-aware backups.

Crash-consistent backups should only be relied upon when application consistency is unavailable.

---

# Instant Restore Architecture

Azure Virtual Machine backups occur in two stages.

## Snapshot Phase

Azure first creates a snapshot of the managed disks.

Characteristics:

- Fast backup completion.
- Low Recovery Time Objective (RTO).
- Recovery directly from disk snapshots.
- Short-term retention for rapid restores.

This mechanism is known as **Instant Restore**.

---

## Vault Transfer Phase

After the snapshot is created, Azure transfers backup data asynchronously to the Recovery Services Vault.

Benefits include:

- Long-term retention.
- Geo-redundant protection (when configured).
- Compliance retention.
- Protection against disk loss.

Restores from the vault generally take longer than Instant Restore because backup data must be retrieved from vault storage.

> [!TIP]
> Instant Restore minimizes recovery time, while the Recovery Services Vault provides durable long-term protection.

---

# Test Recovery Regularly

Backups that are never tested cannot be trusted.

Recommendations:

- Perform Test Failovers.
- Validate Recovery Points.
- Restore individual files.
- Restore entire Virtual Machines.
- Test application functionality after recovery.

Testing should become part of operational procedures.

---

# Use Azure Site Recovery for Disaster Recovery

Azure Backup protects data.

Azure Site Recovery protects service availability.

Use ASR when workloads require:

- Automatic replication.
- Regional disaster recovery.
- Low Recovery Time Objectives.
- Infrastructure recovery.

Backups alone do not provide business continuity.

---

# Azure Site Recovery Network Preparation

Successful failover requires more than replication.

Before a disaster occurs, administrators should prepare the recovery environment.

Recommendations include:

- Create the destination Virtual Network.
- Configure Network Mapping between source and target VNets.
- Validate subnet mappings.
- Verify Network Security Groups.
- Ensure sufficient regional resource quotas.
- Validate storage and compute availability.

Proper network preparation allows replicated Virtual Machines to start correctly after failover.

> [!IMPORTANT]
> Azure Site Recovery replicates workloads, but administrators remain responsible for preparing the target networking environment before disaster recovery operations.

---

# Enable Soft Delete

Soft Delete provides protection against accidental or malicious deletion.

Benefits include:

- Protection against ransomware.
- Protection against administrative mistakes.
- Recovery of deleted backup items.
- Additional recovery window before permanent deletion.

Leave Soft Delete enabled for production environments.

---

# Monitor Backup Operations

Backup jobs should be monitored continuously.

Monitor:

- Backup success rate.
- Failed jobs.
- Replication health.
- Recovery Point creation.
- Vault capacity.
- Storage consumption.

Azure Monitor should generate alerts for failed backups.

---

# Secure Backup Infrastructure

Backup systems are high-value attack targets.

Recommendations:

- Apply Azure RBAC.
- Restrict Recovery Services Vault administration.
- Enable Multi-Factor Authentication.
- Review backup permissions regularly.
- Protect vault configuration using Resource Locks where appropriate.

Least privilege should always apply.

---

# Protect Against Ransomware

Modern backup strategies must consider cyberattacks.

Recommendations:

- Enable Soft Delete.
- Protect backup administrators.
- Monitor deletion attempts.
- Audit backup operations.
- Separate operational duties where possible.

Backup infrastructure should be considered part of the security perimeter.

---

# Multi-User Authorization (MUA)

Microsoft recommends protecting critical backup operations using **Multi-User Authorization (MUA)**.

MUA uses a **Resource Guard** to require additional authorization before sensitive backup operations can be performed.

Protected operations include:

- Disabling Soft Delete.
- Deleting backup data.
- Reducing backup retention.
- Modifying critical vault settings.

The Resource Guard is typically managed by a different administrative team or subscription.

This separation prevents a compromised Backup Administrator account from performing destructive operations without additional authorization.

> [!IMPORTANT]
> Resource Guard provides an additional security layer for Recovery Services Vaults by enforcing separation of duties for critical backup operations.

---

# Use Cross Region Restore When Required

Business-critical workloads may require regional recovery.

Cross Region Restore provides:

- Recovery from regional outages.
- Improved disaster resilience.
- Additional recovery flexibility.

Ensure the selected vault redundancy supports this capability.

---

# Optimize Costs

Backup generates storage costs.

Recommendations:

- Remove obsolete backup items.
- Review retention policies regularly.
- Avoid unnecessarily long retention periods.
- Select appropriate vault redundancy.
- Monitor storage consumption.
- Review Azure Cost Management recommendations.

Balance resilience with operational costs.

---

# Enterprise Scenario

A multinational organization protects:

- Domain Controllers
- SQL Servers
- Virtual Machine Scale Sets
- Azure Files

Architecture:

- Recovery Services Vault
- Azure Backup
- Azure Site Recovery
- Azure Monitor
- Backup Center

Operations include:

- Daily backups.
- Continuous replication.
- Quarterly Test Failovers.
- Centralized Backup Policies.
- Azure Monitor Alerts.
- Cross Region Restore for critical workloads.

The organization achieves low RPO, low RTO, and centralized operational management.

---

# Best Practices Checklist

- Define RPO and RTO before deployment.
- Choose vault redundancy before protecting resources.
- Standardize Backup Policies.
- Protect business-critical workloads.
- Prefer application-consistent backups.
- Perform regular recovery testing.
- Use Azure Site Recovery for disaster recovery.
- Enable Soft Delete.
- Monitor backup jobs continuously.
- Secure Recovery Services Vault access.
- Protect against ransomware.
- Use Cross Region Restore when required.
- Review retention policies regularly.
- Monitor backup costs.

---

# Common Pitfalls

- Treating backup as disaster recovery.
- Never testing restores.
- Ignoring RPO and RTO.
- Selecting incorrect vault redundancy.
- Forgetting Soft Delete.
- Protecting every workload identically.
- Using inconsistent Backup Policies.
- Ignoring failed backup jobs.
- Excessive retention increasing costs.
- Assuming backups guarantee application recovery.

---

# Advanced Operational Recommendations

## Monitor Recovery Objectives

Regularly validate that business requirements are still met.

Review:

- Recovery Point Objective (RPO)
- Recovery Time Objective (RTO)
- Recovery success rates
- Backup duration
- Replication latency

---

## Document Recovery Procedures

Maintain documented recovery runbooks covering:

- Restore procedures
- Planned Failover
- Unplanned Failover
- Failback
- Recovery validation
- Contact information
- Escalation procedures

Operational documentation significantly reduces recovery time during real incidents.

---

## Validate Disaster Recovery Plans

Perform scheduled disaster recovery exercises.

Include:

- Test Failover execution.
- Application validation.
- Network connectivity testing.
- DNS verification.
- User acceptance testing.

Recovery plans should be continuously improved after each exercise.

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
> - Test Failover
> - Unplanned Failover
> - Failback
> - Soft Delete
> - Cross Region Restore
> - Backup Center
> - RPO
> - RTO
> - Azure Backup best practices

---

# Key Takeaways

- Effective BCDR strategies combine Azure Backup for data protection and Azure Site Recovery for workload availability.
- Recovery Services Vault configuration, backup policies, and vault redundancy should be planned before protecting production resources.
- Regular recovery testing, application-consistent backups, and continuous monitoring are essential to ensure backups remain usable.
- Soft Delete, RBAC, and operational controls help protect backup infrastructure against accidental deletion and ransomware attacks.
- Following Microsoft's BCDR best practices improves resilience, minimizes downtime, and helps organizations meet recovery and compliance objectives.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Backup documentation | https://learn.microsoft.com/azure/backup/backup-overview |
| Azure Site Recovery documentation | https://learn.microsoft.com/azure/site-recovery/site-recovery-overview |
| Recovery Services Vault | https://learn.microsoft.com/azure/backup/backup-azure-recovery-services-vault-overview |
| Backup Center | https://learn.microsoft.com/azure/backup/backup-center-overview |
| Backup Vault | https://learn.microsoft.com/azure/backup/backup-vault-overview |
| Azure Backup best practices | https://learn.microsoft.com/azure/backup/guidance-best-practices |
| Azure Site Recovery failover | https://learn.microsoft.com/azure/site-recovery/site-recovery-failover |
| Azure Well-Architected Framework – Reliability | https://learn.microsoft.com/azure/well-architected/reliability/ |
| Microsoft Learn – Protect Azure resources with Azure Backup | https://learn.microsoft.com/training/modules/protect-vms-with-azure-backup/ |
| Microsoft Learn – Implement disaster recovery with Azure Site Recovery | https://learn.microsoft.com/training/modules/disaster-recovery-site-recovery/ |
