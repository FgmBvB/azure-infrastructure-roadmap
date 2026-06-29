# Azure VM Availability and Storage

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It explains how Azure Virtual Machines achieve high availability and how Azure Managed Disks provide durable and scalable storage for VM workloads.

---

## Overview

Azure Virtual Machines combine compute resources with highly durable managed storage and multiple high-availability options.

Choosing the appropriate availability architecture and storage performance tier is essential for building resilient, cost-effective, and highly available workloads.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure Managed Disks.
- Differentiate OS and Data Disks.
- Understand disk performance tiers.
- Compare Availability Sets and Availability Zones.
- Understand VM Scale Sets at a high level.
- Select the appropriate availability option.

---

## Availability Architecture

```text
                 Azure Region
                      │
        ┌─────────────┴─────────────┐
        │                           │
        ▼                           ▼
Availability Zone 1         Availability Zone 2
        │                           │
        ▼                           ▼
     Virtual Machine          Virtual Machine
        │                           │
        └─────────────┬─────────────┘
                      ▼
                Managed Disks
```

---

## Managed Disks

Azure Managed Disks provide persistent storage for Virtual Machines.

Azure manages:

- Storage accounts
- Availability
- Scalability
- Redundancy
- Performance

Managed Disks simplify storage management compared to unmanaged disks.

---

## Host Caching

Managed Disks support host caching to improve storage performance.

| Cache Mode | Description | Typical Use |
|------------|-------------|-------------|
| **ReadOnly** | Frequently accessed data is cached for read operations. | OS Disks and read-intensive workloads |
| **ReadWrite** | Read and write operations are cached. | General-purpose workloads where supported |
| **None** | All operations go directly to Managed Storage. | Write-intensive databases and transaction logs |

Selecting the appropriate caching mode improves storage performance while maintaining application reliability.

> [!IMPORTANT]
> Microsoft generally recommends using **None** for transaction logs and write-intensive database workloads to avoid data consistency issues.

---

## Disk Types

Azure offers several Managed Disk types.

| Disk Type | Typical Workload |
|-----------|------------------|
| **Standard HDD** | Backup, archive, low-cost workloads |
| **Standard SSD** | Development, testing, web servers |
| **Premium SSD** | Production applications and databases |
| **Premium SSD v2** | Performance-sensitive transactional workloads |
| **Ultra Disk** | High-performance databases requiring extremely low latency |

---

## Ephemeral OS Disks

An **Ephemeral OS Disk** stores the operating system locally on the Azure host instead of using a remote Managed Disk.

Benefits include:

- Faster provisioning
- Lower latency
- No Managed Disk storage cost
- Faster VM reimaging

Ephemeral OS Disks are well suited for stateless workloads such as:

- Virtual Machine Scale Sets
- AKS worker nodes
- Build agents
- Temporary application servers

Limitations include:

- The operating system disk is recreated if the VM is redeployed or deallocated.
- Not supported on every VM size.
- Not suitable for workloads requiring persistent operating system storage.

Applications requiring persistent data should continue using Managed Disks.

---

## OS Disk vs Data Disk

A Virtual Machine typically uses two types of persistent disks.

| Disk | Purpose |
|------|---------|
| **OS Disk** | Contains the operating system and boot files. |
| **Data Disk** | Stores application data, databases, and user files. |

Data Disks can be attached or detached independently of the operating system.

---

## Temporary Disk

Many Azure Virtual Machine sizes include a local **Temporary Disk**.

Typical locations include:

- **Windows:** `D:`
- **Linux:** `/mnt`

Unlike Managed Disks, the Temporary Disk is physically attached to the Azure host and is **not persistent**.

Typical uses include:

- Page files
- Swap files
- Temporary caches
- Scratch data

Data stored on the Temporary Disk may be lost during:

- Redeployment
- VM resize
- Host maintenance
- VM deallocation

Critical application data should never be stored on the Temporary Disk.

---

## Availability Sets

Availability Sets improve availability by distributing Virtual Machines across different physical hardware.

Azure uses two concepts:

| Component | Purpose |
|-----------|---------|
| **Fault Domains** | Protect against hardware failures such as power or rack failures. |
| **Update Domains** | Ensure planned maintenance affects only a subset of VMs at a time. |

