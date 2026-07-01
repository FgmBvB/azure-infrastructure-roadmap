# Azure CLI

> [!NOTE]
> This section is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Azure CLI, Microsoft's cross-platform command-line interface for managing Azure resources, automating deployments, and administering cloud infrastructure through Azure Resource Manager.

---

# Overview

Azure CLI is one of the primary administration tools available for Azure.

It allows administrators to provision, configure, automate, monitor, and manage Azure resources using simple, consistent commands from virtually any operating system.

Unlike the Azure Portal, Azure CLI is designed for repeatable automation, scripting, CI/CD pipelines, and large-scale infrastructure management.

---

# Learning Objectives

After completing this section you should be able to:

- Understand Azure CLI architecture.
- Authenticate securely.
- Manage Azure subscriptions.
- Execute Azure CLI commands.
- Understand command syntax.
- Configure Azure CLI defaults.
- Use JMESPath queries.
- Format command output.
- Automate Azure administration.
- Handle long-running operations.
- Use Azure Cloud Shell effectively.
- Apply Azure CLI best practices.

---

# Section Structure

| Document | Description |
|----------|-------------|
| **01 - Overview** | Azure CLI architecture, authentication, command structure, Azure Resource Manager integration, JMESPath queries, output formats, Cloud Shell, automation scenarios, asynchronous operations, and AZ-104 fundamentals. |
| **02 - Best Practices** | Secure authentication, subscription management, default configuration, automation techniques, JMESPath usage, TSV output, long-running operations, Cloud Shell persistence, scripting recommendations, and Microsoft's production best practices. |

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

Azure CLI communicates with Azure Resource Manager (ARM), which authenticates, authorizes, and forwards requests to the appropriate Azure Resource Provider.

---

# Core Capabilities

This section covers the primary Azure CLI capabilities.

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

- Bash scripting
- PowerShell integration
- CI/CD pipelines
- Azure DevOps
- GitHub Actions
- Bulk administration

---

## Query and Reporting

- JSON output
- Table output
- YAML output
- TSV output
- JMESPath filtering

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

Select Subscription

↓

Execute Commands

↓

Query Resources

↓

Deploy or Modify Resources

↓

Validate Results

↓

Automation
```

Azure CLI enables administrators to automate the complete lifecycle of Azure resources.

---

# Design Principles

Microsoft recommends following these principles:

- Automate repetitive administrative tasks.
- Authenticate securely.
- Verify the active subscription.
- Use default CLI configuration where appropriate.
- Filter results using JMESPath.
- Protect secrets and credentials.
- Store scripts in version control.
- Use asynchronous operations for long deployments.
- Validate resources before making changes.
- Review scripts regularly.

---

# AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Azure CLI
- Authentication
- Azure Resource Manager
- Subscription management
- Command syntax
- Output formats
- JMESPath queries
- Azure Cloud Shell
- Azure CLI configuration
- Long-running operations
- Automation best practices

---

# Key Takeaways

- Azure CLI is Microsoft's cross-platform command-line interface for managing Azure resources through Azure Resource Manager.
- It provides a consistent command structure for administration, scripting, and infrastructure automation across Windows, Linux, macOS, and Azure Cloud Shell.
- Features such as JMESPath queries, configurable defaults, multiple output formats, and asynchronous operations make Azure CLI well suited for enterprise automation.
- Azure CLI integrates seamlessly with Azure Cloud Shell, CI/CD platforms, and Azure services, enabling secure and repeatable infrastructure management.
- Mastering Azure CLI is an essential skill for Azure administrators and a key objective of the AZ-104 certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure CLI documentation | https://learn.microsoft.com/cli/azure/ |
| Azure CLI command reference | https://learn.microsoft.com/cli/azure/reference-index |
| Install Azure CLI | https://learn.microsoft.com/cli/azure/install-azure-cli |
| Azure Cloud Shell | https://learn.microsoft.com/azure/cloud-shell/overview |
| Azure Resource Manager | https://learn.microsoft.com/azure/azure-resource-manager/management/overview |
| Microsoft Learn – Introduction to Azure CLI | https://learn.microsoft.com/training/modules/intro-to-azure-cli/ |
