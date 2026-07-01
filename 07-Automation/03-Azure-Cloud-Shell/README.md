# Azure Cloud Shell

> [!NOTE]
> This section is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure Cloud Shell, Microsoft's browser-based administration environment that provides instant access to Azure CLI and Azure PowerShell without requiring local installation.

---

# Overview

Azure Cloud Shell is a Microsoft-managed command-line environment that allows administrators to manage Azure resources directly from a web browser.

It provides a fully configured administration workstation with Azure CLI, Azure PowerShell, Infrastructure as Code tools, and development utilities already installed and maintained by Microsoft.

Cloud Shell eliminates the need to install local management software while providing secure authentication, persistent storage, and seamless integration with Azure Resource Manager.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure Cloud Shell architecture.
- Understand supported shells.
- Authenticate automatically.
- Understand persistent and temporary storage.
- Manage Azure resources using Azure CLI.
- Manage Azure resources using Azure PowerShell.
- Understand Azure Files integration.
- Understand Cloud Shell session lifecycle.
- Reconfigure Cloud Shell storage.
- Apply Cloud Shell operational best practices.

---

# Section Structure

| Document | Description |
|----------|-------------|
| **01 - Overview** | Cloud Shell architecture, supported shells, authentication, Azure Files integration, persistent storage, temporary storage, built-in tools, Azure CLI, Azure PowerShell, ARM integration, session lifecycle, storage infrastructure, and AZ-104 concepts. |
| **02 - Best Practices** | Persistent storage management, subscription verification, Git integration, secure administration, Cloud Shell storage management, session handling, long-running tasks, Azure Files usage, operational recommendations, and Microsoft's production best practices. |

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

Cloud Shell provides a Microsoft-managed administration environment that communicates directly with Azure Resource Manager using the authenticated Microsoft Entra identity of the current user.

---

# Core Capabilities

This section covers the primary Azure Cloud Shell capabilities.

## Administration

- Azure CLI
- Azure PowerShell
- Resource management
- Subscription management
- Azure Resource Manager integration

---

## Built-in Tools

Cloud Shell includes Microsoft-maintained tools such as:

- Azure CLI
- Azure PowerShell
- Git
- Bicep
- Terraform
- kubectl
- Helm
- OpenSSH
- jq
- Vim
- Nano

---

## Persistent Storage

Cloud Shell provides persistent storage through Azure Files.

Persistent data includes:

- Scripts
- Templates
- Configuration files
- Git repositories
- Deployment artifacts

---

## Infrastructure as Code

Cloud Shell supports:

- ARM Templates
- Bicep
- Terraform

without requiring additional installation.

---

# Typical Workflow

```text
Open Azure Portal

↓

Launch Cloud Shell

↓

Automatic Authentication

↓

Select Bash or PowerShell

↓

Execute Commands

↓

Deploy or Manage Resources

↓

Save Files to clouddrive
```

Cloud Shell provides immediate access to Azure administration from any supported web browser.

---

# Design Principles

Microsoft recommends following these principles:

- Store important files inside **$HOME/clouddrive**.
- Verify the active subscription before making changes.
- Protect secrets using Azure Key Vault.
- Keep automation scripts in source control.
- Use the appropriate shell for each task.
- Understand the difference between temporary and persistent storage.
- Use Cloud Shell primarily for administration and operational tasks.
- Regularly review Azure Files storage usage.

---

# AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Azure Cloud Shell
- Azure CLI
- Azure PowerShell
- Automatic authentication
- Azure Files
- Persistent storage
- Session lifecycle
- Built-in administration tools
- Azure Resource Manager integration
- Cloud Shell best practices

---

# Key Takeaways

- Azure Cloud Shell is a Microsoft-managed browser-based administration environment that provides immediate access to Azure CLI and Azure PowerShell.
- Authentication is handled automatically through the signed-in Microsoft Entra account, allowing administrators to manage Azure resources without additional configuration.
- Persistent storage is backed by Azure Files through the **$HOME/clouddrive** directory, while other locations should be treated as temporary.
- Cloud Shell includes a comprehensive collection of preinstalled administration and Infrastructure as Code tools, making it ideal for day-to-day Azure operations.
- Understanding Cloud Shell's architecture, storage model, session lifecycle, and operational best practices is an important objective of the AZ-104 certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Cloud Shell Overview | https://learn.microsoft.com/azure/cloud-shell/overview |
| Azure Cloud Shell Features | https://learn.microsoft.com/azure/cloud-shell/features |
| Azure CLI | https://learn.microsoft.com/cli/azure/ |
| Azure PowerShell | https://learn.microsoft.com/powershell/azure/ |
| Azure Files | https://learn.microsoft.com/azure/storage/files/storage-files-introduction |
| Azure Resource Manager | https://learn.microsoft.com/azure/azure-resource-manager/management/overview |
| Microsoft Learn – Work with Azure Cloud Shell | https://learn.microsoft.com/training/modules/work-azure-cloud-shell/ |