Availability Sets are intended for Virtual Machines located within a single Azure datacenter.

---

## Availability Set Limits

Availability Sets distribute Virtual Machines across **Fault Domains** and **Update Domains** to improve availability.

### Fault Domains

A Fault Domain represents a group of hardware that shares common infrastructure, such as:

- Power source
- Network switch
- Physical rack

Depending on the Azure region, an Availability Set supports **2 or 3 Fault Domains**.

---

### Update Domains

An Update Domain represents a logical group of Virtual Machines that can be restarted together during planned Azure maintenance.

Characteristics:

- Default: **5 Update Domains**
- Maximum: **20 Update Domains**

Azure updates one Update Domain at a time, reducing the impact of planned maintenance.

> [!TIP]
> Availability Sets reduce the impact of both planned maintenance and unexpected hardware failures, but they do not protect against an entire datacenter outage. For that level of resilience, use **Availability Zones**.

## Availability Zones

Availability Zones provide higher availability by placing Virtual Machines in physically separate datacenters within the same Azure region.

Benefits include:

- Independent power
- Independent cooling
- Independent networking
- Protection against datacenter failures

Availability Zones provide greater resilience than Availability Sets.

---

## Availability Sets vs Availability Zones

| Availability Sets | Availability Zones |
|-------------------|--------------------|
| Same datacenter | Separate datacenters |
| Fault Domains and Update Domains | Physical isolation |
| Protect against host failures | Protect against datacenter failures |
| Lower availability | Higher availability |

---

## Managed Disk Redundancy

Azure provides multiple redundancy options for Managed Disks.

| Redundancy | Description |
|------------|-------------|
| **LRS** | Locally Redundant Storage within a single datacenter. |
| **ZRS** | Zone-Redundant Storage across multiple Availability Zones. |

The available redundancy options depend on the Azure region and disk type.

---

## Enterprise Scenario

A company deploys two production web servers across separate Availability Zones.

Each VM uses Premium SSD Managed Disks protected by Zone-Redundant Storage.

Azure Load Balancer distributes traffic between both VMs, providing resilience against both hardware failures and datacenter outages.

---

## Best Practices

- Use Managed Disks instead of unmanaged disks.
- Select the appropriate disk performance tier.
- Use Premium SSD for production workloads.
- Store application data on Data Disks rather than the OS Disk.
- Never store critical data on the Temporary Disk.
- Deploy production workloads using Availability Zones whenever supported.
- Use Availability Sets only when Availability Zones are unavailable.

---

## Common Pitfalls

- Confusing Temporary Disks with Managed Disks.
- Storing production data on the Temporary Disk.
- Deploying critical workloads on a single VM.
- Selecting oversized disk performance tiers.
- Confusing Availability Sets with Availability Zones.
- Assuming every Azure region supports Availability Zones.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Managed Disks
> - OS Disk vs Data Disk
> - Temporary Disk
> - Disk performance tiers
> - Availability Sets
> - Fault Domains
> - Update Domains
> - Availability Zones
> - Managed Disk redundancy

---

## Key Takeaways

- Managed Disks provide durable and scalable storage for Azure Virtual Machines.
- OS Disks and Data Disks are persistent, while the Temporary Disk is not.
- Availability Sets protect against host-level failures within a datacenter.
- Availability Zones protect against datacenter-level failures within a region.
- Selecting the appropriate storage and availability architecture improves reliability, performance, and operational resilience.

---

## References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Managed Disks | https://learn.microsoft.com/azure/virtual-machines/managed-disks-overview |
| Managed Disk types | https://learn.microsoft.com/azure/virtual-machines/disks-types |
| Availability options for Azure Virtual Machines | https://learn.microsoft.com/azure/virtual-machines/availability |
| Availability Zones | https://learn.microsoft.com/azure/reliability/availability-zones-overview |
| Availability Sets | https://learn.microsoft.com/azure/virtual-machines/availability-set-overview |
| Microsoft Learn – Create and manage Azure Virtual Machines | https://learn.microsoft.com/training/modules/create-windows-virtual-machine-in-azure/ |
