# Azure Virtual Machines Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for deploying, managing, securing, and optimizing Azure Virtual Machines in production environments.

---

## Overview

Virtual Machines are one of the most widely used Azure compute services.

A well-designed VM deployment improves availability, security, performance, scalability, and cost efficiency while reducing operational risks.

Microsoft recommends combining Virtual Machines with Azure-native services such as Azure Backup, Azure Monitor, Microsoft Defender for Cloud, Azure Policy, and Azure RBAC.

---

## VM Operational Lifecycle

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
Monitor
 │
 ▼
Maintain
 │
 ▼
Protect
 │
 ▼
Optimize
```

---

> [!TIP]
> **Key Concepts**
>
> - Select the correct VM size.
> - Use Managed Disks.
> - Deploy production workloads with high availability.
> - Enable monitoring and backup.
> - Apply the principle of least privilege.
> - Shut down unused resources to reduce costs.

---

## Availability

For production workloads:

- Deploy Virtual Machines across **Availability Zones** whenever supported.
- Use **Availability Sets** only when Availability Zones are unavailable.
- Protect workloads with Azure Backup.
- Design applications to tolerate individual VM failures.
- Use Azure Load Balancer for redundant VM deployments.

---

## Storage

Microsoft recommends:

- Use **Managed Disks** instead of unmanaged disks.
- Choose the appropriate disk performance tier.
- Store application data on dedicated Data Disks.
- Never store production data on the Temporary Disk.
- Select the appropriate host caching policy for the workload.

---

## Security

To improve VM security:

- Restrict RDP and SSH access.
- Use Network Security Groups (NSGs).
- Enable Microsoft Defender for Cloud recommendations.
- Apply Azure RBAC using the principle of least privilege.
- Keep operating systems updated.
- Enable disk encryption where required.
- Protect administrative accounts with Multi-Factor Authentication (MFA).

---

## Cost Optimization

To reduce Azure costs:

- Right-size Virtual Machines based on actual usage.
- Deallocate unused VMs.
- Remove unused Managed Disks.
- Consider Reserved VM Instances for predictable workloads.
- Consider Azure Spot VMs for interruptible workloads.
- Review Azure Advisor recommendations regularly.

---

## Monitoring

Enable monitoring from the beginning of the deployment.

Recommended services include:

- Azure Monitor
- VM Insights
- Activity Log
- Boot Diagnostics
- Metrics
- Log Analytics

Proactive monitoring reduces downtime and simplifies troubleshooting.

---

## Backup and Recovery

Microsoft recommends:

- Enable Azure Backup for production VMs.
- Test restore procedures regularly.
- Define Recovery Point Objectives (RPO) and Recovery Time Objectives (RTO).
- Protect critical workloads using Azure Site Recovery when disaster recovery is required.

---

## Administration

Operational recommendations include:

- Use VM Extensions for automation.
- Use Run Command for short administrative tasks.
- Use Redeploy when troubleshooting Azure host issues.
- Verify the Azure VM Agent is healthy.
- Enable Boot Diagnostics for production workloads.
- Use the Serial Console for startup troubleshooting.

---

## Enterprise Scenario

A financial services company deploys production Virtual Machines across multiple Availability Zones using Premium SSD Managed Disks.

Azure Backup protects all workloads, Azure Monitor collects performance metrics, and Microsoft Defender for Cloud continuously evaluates the security posture.

Network Security Groups restrict administrative access, while Azure RBAC ensures administrators receive only the permissions required for their role.

---

## Best Practices Checklist

- Choose the correct VM size.
- Use Managed Disks.
- Deploy production workloads across Availability Zones.
- Enable Azure Backup.
- Monitor VM health continuously.
- Protect VMs with NSGs and Azure RBAC.
- Enable Boot Diagnostics.
- Keep operating systems updated.
- Deallocate unused Virtual Machines.
- Review Azure Advisor recommendations.

---

## Common Pitfalls

- Leaving stopped VMs allocated.
- Storing important data on the Temporary Disk.
- Exposing RDP or SSH directly to the Internet.
- Deploying production workloads without redundancy.
- Choosing oversized VM SKUs.
- Ignoring monitoring and backup.
- Forgetting to test restore procedures.
- Assuming Availability Sets provide datacenter-level resilience.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - VM sizing
> - Availability recommendations
> - Managed Disks
> - Temporary Disk
> - Azure Backup
> - Azure Monitor
> - Azure VM Agent
> - Redeploy
> - Cost optimization
> - Security best practices

---

## Key Takeaways

- Azure Virtual Machines require proper planning to achieve high availability, security, and cost efficiency.
- Managed Disks, Azure Backup, Azure Monitor, and Availability Zones form the foundation of production-ready VM deployments.
- Regular monitoring, patching, and lifecycle management improve operational reliability.
- Azure-native governance and security services help protect Virtual Machines throughout their lifecycle.
- Following Microsoft's recommended practices reduces operational risk and simplifies long-term administration.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Virtual Machines documentation | https://learn.microsoft.com/azure/virtual-machines/ |
| Availability options for Azure Virtual Machines | https://learn.microsoft.com/azure/virtual-machines/availability |
| Azure Managed Disks | https://learn.microsoft.com/azure/virtual-machines/managed-disks-overview |
| Azure Backup documentation | https://learn.microsoft.com/azure/backup/ |
| Azure Monitor documentation | https://learn.microsoft.com/azure/azure-monitor/ |
| Microsoft Defender for Cloud | https://learn.microsoft.com/azure/defender-for-cloud/ |
| Azure Advisor | https://learn.microsoft.com/azure/advisor/advisor-overview |
| Virtual Machine Scale Sets | https://learn.microsoft.com/azure/virtual-machine-scale-sets/overview |
| Microsoft Learn – Create and manage Azure Virtual Machines | https://learn.microsoft.com/training/modules/create-windows-virtual-machine-in-azure/ |
