# Azure CLI Overview

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It introduces Azure CLI, Microsoft's cross-platform command-line interface for deploying, configuring, automating, and managing Azure resources from the terminal.

---

# Overview

Azure CLI is Microsoft's command-line tool for managing Azure resources.

It provides a consistent, scriptable interface that allows administrators to perform virtually every management operation available through the Azure Portal, Azure PowerShell, and Azure REST APIs.

Azure CLI is:

- Cross-platform
- Open source
- Script-friendly
- Automation-ready
- Fully integrated with Azure Resource Manager (ARM)

It is one of the primary automation tools evaluated throughout the AZ-104 certification.

---

# Azure CLI Architecture

```text
Administrator

↓

Azure CLI

↓

Azure Resource Manager (ARM)

↓

Azure Resource Providers

↓

Azure Resources
```

Every Azure CLI command communicates with Azure Resource Manager, which authenticates, authorizes, and forwards requests to the appropriate Azure Resource Provider.

---

# Installation Options

Azure CLI can be used from multiple environments.

Supported options include:

- Windows
- Linux
- macOS
- Azure Cloud Shell
- Docker Containers
- GitHub Actions
- Azure DevOps Pipelines

Cloud Shell already includes Azure CLI preinstalled.

---

# Authentication

Before managing Azure resources, Azure CLI must authenticate against Azure.

The most common authentication methods are:

- Interactive user login
- Service Principal
- Managed Identity
- Azure Cloud Shell (automatic authentication)

Typical login command:

```bash
az login
```

After authentication, Azure CLI obtains an Azure Active Directory access token used for subsequent operations.

---

# Subscription Management

Many organizations manage multiple Azure subscriptions.

Azure CLI allows administrators to:

- View subscriptions
- Change active subscriptions
- Query subscription information
- Automate multi-subscription deployments

Common commands include:

```bash
az account list

az account show

az account set --subscription "<subscription-name>"
```

Always verify the active subscription before deploying resources.

---

# Resource Management

Azure CLI supports every major Azure resource.

Examples include:

- Resource Groups
- Virtual Machines
- Virtual Networks
- Storage Accounts
- Key Vault
- Azure SQL
- App Service
- Azure Kubernetes Service (AKS)

Resources can be:

- Created
- Updated
- Deleted
- Queried
- Exported

using a consistent command structure.

---

# Command Structure

Azure CLI commands follow a predictable syntax.

```text
az

↓

Resource Group

↓

Resource Type

↓

Operation

↓

Parameters
```

Example:

```bash
az vm create
```

General format:

```bash
az <group> <resource> <command> [parameters]
```

This consistent structure makes Azure CLI easy to learn and automate.

---

# Output Formats

Azure CLI supports multiple output formats.

| Format | Description |
|----------|-------------|
| json | Default structured output |
| table | Human-readable table |
| tsv | Tab-separated values |
| yaml | YAML output |
| none | Suppress output |

Example:

```bash
az vm list --output table
```

Choosing the appropriate output format simplifies scripting and reporting.

---

# Querying Results

Azure CLI supports **JMESPath** queries for filtering command output.

Example:

```bash
az vm list --query "[].name"
```

Benefits include:

- Reduce output size.
- Extract specific properties.
- Simplify automation.
- Build reusable scripts.

JMESPath is widely used in Azure automation scenarios.

---

# Advanced JMESPath Queries

Azure CLI supports advanced **JMESPath** expressions for filtering, transforming, and formatting command output.

### Conditional Filtering

Return only resources that match a specific condition.

Example:

```bash
az storage account list \
  --query "[?kind=='StorageV2'].name"
```

---

### Custom Projections

Create simplified output with custom property names.

Example:

```bash
az vm list \
  --query "[].{VM:name, ResourceGroup:resourceGroup, Size:hardwareProfile.vmSize}"
```

Benefits include:

- Smaller output
- Easier scripting
- Better reporting
- Cleaner automation

> [!TIP]
> Advanced JMESPath queries reduce the need for external parsing tools in automation scripts.

---

# Azure CLI and ARM

Azure CLI is a management client for Azure Resource Manager.

When a command executes:

```text
Azure CLI

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

This architecture ensures consistent behavior across Azure services.

---

# Azure CLI vs Azure PowerShell

| Azure CLI | Azure PowerShell |
|------------|------------------|
| Cross-platform | Cross-platform |
| Bash-friendly | PowerShell-oriented |
| Text/JSON output | Object-based output |
| JMESPath queries | PowerShell pipeline |
| Preferred in Linux environments | Preferred in PowerShell environments |

Both tools provide full Azure management capabilities.

---

# Azure CLI and Cloud Shell

Azure Cloud Shell includes Azure CLI by default.

Benefits include:

- No installation required.
- Automatic authentication.
- Persistent storage.
- Browser-based access.
- Always updated.

Cloud Shell is frequently used in Microsoft Learn exercises and Azure documentation.

---

# Automation Scenarios

Azure CLI is commonly used for:

- Infrastructure deployment
- Resource provisioning
- Automation scripts
- CI/CD pipelines
- Scheduled maintenance
- Bulk resource management
- Inventory reporting
- Governance tasks

Most repetitive Azure administrative tasks can be automated using Azure CLI.

---

# Enterprise Scenario

An organization deploys hundreds of Virtual Machines every month.

Instead of creating resources manually through the Azure Portal, administrators use Azure CLI scripts to:

- Create Resource Groups.
- Deploy Virtual Machines.
- Configure networking.
- Create Storage Accounts.
- Apply Tags.
- Configure RBAC.
- Generate deployment reports.

Automation reduces deployment time, improves consistency, and minimizes human error.

---

# Common Pitfalls

- Forgetting to authenticate.
- Using the wrong subscription.
- Hardcoding sensitive information in scripts.
- Ignoring command output.
- Not validating resource existence before creation.
- Running destructive commands without confirmation.
- Mixing Azure CLI syntax with Azure PowerShell syntax.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure CLI architecture
> - Authentication methods
> - Subscription management
> - Command structure
> - Output formats
> - JMESPath queries
> - Azure CLI vs Azure PowerShell
> - Azure CLI vs Azure Portal
> - Azure Cloud Shell integration
> - Automation scenarios

---

# Key Takeaways

- Azure CLI is Microsoft's cross-platform command-line interface for managing Azure resources through Azure Resource Manager.
- Its consistent command structure, support for multiple output formats, and JMESPath query language make it well suited for scripting and automation.
- Azure CLI integrates seamlessly with Azure Cloud Shell, CI/CD pipelines, and automation workflows, allowing administrators to manage Azure efficiently from almost any environment.
- Understanding authentication, subscription management, and command syntax is essential for both day-to-day Azure administration and the AZ-104 exam.
- Azure CLI is one of the most widely used tools for automating Azure infrastructure deployments and operational tasks.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure CLI documentation | https://learn.microsoft.com/cli/azure/ |
| Install Azure CLI | https://learn.microsoft.com/cli/azure/install-azure-cli |
| Azure CLI command reference | https://learn.microsoft.com/cli/azure/reference-index |
| Azure Cloud Shell | https://learn.microsoft.com/azure/cloud-shell/overview |
| JMESPath | https://jmespath.org/ |
| Azure Resource Manager | https://learn.microsoft.com/azure/azure-resource-manager/management/overview |
| Microsoft Learn – Introduction to Azure CLI | https://learn.microsoft.com/training/modules/intro-to-azure-cli/ |
