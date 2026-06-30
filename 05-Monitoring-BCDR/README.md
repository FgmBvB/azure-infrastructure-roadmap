# 📊 Monitoring & Business Continuity

> [!NOTE]
> This module is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure's monitoring, observability, backup, and disaster recovery services, focusing on how administrators detect issues, protect workloads, and ensure business continuity in production environments.

---

# Overview

Operating Azure successfully requires much more than deploying infrastructure.

Administrators must continuously monitor resources, detect operational issues, respond to incidents, protect critical data, and recover services when failures occur.

This module covers Microsoft's native monitoring and Business Continuity & Disaster Recovery (BCDR) platform, including:

- Azure Monitor
- Log Analytics
- Azure Backup
- Azure Site Recovery
- Recovery Services Vault
- Backup Center
- Business Continuity planning

Together, these services help organizations improve reliability, reduce downtime, and meet recovery objectives.

---

# Learning Objectives

After completing this module you should be able to:

- Understand Azure Monitor architecture.
- Collect and analyze metrics and logs.
- Configure Log Analytics Workspaces.
- Configure Azure Monitor Agent (AMA).
- Configure Data Collection Rules (DCR).
- Configure Azure Monitor Alerts and Action Groups.
- Understand Azure Service Health and Resource Health.
- Configure Azure Backup.
- Configure Recovery Services Vaults.
- Understand Backup Vault.
- Configure Azure Site Recovery.
- Understand replication and failover.
- Calculate RPO and RTO.
- Apply Microsoft's monitoring and disaster recovery best practices.

---

# Module Structure

| Section | Description |
|----------|-------------|
| **01 - Monitoring** | Azure Monitor, Metrics, Logs, Log Analytics Workspace, Azure Monitor Agent (AMA), Data Collection Rules (DCR), Alerts, Action Groups, Service Health, Resource Health, Azure Advisor, and monitoring best practices. |
| **02 - Backup and Disaster Recovery** | Azure Backup, Recovery Services Vault, Backup Vault, Azure Site Recovery (ASR), replication, failover, recovery planning, ransomware protection, and business continuity best practices. |
| **03 - Best Practices** | Consolidated operational recommendations for monitoring, backup, disaster recovery, governance, security, resilience, and cost optimization. |

---

# Module Architecture

```text
                 Azure Resources
                        │
        ┌───────────────┴────────────────┐
        │                                │
        ▼                                ▼
 Azure Monitor                  Azure Backup / ASR
        │                                │
        ▼                                ▼
 Metrics & Logs               Recovery Services Vault
        │                                │
        ▼                                ▼
 Alerts & Analysis            Recovery Points
        │                                │
        └───────────────┬────────────────┘
                        ▼
             Operations & Recovery
                        │
                        ▼
              Business Continuity
```

---

# Core Services Covered

## Monitoring

- Azure Monitor
- Metrics
- Logs
- Log Analytics Workspace
- Azure Monitor Agent (AMA)
- Data Collection Rules (DCR)
- Diagnostic Settings
- Azure Monitor Alerts
- Action Groups
- Azure Service Health
- Azure Resource Health
- Azure Advisor

---

## Backup

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
- Continuous Replication
- Planned Failover
- Unplanned Failover
- Test Failover
- Failback
- Network Mapping

---

## Business Continuity

- Recovery Point Objective (RPO)
- Recovery Time Objective (RTO)
- Restore Validation
- Disaster Recovery Planning
- Business Continuity Strategy

---

## Security & Governance

- Azure RBAC
- Resource Guard
- Multi-User Authorization (MUA)
- Monitoring Governance
- Backup Governance
- Cost Optimization

---

# Operational Lifecycle

```text
Deploy Resources

↓

Configure Monitoring

↓

Collect Telemetry

↓

Detect Issues

↓

Generate Alerts

↓

Investigate

↓

Protect Workloads

↓

Backup & Replication

↓

Recover Services

↓

Review & Improve
```

Monitoring and Business Continuity are continuous operational processes that evolve with the Azure environment.

---

# Design Principles

Microsoft recommends following these principles:

- Centralize monitoring.
- Collect only necessary telemetry.
- Configure Diagnostic Settings early.
- Use Azure Monitor Agent for new deployments.
- Standardize Data Collection Rules.
- Define RPO and RTO before implementing backups.
- Choose Recovery Services Vault redundancy carefully.
- Protect backup infrastructure with least privilege.
- Test restores and failovers regularly.
- Continuously review monitoring effectiveness and recovery procedures.

---

# AZ-104 Exam Focus

This module aligns with the Microsoft AZ-104 objectives related to:

- Azure Monitor
- Log Analytics Workspace
- Azure Monitor Agent
- Data Collection Rules
- Metrics and Logs
- Diagnostic Settings
- Azure Monitor Alerts
- Action Groups
- Azure Service Health
- Azure Resource Health
- Azure Advisor
- Azure Backup
- Recovery Services Vault
- Backup Vault
- Azure Site Recovery
- Backup Policies
- Recovery Points
- Replication
- Planned, Test, and Unplanned Failover
- Failback
- Soft Delete
- Cross Region Restore
- Backup Center
- Resource Guard
- RPO
- RTO

---

# Key Takeaways

- Azure Monitor provides centralized observability through metrics, logs, alerts, and operational insights.
- Azure Backup and Azure Site Recovery work together to protect both data and workload availability.
- Recovery objectives (RPO and RTO), backup policies, and disaster recovery planning should be defined before production deployment.
- Continuous monitoring, regular recovery testing, and strong security controls improve operational resilience.
- Following Microsoft's operational best practices helps organizations build reliable, secure, and recoverable Azure environments.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Monitor | https://learn.microsoft.com/azure/azure-monitor/overview |
| Azure Backup | https://learn.microsoft.com/azure/backup/backup-overview |
| Azure Site Recovery | https://learn.microsoft.com/azure/site-recovery/site-recovery-overview |
| Azure Well-Architected Framework – Reliability | https://learn.microsoft.com/azure/well-architected/reliability/ |
| Azure Well-Architected Framework – Operational Excellence | https://learn.microsoft.com/azure/well-architected/operational-excellence/ |
| Azure Advisor | https://learn.microsoft.com/azure/advisor/advisor-overview |
| Azure Service Health | https://learn.microsoft.com/azure/service-health/overview |
| Azure Resource Health | https://learn.microsoft.com/azure/service-health/resource-health-overview |
| Microsoft Learn – Monitor Azure resources | https://learn.microsoft.com/training/modules/monitor-azure-resources-with-azure-monitor/ |
| Microsoft Learn – Protect Azure resources with Azure Backup | https://learn.microsoft.com/training/modules/protect-vms-with-azure-backup/ |
| Microsoft Learn – Implement disaster recovery with Azure Site Recovery | https://learn.microsoft.com/training/modules/disaster-recovery-site-recovery/ |
