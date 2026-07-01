# Azure Cloud Shell Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure Cloud Shell, Microsoft's browser-based command-line environment that provides instant access to Azure CLI and Azure PowerShell without requiring local installation.

---

# Overview

Azure Cloud Shell is a browser-accessible command-line environment hosted by Microsoft Azure.

It provides administrators with a fully configured management workstation that includes Azure CLI, Azure PowerShell, and numerous development tools, allowing Azure resources to be managed securely from virtually any device.

Cloud Shell eliminates the need to install local management software while providing automatic authentication and persistent storage for scripts and configuration files.

Azure Cloud Shell is frequently used throughout Microsoft Learn modules and is an important topic for the AZ-104 certification.

---

# Azure Cloud Shell Architecture

```text
Administrator

↓

Web Browser

↓

Azure Cloud Shell

↓

Azure CLI / Azure PowerShell

↓

Azure Resource Manager (ARM)

↓

Azure Resource Providers

↓

Azure Resources
```

Cloud Shell communicates with Azure Resource Manager using the authenticated Azure identity of the current user.

---

# Supported Shells

Azure Cloud Shell supports two environments.

| Shell | Primary Use |
|---------|-------------|
| Bash | Azure CLI, Linux administration, scripting |
| PowerShell | Azure PowerShell, object-oriented automation |

The active shell can be changed at any time.

---

# Built-in Tools

Cloud Shell includes numerous preinstalled tools.

Examples include:

- Azure CLI
- Azure PowerShell
- Git
- Terraform
- Bicep
- kubectl
- Helm
- OpenSSH
- jq
- Vim
- Nano

Microsoft maintains these tools and updates them automatically.

---

# Authentication

Cloud Shell automatically authenticates using the Microsoft Entra account that opened the Azure Portal.

No additional login commands are normally required.

Azure CLI:

```bash
az account show
```

Azure PowerShell:

```powershell
Get-AzContext
```

Administrators can immediately begin managing Azure resources after launching Cloud Shell.

---

# Persistent Storage

Cloud Shell itself is temporary, but user files can persist across sessions.

When Cloud Shell is initialized for the first time, Azure provisions:

- A Storage Account
- An Azure Files share

The Azure Files share is mounted automatically at:

```text
$HOME/clouddrive
```

Typical persistent content includes:

- Scripts
- ARM templates
- Bicep files
- Configuration files
- Downloaded resources

If the associated Storage Account or Azure File Share is deleted, Cloud Shell loses its persistent storage until a new storage location is configured.

---

# Temporary Storage

Not every directory is persistent.

```text
$HOME
```

contains temporary files that may be removed when the Cloud Shell session ends.

Only files stored inside:

```text
$HOME/clouddrive
```

are preserved between sessions.

---

# Resource Management

Cloud Shell supports virtually every Azure administration task.

Examples include:

- Resource Groups
- Virtual Machines
- Networking
- Storage Accounts
- Azure SQL
- Key Vault
- Azure Kubernetes Service (AKS)
- Azure Monitor
- Microsoft Entra ID

---

# File Management

Cloud Shell supports:

- Uploading files
- Downloading files
- Editing files
- Git repositories
- ZIP extraction
- Script execution

Files stored inside **clouddrive** remain available in future sessions.

---

# Cloud Shell and Azure CLI

Cloud Shell includes Azure CLI preinstalled.

Typical scenarios include:

- Resource deployment
- VM administration
- Storage management
- Networking
- Subscription management
- Automation scripts

No installation or updates are required.

---

# Cloud Shell and Azure PowerShell

Cloud Shell also includes Azure PowerShell.

Typical scenarios include:

- Object-oriented scripting
- PowerShell pipelines
- Bulk administration
- Reporting
- Azure automation

The Az module is maintained automatically by Microsoft.

---

# Cloud Shell and ARM

Cloud Shell communicates with Azure Resource Manager regardless of the selected shell.

```text
Azure CLI / Azure PowerShell

↓

Azure Resource Manager

↓

Authentication

↓

Authorization

↓

Resource Providers

↓

Azure Resources
```

---

# Cloud Shell and Bicep

Cloud Shell includes Bicep support.

Administrators can:

- Compile templates
- Deploy Bicep files
- Validate deployments
- Manage Infrastructure as Code

without installing additional software.

---

# Cloud Shell vs Local Environment

| Azure Cloud Shell | Local Environment |
|-------------------|-------------------|
| No installation | Installation required |
| Automatic authentication | Manual authentication |
| Browser-based | Local terminal |
| Microsoft-managed updates | User-managed updates |
| Persistent Azure Files storage | Local storage |
| Available anywhere | Limited to local device |

---

# Automation Scenarios

Azure Cloud Shell is commonly used for:

- Azure administration
- Troubleshooting
- Resource deployment
- Infrastructure as Code
- Learning environments
- Microsoft Learn exercises
- Quick scripting
- Emergency administration

---

# Enterprise Scenario

An administrator is travelling and needs to restore network connectivity for a production Virtual Machine.

Using only a web browser, the administrator:

- Opens the Azure Portal.
- Launches Cloud Shell.
- Automatically authenticates.
- Runs Azure CLI commands.
- Validates the network configuration.
- Restores connectivity.

No local tools or VPN software need to be installed.

---

# Common Pitfalls

- Saving important files outside **$HOME/clouddrive**.
- Deleting the associated Storage Account.
- Assuming all directories are persistent.
- Forgetting to verify the active subscription.
- Assuming Cloud Shell replaces local development environments.
- Ignoring Azure RBAC permissions.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Cloud Shell architecture
> - Bash vs PowerShell
> - Automatic authentication
> - Persistent storage
> - Azure Files integration
> - Azure CLI
> - Azure PowerShell
> - ARM integration
> - Typical administration scenarios

---

# Key Takeaways

- Azure Cloud Shell is a browser-based management environment that provides immediate access to Azure CLI and Azure PowerShell without requiring local installation.
- Authentication is handled automatically using the signed-in Microsoft Entra account, allowing administrators to begin managing Azure resources immediately.
- Persistent storage is provided through an Azure Files share mounted at **$HOME/clouddrive**, while other locations may not persist between sessions.
- Cloud Shell includes a rich set of preinstalled administration and Infrastructure as Code tools such as Azure CLI, Azure PowerShell, Bicep, Terraform, Git, and kubectl.
- Understanding Cloud Shell's architecture, storage model, authentication, and automation capabilities is essential for the AZ-104 certification and day-to-day Azure administration.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Cloud Shell Overview | https://learn.microsoft.com/azure/cloud-shell/overview |
| Azure Cloud Shell Features | https://learn.microsoft.com/azure/cloud-shell/features |
| Azure CLI | https://learn.microsoft.com/cli/azure/ |
| Azure PowerShell | https://learn.microsoft.com/powershell/azure/ |
| Azure Resource Manager | https://learn.microsoft.com/azure/azure-resource-manager/management/overview |
| Azure Files | https://learn.microsoft.com/azure/storage/files/storage-files-introduction |
| Microsoft Learn – Work with Azure Cloud Shell | https://learn.microsoft.com/training/modules/work-azure-cloud-shell/ |
