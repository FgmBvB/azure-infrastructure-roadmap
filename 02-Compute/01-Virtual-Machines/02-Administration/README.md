# Azure Virtual Machine Administration

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers the day-to-day administration of Azure Virtual Machines, including lifecycle operations, management tools, diagnostics, extensions, and troubleshooting.

---

## Overview

Managing Azure Virtual Machines involves much more than creating and deleting VMs.

Azure provides numerous administrative tools that allow administrators to monitor, troubleshoot, maintain, and automate Virtual Machines throughout their lifecycle.

Understanding these tools is essential for operating production workloads efficiently.

---

## Learning Objectives

After completing this section you should be able to:

- Perform common VM administrative tasks.
- Understand VM lifecycle operations.
- Manage VM Extensions.
- Use Run Command.
- Configure Boot Diagnostics.
- Access the Serial Console.
- Redeploy and Resize Virtual Machines.
- Troubleshoot common VM issues.

---

## Administration Workflow

```text
Create VM
    │
    ▼
Configure
    │
    ▼
Monitor
    │
    ▼
Maintain
    │
    ▼
Troubleshoot
    │
    ▼
Update
    │
    ▼
Retire
```

---

## Common Administrative Tasks

Azure administrators commonly perform:

- Create Virtual Machines
- Start and Stop VMs
- Restart VMs
- Deallocate VMs
- Resize VMs
- Redeploy VMs
- Capture VM Images
- Attach or Detach Managed Disks
- Configure Networking
- Install VM Extensions
- Monitor VM Health

---

## Resize Virtual Machines

Virtual Machines can be resized to increase or decrease compute capacity.

Changing the VM size modifies:

- vCPUs
- Memory
- Network bandwidth
- Temporary disk capacity

Some resize operations require the VM to be restarted.

If the requested size is unavailable on the current hardware cluster, Azure may require the VM to be deallocated before resizing.

---

## Resize Constraints

When a Virtual Machine is running, it is allocated to a specific Azure host.

Not every host supports every VM size or hardware generation.

If the requested VM size is unavailable on the current host, Azure may return an allocation error during the resize operation.

In these situations, administrators should:

1. Deallocate the Virtual Machine.
2. Change the VM size.
3. Start the Virtual Machine again.

After deallocation, Azure is free to place the VM on another host that supports the requested VM size.

> [!TIP]
> Deallocating a VM releases the underlying compute resources, allowing Azure to select a different physical host during the next startup.

---

## Redeploy

The **Redeploy** operation moves a Virtual Machine to a new Azure host while preserving its Managed Disks and configuration.

Redeploy is commonly used when troubleshooting issues related to the underlying Azure host.

During a redeployment:

- OS and Data Disks are preserved.
- Network configuration remains unchanged.
- The VM starts on a different physical host.
- The contents of the Temporary Disk are lost.

---

## Run Command

Run Command allows administrators to execute scripts inside a Virtual Machine without opening RDP or SSH connections.

Typical use cases include:

- Reset configuration
- Run PowerShell scripts
- Execute Bash commands
- Collect diagnostic information
- Repair startup issues

This feature communicates with the Azure VM Agent.

---

## Run Command vs Custom Script Extension

Although both features execute scripts inside a Virtual Machine, they are designed for different purposes.

| Feature | Run Command | Custom Script Extension |
|----------|-------------|-------------------------|
| Typical use | Troubleshooting and quick administration | Post-deployment configuration |
| Execution | Immediate | During or after deployment |
| Script source | Sent through Azure API | Azure Storage, GitHub, or other supported locations |
| Requires VM Agent | Yes | Yes |
| Typical scenarios | Diagnostics, configuration changes | Software installation, configuration automation |

Microsoft recommends:

- Use **Run Command** for short-lived administrative or troubleshooting tasks.
- Use **Custom Script Extension** for deployment automation and post-deployment configuration.

Neither feature should be used for long-running configuration management solutions.

---

## VM Extensions

VM Extensions provide post-deployment configuration and automation.

Common extensions include:

