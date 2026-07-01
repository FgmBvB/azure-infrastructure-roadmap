# Azure PowerShell Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure PowerShell, Microsoft's PowerShell module for managing Azure resources through Azure Resource Manager (ARM) using object-oriented commands and automation.

---

# Overview

Azure PowerShell is Microsoft's PowerShell module for administering Azure resources.

Built on top of PowerShell, it provides a rich set of cmdlets that interact directly with Azure Resource Manager (ARM), allowing administrators to deploy, configure, automate, and monitor Azure infrastructure.

Unlike Azure CLI, which primarily outputs text and JSON, Azure PowerShell returns **PowerShell objects**, making it especially powerful for scripting and automation within Windows and cross-platform PowerShell environments.

Azure PowerShell is one of the primary automation tools evaluated throughout the AZ-104 certification.

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

Every Azure PowerShell cmdlet communicates with Azure Resource Manager, which authenticates, authorizes, and forwards requests to the appropriate Azure Resource Provider.

---

# Az Module

Azure PowerShell uses the **Az** module.

The Az module replaced the legacy AzureRM module and is the only PowerShell module recommended by Microsoft.

The module contains hundreds of cmdlets grouped into service-specific modules.

Examples include:

- Az.Accounts
- Az.Compute
- Az.Network
- Az.Storage
- Az.Resources
- Az.KeyVault
- Az.Monitor

---

# Installation

Azure PowerShell can be installed on:

- Windows
- Linux
- macOS
- Azure Cloud Shell

Typical installation:

```powershell
Install-Module Az -Scope CurrentUser
```

Update:

```powershell
Update-Module Az
```

Cloud Shell already includes Azure PowerShell.

---

# Authentication

Before executing Azure PowerShell cmdlets, administrators must authenticate.

Common authentication methods include:

- Interactive login
- Service Principal
- Managed Identity
- Azure Cloud Shell

Interactive login:

```powershell
Connect-AzAccount
```

After authentication, Azure PowerShell obtains an Azure AD access token that is reused by subsequent cmdlets.

---

# Subscription Management

Organizations frequently manage multiple Azure subscriptions.

Azure PowerShell provides cmdlets to:

- View subscriptions
- Change the active subscription
- Query subscription information

Examples:

```powershell
Get-AzSubscription

Get-AzContext

Set-AzContext -Subscription "<subscription-name>"
```

Always verify the active subscription before deploying or modifying resources.

---

# Resource Management

Azure PowerShell supports management of virtually every Azure resource.

Examples include:

- Resource Groups
- Virtual Machines
- Virtual Networks
- Storage Accounts
- Key Vault
- Azure SQL
- App Service
- AKS

Administrators can:

- Create resources
- Modify resources
- Delete resources
- Query resources
- Automate deployments

---

# Cmdlet Naming Convention

Azure PowerShell follows PowerShell's standard verb-noun syntax.

Examples:

```powershell
Get-AzVM

New-AzVM

Remove-AzVM

Start-AzVM

Stop-AzVM
```

Most cmdlets follow the pattern:

```text
Verb-AzResource
```

This consistency makes Azure PowerShell predictable and easy to learn.

---

# Object-Oriented Pipeline

Unlike Azure CLI, Azure PowerShell returns objects rather than plain text.

Example:

```powershell
Get-AzVM | Select-Object Name, Location
```

Objects can be:

- Filtered
- Sorted
- Grouped
- Exported
- Passed through the pipeline

This is one of the major strengths of PowerShell automation.

---

# Filtering Objects

Azure PowerShell integrates with the PowerShell pipeline.

Examples:

```powershell
Get-AzVM |
Where-Object {$_.Location -eq "East US"}
```

```powershell
Get-AzVM |
Sort-Object Name
```

```powershell
Get-AzVM |
Select-Object Name, ResourceGroupName
```

No external parsing language is required.

---

# Azure PowerShell and ARM

Azure PowerShell communicates with Azure Resource Manager.

```text
Azure PowerShell

↓

Azure Resource Manager

↓

Authentication

↓

Authorization

↓

Resource Provider

↓

Azure Resource
```

This ensures consistent deployment behavior across Azure services.

---

# Azure PowerShell vs Azure CLI

| Azure PowerShell | Azure CLI |
|------------------|-----------|
| Object-oriented | Text/JSON-oriented |
| PowerShell pipeline | JMESPath queries |
| Cmdlets | Commands |
| Verb-Noun syntax | az group resource command |
| Best for PowerShell environments | Best for Bash environments |

Both tools provide equivalent Azure management capabilities.

---

# Azure PowerShell and Cloud Shell

Azure Cloud Shell includes Azure PowerShell by default.

Benefits include:

- No installation required.
- Automatic authentication.
- Persistent storage.
- Browser-based administration.
- Always updated.

---

# Automation Scenarios

Azure PowerShell is commonly used for:

- Infrastructure deployment
- Resource provisioning
- VM lifecycle management
- RBAC assignments
- Scheduled administration
- Bulk resource updates
- Reporting
- CI/CD pipelines

It is particularly effective when automation requires complex object manipulation.

---

# Enterprise Scenario

An enterprise manages hundreds of Azure Virtual Machines.

Administrators use Azure PowerShell to:

- Retrieve VM inventories.
- Filter VMs by location.
- Start or stop VMs in bulk.
- Configure networking.
- Assign RBAC roles.
- Generate operational reports.

Using PowerShell objects simplifies large-scale administration and reporting.

---

# Common Pitfalls

- Forgetting to authenticate.
- Executing commands in the wrong subscription.
- Mixing Azure CLI commands with PowerShell cmdlets.
- Ignoring the active context.
- Using deprecated AzureRM cmdlets.
- Hardcoding credentials.
- Not handling cmdlet errors.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure PowerShell architecture
> - Az module
> - Authentication
> - Subscription management
> - Cmdlet naming convention
> - Object pipeline
> - Azure PowerShell vs Azure CLI
> - Azure Cloud Shell integration
> - Automation scenarios

---

# Key Takeaways

- Azure PowerShell is Microsoft's object-oriented automation framework for administering Azure through Azure Resource Manager.
- The Az module provides a consistent set of cmdlets that follow PowerShell's standard verb-noun naming convention.
- Returning PowerShell objects instead of text enables powerful filtering, reporting, and automation through the native PowerShell pipeline.
- Azure PowerShell integrates seamlessly with Azure Cloud Shell, CI/CD platforms, and Azure services, making it a core tool for enterprise automation.
- Understanding authentication, contexts, object handling, and the Az module is essential for both Azure administration and the AZ-104 certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure PowerShell documentation | https://learn.microsoft.com/powershell/azure/ |
| Install Azure PowerShell | https://learn.microsoft.com/powershell/azure/install-az-ps |
| Az module reference | https://learn.microsoft.com/powershell/module/az/ |
| Azure Cloud Shell | https://learn.microsoft.com/azure/cloud-shell/overview |
| Azure Resource Manager | https://learn.microsoft.com/azure/azure-resource-manager/management/overview |
| Microsoft Learn – Introduction to Azure PowerShell | https://learn.microsoft.com/training/modules/automate-azure-tasks-with-powershell/ |
