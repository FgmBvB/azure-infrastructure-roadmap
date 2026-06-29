# Azure Virtual Machines Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Virtual Machines (VMs), explains their architecture, deployment options, and core components, and describes their role as Azure's primary Infrastructure as a Service (IaaS) compute offering.

---

## Overview

Azure Virtual Machines (VMs) are Azure's Infrastructure as a Service (IaaS) compute service.

A Virtual Machine provides complete control over the operating system, installed software, networking, and storage, allowing organizations to migrate existing workloads or deploy new applications without managing physical hardware.

Virtual Machines support both Windows and Linux operating systems and can be deployed individually or as part of highly available and scalable architectures.

---

## Learning Objectives

After completing this section you should be able to:

- Understand Azure Virtual Machines.
- Identify the components of a VM.
- Choose the appropriate VM deployment model.
- Understand VM architecture.
- Differentiate compute, storage, and networking components.
- Understand VM lifecycle operations.

---

## Virtual Machine Architecture

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

## Core Components

Every Azure Virtual Machine is composed of several Azure resources.

| Component | Purpose |
|-----------|---------|
| **Virtual Machine** | Compute resource. |
| **Managed Disk** | Operating system and data storage. |
| **Network Interface (NIC)** | Network connectivity. |
| **Virtual Network (VNet)** | Private network communication. |
| **Public IP (Optional)** | Internet connectivity. |
| **Network Security Group (Optional)** | Network traffic filtering. |

---

## Temporary Disk

Many Azure Virtual Machine sizes include a local **Temporary Disk**.

Typical locations are:

- **Windows:** `D:`
- **Linux:** `/mnt` or another temporary mount point depending on the distribution.

Unlike Managed Disks, the Temporary Disk is physically attached to the Azure host server and is **not persistent**.

It is intended for:

- Page files
- Swap files
- Temporary caches
- Scratch data
- Temporary logs

Do **not** store application or business data on the Temporary Disk.

The contents can be lost during operations such as:

- VM redeployment
- VM resizing
- Host maintenance
- VM deallocation

Only Managed Disks provide persistent storage.

---

## Supported Operating Systems

Azure supports both Microsoft and third-party operating systems.

Examples include:

**Windows**

- Windows Server 2025
- Windows Server 2022
- Windows Server 2019

**Linux**

- Ubuntu
- Red Hat Enterprise Linux
- SUSE Linux Enterprise
- Debian
- Oracle Linux
- AlmaLinux
- Rocky Linux

Custom images are also supported.

---

## VM Images

Every Virtual Machine is created from an image.

Common image sources include:

- Azure Marketplace images
- Custom images
- Azure Compute Gallery
- Specialized images
- Generalized images (Sysprep / waagent)

Images simplify standardized deployments across environments.

---

## VM Sizes

Azure provides many VM sizes optimized for different workloads.

Examples include:

| Series | Optimized For |
|---------|---------------|
| **B-series** | Burstable workloads |
| **D-series** | General purpose |
| **E-series** | Memory optimized |
| **F-series** | Compute optimized |
| **M-series** | Large memory workloads |

VM size determines:

- vCPUs
- Memory
- Temporary storage
- Network throughput
- Maximum data disks

---

## Virtual Machine Lifecycle

A Virtual Machine moves through several operational states.

```text
Create
   │
   ▼
Start
   │
   ▼
Running
   │
   ├────────► Restart
   │
   ├────────► Stop
   │
   ▼
Deallocate
   │
   ▼
Delete
```

Understanding the difference between **Stopped** and **Stopped (Deallocated)** is important because compute charges continue while a VM is stopped but not deallocated.

---

## VM Power States

Understanding Azure VM power states is important for both cost management and troubleshooting.

