# Azure PowerShell

> [!NOTE]
> This section is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure PowerShell, Microsoft's object-oriented automation framework for managing Azure resources through Azure Resource Manager (ARM) using the **Az** module and native PowerShell capabilities.

---

# Overview

Azure PowerShell provides a comprehensive set of PowerShell cmdlets for provisioning, configuring, automating, and managing Azure resources.

Built on top of the PowerShell ecosystem, it combines Azure Resource Manager integration with object-oriented scripting, making it particularly well suited for enterprise automation, bulk administration, and Infrastructure as Code workflows.

Unlike Azure CLI, Azure PowerShell returns PowerShell objects instead of plain text, allowing administrators to leverage the native pipeline, filtering, sorting, formatting, and scripting capabilities of PowerShell.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure PowerShell architecture.
- Understand the Az module.
- Authenticate securely.
- Manage Azure contexts and subscriptions.
- Execute Azure PowerShell cmdlets.
- Understand PowerShell object pipelines.
- Filter and manipulate PowerShell objects.
- Perform Azure automation using PowerShell.
- Manage long-running operations.
- Use Azure Cloud Shell with Azure PowerShell.
- Apply Microsoft's Azure PowerShell best practices.

---

# Section Structure

| Document | Description |
|----------|-------------|
| **01 - Overview** | Azure PowerShell architecture, Az module, authentication, Azure Context, subscription management, cmdlet syntax, object-oriented pipeline, ARM integration, Cloud Shell, automation scenarios, background jobs, and AZ-104 concepts. |
| **02 - Best Practices** | Secure authentication, Azure Context management, pipeline usage, named parameters, PowerShell Splatting, error handling, background jobs, long-running operations, Cloud Shell usage, source control, module management, and Microsoft's production recommendations. |

---

# Azure PowerShell Architecture

```text
Administrator

↓

Azure PowerShell

↓

Az Module

↓

Azure Resource Manager (ARM)

↓

Azure Resource Providers

↓

Azure Resources
```

Azure PowerShell communicates directly with Azure Resource Manager, which authenticates, authorizes, and forwards requests to the appropriate Azure Resource Provider.

---

# Core Capabilities

This section covers the primary Azure PowerShell capabilities.

## Administration

- Resource management
- Subscription management
- Resource Groups
- Virtual Machines
- Networking
- Storage
- Identity
- Monitoring

---

## Automation

- PowerShell scripting
- Object-oriented pipeline
- Bulk administration
- Scheduled tasks
- CI/CD pipelines
- Azure DevOps integration

---

## Object Processing

- PowerShell objects
- Filtering
- Sorting
- Formatting
- Pipeline processing
- Object selection

---

## Cloud Integration

- Azure Cloud Shell
- Azure Resource Manager
- Managed Identities
- Service Principals
- Azure Key Vault integration

---

# Typical Workflow

```text
Authenticate

↓

Select Azure Context

↓

Execute Cmdlets

↓

Process Objects

↓

Deploy or Modify Resources

↓

Validate Results

↓

Automation
```

Azure PowerShell enables administrators to automate the complete lifecycle of Azure resources using native PowerShell scripting.

---

# Design Principles

Microsoft recommends following these principles:

- Use secure authentication methods.
- Verify the active Azure Context before making changes.
- Prefer object pipelines over manual data processing.
- Parameterize scripts for reusability.
- Use PowerShell Splatting for complex cmdlets.
- Implement robust error handling.
- Protect secrets using Azure Key Vault.
- Use background jobs for long-running operations.
- Store scripts in version control.
- Keep the Az module updated.

---

# AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Azure PowerShell
- Az module
- Authentication
- Azure Context
- Subscription management
- Cmdlet syntax
- PowerShell pipeline
- Object processing
- Azure Cloud Shell
- Background jobs
- Automation best practices

---

# Key Takeaways

- Azure PowerShell is Microsoft's object-oriented automation framework for administering Azure through Azure Resource Manager.
- The Az module provides a modern and consistent set of cmdlets that integrate seamlessly with the native PowerShell pipeline.
- Azure Contexts, object processing, background jobs, and robust error handling enable secure and scalable automation across multiple Azure environments.
- Azure PowerShell integrates with Azure Cloud Shell, Azure DevOps, GitHub Actions, and other automation platforms, making it a core tool for enterprise administration.
- Mastering Azure PowerShell is an essential skill for Azure administrators and a key objective of the AZ-104 certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure PowerShell documentation | https://learn.microsoft.com/powershell/azure/ |
| Az module reference | https://learn.microsoft.com/powershell/module/az/ |
| Install Azure PowerShell | https://learn.microsoft.com/powershell/azure/install-az-ps |
| Azure Cloud Shell | https://learn.microsoft.com/azure/cloud-shell/overview |
| Azure Resource Manager | https://learn.microsoft.com/azure/azure-resource-manager/management/overview |
| Microsoft Learn – Automate Azure tasks with PowerShell | https://learn.microsoft.com/training/modules/automate-azure-tasks-with-powershell/ |