| Extension | Purpose |
|-----------|---------|
| Custom Script Extension | Execute scripts after deployment |
| Azure Monitor Agent | Collect monitoring data |
| Microsoft Antimalware | Malware protection (Windows) |
| Desired State Configuration (DSC) | Configuration management |
| Dependency Agent | Dependency mapping |

Extensions simplify software installation and operational management.

---

## Boot Diagnostics

Boot Diagnostics captures screenshots and serial log information during VM startup.

It is useful when:

- The operating system fails to boot.
- Remote access is unavailable.
- Startup configuration is corrupted.

Boot Diagnostics stores diagnostic data in an Azure Storage Account or managed storage.

---

## Serial Console

Azure Serial Console provides low-level access to a Virtual Machine through the Azure portal.

Typical scenarios include:

- Repair boot failures.
- Modify firewall settings.
- Recover from incorrect network configuration.
- Troubleshoot startup problems.

Serial Console works even when standard network connectivity is unavailable.

---

## Azure VM Agent

The Azure VM Agent enables communication between Azure and the guest operating system.

It is required for several Azure features, including:

- VM Extensions
- Run Command
- Azure Backup
- Guest configuration
- Some monitoring capabilities

Many management operations depend on a healthy VM Agent.

---

## Azure VM Agent Requirements

The Azure VM Agent enables communication between Azure and the guest operating system.

Marketplace images include the Azure VM Agent by default.

If a Virtual Machine is created from a custom image, administrators should verify that the VM Agent is installed and functioning correctly.

If the Azure VM Agent becomes unavailable:

- VM Extensions cannot be installed or updated.
- Run Command is unavailable.
- Some Azure Backup operations may fail.
- Certain guest management features stop functioning.

The Virtual Machine itself continues running normally, but Azure loses the ability to perform several management operations inside the guest operating system.

---

## Monitoring VM Health

Azure provides several monitoring tools.

Common monitoring services include:

- Azure Monitor
- Activity Log
- Metrics
- Diagnostic Logs
- Boot Diagnostics
- Azure Advisor

These services help identify performance issues and operational problems.

---

## Enterprise Scenario

An administrator receives reports that a production Virtual Machine is no longer responding over RDP.

Using Boot Diagnostics, they discover the operating system is failing during startup.

The administrator accesses the Serial Console to repair the configuration, then uses Redeploy to move the VM to a healthy Azure host.

Azure Monitor confirms the VM returns to normal operation.

---

## Best Practices

- Enable Boot Diagnostics.
- Keep the Azure VM Agent healthy.
- Use VM Extensions instead of manual software installation.
- Monitor VM performance continuously.
- Redeploy only when troubleshooting host-related issues.
- Resize VMs according to workload requirements.
- Deallocate unused VMs to reduce costs.

---

## Common Pitfalls

- Confusing Stop with Deallocate.
- Forgetting that Redeploy clears the Temporary Disk.
- Disabling or removing the Azure VM Agent.
- Installing unnecessary VM Extensions.
- Ignoring Boot Diagnostics during startup failures.
- Resizing without verifying SKU availability.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - VM lifecycle operations
> - Resize
> - Redeploy
> - Run Command
> - VM Extensions
> - Azure VM Agent
> - Boot Diagnostics
> - Serial Console
> - Monitoring tools

---

## Key Takeaways

- Azure provides multiple tools for managing Virtual Machines throughout their lifecycle.
- Run Command and VM Extensions simplify remote administration.
- Boot Diagnostics and Serial Console are essential troubleshooting tools.
- Redeploy resolves issues related to the underlying Azure host while preserving Managed Disks.
- Effective monitoring and proactive maintenance improve VM reliability and availability.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| https://learn.microsoft.com/azure/virtual-machines/ | Azure Virtual Machines documentation |
| https://learn.microsoft.com/azure/virtual-machines/extensions/overview | VM Extensions |
| https://learn.microsoft.com/azure/virtual-machines/run-command | Run Command |
| https://learn.microsoft.com/azure/virtual-machines/boot-diagnostics | Boot Diagnostics |
| https://learn.microsoft.com/azure/virtual-machines/troubleshooting/serial-console-overview | Azure Serial Console |
| https://learn.microsoft.com/training/modules/create-windows-virtual-machine-in-azure/ | Microsoft Learn module |
