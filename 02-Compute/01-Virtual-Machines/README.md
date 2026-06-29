# Azure Virtual Machines

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Virtual Machines (VMs), including architecture, administration, availability, storage, monitoring, troubleshooting, and Microsoft's recommended operational best practices.

---

## Overview

Azure Virtual Machines (VMs) are Microsoft's primary **Infrastructure as a Service (IaaS)** compute offering.

They provide full control over the operating system, storage, networking, and installed applications, making them suitable for lifting and shifting on-premises workloads, hosting enterprise applications, and building highly available cloud infrastructures.

This section covers the complete lifecycle of Azure Virtual Machines, from deployment and administration to storage, availability, monitoring, and operational best practices.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure Virtual Machine architecture.
- Deploy and administer Virtual Machines.
- Configure storage and availability options.
- Manage VM lifecycle operations.
- Troubleshoot Virtual Machines.
- Optimize performance, security, and cost.
- Apply Microsoft recommended best practices.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | VM architecture, components, images, VM sizes, lifecycle, and core concepts. |
| **02 - Administration** | VM lifecycle management, Resize, Redeploy, Run Command, VM Extensions, Azure VM Agent, Boot Diagnostics, Serial Console, and monitoring tools. |
| **03 - Availability and Storage** | Managed Disks, OS and Data Disks, Temporary Disk, Host Caching, Availability Sets, Availability Zones, and storage redundancy. |
| **04 - Best Practices** | Security, monitoring, backup, availability, cost optimization, operational recommendations, and common deployment mistakes. |

---

## Azure Virtual Machine Architecture

```text
                 Azure Subscription
                        │
                        ▼
                 Resource Group
                        │
                        ▼
                Virtual Machine
      ┌────────────┼────────────┐
      │            │            │
      ▼            ▼            ▼
Operating      Managed      Network
 System         Disks      Interface
      │                         │
      ▼                         ▼
 VM Extensions          Virtual Network
```

---

## Skills Covered

This section includes:

- Azure Virtual Machines
- VM Images
- VM Sizes
- Managed Disks
- OS Disks
- Data Disks
- Temporary Disks
- Host Caching
- Availability Sets
- Availability Zones
- Resize
- Redeploy
- Run Command
- VM Extensions
- Azure VM Agent
- Boot Diagnostics
- Serial Console
- Azure Monitor
- Azure Backup

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Deploy and manage Azure Virtual Machines.
- Configure VM storage.
- Configure high availability.
- Monitor Virtual Machines.
- Troubleshoot VM issues.
- Protect Virtual Machines.
- Optimize VM performance and costs.

---

## Key Takeaways

- Azure Virtual Machines provide flexible Infrastructure as a Service (IaaS) compute.
- VM administration includes lifecycle management, diagnostics, monitoring, and troubleshooting.
- Managed Disks and Availability Zones improve reliability and resilience.
- Azure-native services such as Azure Backup and Azure Monitor simplify production operations.
- Following Microsoft's best practices improves security, availability, operational efficiency, and cost optimization.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Virtual Machines documentation | https://learn.microsoft.com/azure/virtual-machines/ |
| VM sizes in Azure | https://learn.microsoft.com/azure/virtual-machines/sizes/overview |
| Azure Managed Disks | https://learn.microsoft.com/azure/virtual-machines/managed-disks-overview |
| Availability options for Azure Virtual Machines | https://learn.microsoft.com/azure/virtual-machines/availability |
| Azure Monitor documentation | https://learn.microsoft.com/azure/azure-monitor/ |
| Azure Backup documentation | https://learn.microsoft.com/azure/backup/ |
| Microsoft Learn – Create and manage Azure Virtual Machines | https://learn.microsoft.com/training/modules/create-windows-virtual-machine-in-azure/ |