| Power State | Description | Compute Charges |
|-------------|-------------|-----------------|
| **Running** | The VM is running normally. | Yes |
| **Stopped** | The operating system has been shut down from inside the VM, but Azure still reserves the compute resources. | Yes |
| **Stopped (Deallocated)** | The VM has been stopped from Azure (Portal, CLI, PowerShell, or API), releasing the underlying compute resources. | No |

Examples:

Windows:

```powershell
Stop-Computer
```

Linux:

```bash
shutdown -h now
```

Azure CLI:

```bash
az vm deallocate --resource-group <resource-group> --name <vm-name>
```

> [!TIP]
> If a VM is **Deallocated**, Azure releases the underlying compute resources and stops compute billing. Storage charges continue because the managed disks remain allocated.

If the VM uses a **dynamic public IP address**, the IP may change when the VM is started again after being deallocated.

---

## Availability Options

Azure offers several mechanisms to improve availability.

- Availability Zones
- Availability Sets
- Virtual Machine Scale Sets
- Azure Site Recovery
- Azure Backup

These features help reduce downtime and improve resilience.

---

## Common Management Tasks

Administrators commonly perform tasks such as:

- Create VMs
- Resize VMs
- Start and stop VMs
- Restart VMs
- Redeploy VMs
- Capture images
- Attach managed disks
- Configure networking
- Install VM Extensions
- Monitor VM health

---

## Redeploy

The **Redeploy** operation moves a Virtual Machine to a new Azure host while preserving its configuration and Managed Disks.

Redeploy is commonly used to recover from hardware-related issues affecting the underlying Azure host.

During a redeployment:

- Managed OS and Data Disks are preserved.
- Network configuration is retained.
- The VM is restarted on a different physical host.
- The contents of the Temporary Disk are lost.

Redeploy is a useful troubleshooting option when a Virtual Machine experiences unexpected availability or connectivity issues caused by the Azure host infrastructure.

---

## Enterprise Scenario

A company migrates its on-premises Active Directory domain controllers and application servers to Azure Virtual Machines.

Production servers are deployed across multiple Availability Zones, use Premium SSD managed disks, and are protected by Azure Backup.

Network Security Groups restrict inbound traffic, while Azure Monitor collects performance and health metrics.

---

## Best Practices

- Select the appropriate VM size.
- Use Managed Disks.
- Deploy production workloads with high availability.
- Apply the principle of least privilege.
- Enable monitoring and diagnostics.
- Protect VMs with Azure Backup.
- Keep operating systems updated.
- Shut down or deallocate unused VMs to reduce costs.

---

## Common Pitfalls

- Forgetting to deallocate stopped VMs.
- Choosing oversized VM SKUs.
- Exposing RDP or SSH directly to the Internet.
- Ignoring backup configuration.
- Deploying production VMs without high availability.
- Not monitoring VM performance.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - VM architecture
> - VM components
> - VM images
> - VM sizes
> - VM lifecycle
> - Availability options
> - Managed Disks
> - Networking fundamentals

---

## Key Takeaways

- Azure Virtual Machines provide Infrastructure as a Service (IaaS) compute.
- A VM consists of compute, storage, and networking resources.
- VM size determines compute capacity and performance.
- Images enable standardized deployments.
- High availability features improve resilience for production workloads.
- Proper monitoring, backup, and lifecycle management are essential for secure and cost-effective operations.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Azure Virtual Machines documentation](https://learn.microsoft.com/azure/virtual-machines/) | Azure Virtual Machines overview |
| [VM sizes in Azure](https://learn.microsoft.com/azure/virtual-machines/sizes/overview) | Virtual Machine size families |
| [Azure Compute Gallery](https://learn.microsoft.com/azure/virtual-machines/azure-compute-gallery) | Image management |
| [Availability options for Azure Virtual Machines](https://learn.microsoft.com/azure/virtual-machines/availability) | Availability Sets and Availability Zones |
| [Microsoft Learn – Create and manage Azure Virtual Machines](https://learn.microsoft.com/training/modules/create-windows-virtual-machine-in-azure/) | Microsoft Learn module |
