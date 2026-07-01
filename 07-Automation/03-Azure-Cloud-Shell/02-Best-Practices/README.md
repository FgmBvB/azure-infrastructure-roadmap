# Azure Cloud Shell Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for using Azure Cloud Shell securely, efficiently, and consistently in production environments.

---

# Overview

Azure Cloud Shell provides a secure, browser-based administration environment with Azure CLI and Azure PowerShell preinstalled.

Although Cloud Shell requires almost no setup, administrators should follow operational best practices to maximize security, reliability, and productivity.

---

# Use Persistent Storage

Cloud Shell provides persistent storage through an Azure Files share mounted at:

```text
$HOME/clouddrive
```

Store important files such as:

- Azure CLI scripts
- PowerShell scripts
- ARM templates
- Bicep templates
- Terraform files
- Configuration files

Avoid storing important files outside **clouddrive**, since temporary storage is deleted when the session ends.

---

# Verify the Active Subscription

Cloud Shell automatically authenticates using your Azure account.

Always verify the active subscription before making changes.

Azure CLI:

```bash
az account show
```

Azure PowerShell:

```powershell
Get-AzContext
```

Switch subscriptions whenever necessary.

---

# Keep Scripts in Source Control

Do not use Cloud Shell as permanent storage.

Instead:

- Store automation in Git repositories.
- Clone repositories into Cloud Shell.
- Commit changes frequently.
- Use GitHub or Azure DevOps for version control.

Cloud Shell should be considered an execution environment, not a source code repository.

---

# Protect Sensitive Information

Never store:

- Passwords
- Client Secrets
- Storage Keys
- SAS Tokens
- Connection Strings

Instead use:

- Azure Key Vault
- Managed Identities
- Secure pipeline secrets

Sensitive information should never be saved inside scripts.

---

# Use the Appropriate Shell

Select the shell that best fits the task.

Use **Bash** when working primarily with:

- Azure CLI
- Linux administration
- Bash scripting

Use **PowerShell** when working with:

- Azure PowerShell
- PowerShell objects
- Object pipelines
- Windows administration

Choosing the correct shell simplifies automation.

---

# Organize Files

Maintain a consistent directory structure.

Example:

```text
clouddrive/

├── Scripts/
├── Bicep/
├── ARM/
├── Terraform/
├── Reports/
└── Logs/
```

Well-organized storage improves productivity.

---

# Automate Repetitive Tasks

Cloud Shell is ideal for executing repeatable administrative tasks.

Examples include:

- Resource deployment
- Virtual Machine management
- Networking configuration
- Storage administration
- RBAC assignments
- Cost reporting

Avoid repeating manual portal operations whenever automation is possible.

---

# Use Integrated Tools

Cloud Shell includes numerous Microsoft-maintained tools.

Examples include:

- Azure CLI
- Azure PowerShell
- Git
- Bicep
- Terraform
- kubectl
- Helm

Avoid installing duplicate tools unless absolutely necessary.

---

# Save Work Frequently

Cloud Shell sessions are temporary.

Always save:

- Scripts
- Templates
- Reports
- Configuration files

inside **$HOME/clouddrive**.

Unsaved work stored elsewhere may be lost when the session ends.

---

# Manage Long-Running Tasks Carefully

Cloud Shell sessions are intended for interactive administration.

Very long-running scripts should be designed to:

- Produce periodic output.
- Save intermediate results.
- Resume safely after interruption when possible.

For large-scale automation, consider Azure Automation, GitHub Actions, or Azure DevOps instead of relying on an interactive Cloud Shell session.

---

# Understand Session Persistence

Cloud Shell compute resources are temporary.

Only data stored in the mounted Azure Files share persists across sessions.

Typical persistent content includes:

- Scripts
- Templates
- Git repositories
- Configuration files

Running processes and temporary files are not preserved after the session ends.

---

# Monitor Storage Usage

The Azure Files share associated with Cloud Shell is billed as a normal Azure Storage resource.

Regularly:

- Remove obsolete files.
- Delete unused repositories.
- Archive old reports.
- Organize templates.

Good housekeeping helps reduce storage costs.

---

# Apply Least Privilege

Cloud Shell inherits the permissions of the authenticated Microsoft Entra account.

Use only the RBAC permissions required for administrative tasks.

Avoid assigning:

- Owner

when a more restrictive role is sufficient.

Examples include:

- Reader
- Contributor
- Virtual Machine Contributor
- Storage Account Contributor

---

# Use Cloud Shell for Administration

Cloud Shell is best suited for:

- Azure administration
- Troubleshooting
- Infrastructure deployments
- Quick automation
- Learning
- Operational support

Large software development projects should generally be performed in a dedicated local development environment.

---

# Enterprise Scenario

A cloud administrator needs to deploy Bicep templates across multiple subscriptions while travelling.

The administrator:

- Opens Azure Portal.
- Launches Cloud Shell.
- Verifies the active subscription.
- Clones the Git repository.
- Retrieves secrets from Azure Key Vault.
- Deploys infrastructure using Azure CLI.
- Saves deployment logs to **clouddrive**.
- Commits updated templates back to Git.

No local software installation is required.

---

# Best Practices Checklist

- Store important files in **$HOME/clouddrive**.
- Verify the active subscription.
- Keep scripts in source control.
- Protect secrets.
- Choose the appropriate shell.
- Organize directories.
- Automate repetitive tasks.
- Use built-in tools.
- Save work frequently.
- Understand session persistence.
- Monitor Azure Files storage usage.
- Apply least privilege.
- Use Cloud Shell for administration rather than development.

---

# Common Pitfalls

- Saving important files outside **clouddrive**.
- Running commands in the wrong subscription.
- Storing secrets inside scripts.
- Assuming Cloud Shell behaves like a permanent virtual machine.
- Ignoring Azure RBAC permissions.
- Leaving unnecessary files in the Azure Files share.
- Using Cloud Shell for workloads better suited to CI/CD or Azure Automation.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Persistent storage
> - Azure Files integration
> - Subscription verification
> - Azure CLI and Azure PowerShell usage
> - Built-in administration tools
> - Session lifecycle
> - Azure RBAC
> - Secure administration practices
> - Cloud Shell operational limitations

---

# Key Takeaways

- Azure Cloud Shell is a Microsoft-managed administration environment that provides immediate access to Azure CLI and Azure PowerShell without local installation.
- Persistent files should always be stored in **$HOME/clouddrive**, while temporary storage should never be relied upon for important data.
- Secure administration depends on verifying the active subscription, protecting secrets with Azure Key Vault or Managed Identities, and applying the principle of least privilege.
- Cloud Shell is ideal for interactive administration, troubleshooting, and Infrastructure as Code workflows, but long-running or enterprise-scale automation is better handled by dedicated automation platforms.
- Following Microsoft's best practices ensures Cloud Shell remains a secure, efficient, and reliable tool for Azure administration and the AZ-104 certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure Cloud Shell Overview | https://learn.microsoft.com/azure/cloud-shell/overview |
| Azure Cloud Shell Features | https://learn.microsoft.com/azure/cloud-shell/features |
| Azure CLI | https://learn.microsoft.com/cli/azure/ |
| Azure PowerShell | https://learn.microsoft.com/powershell/azure/ |
| Azure Files | https://learn.microsoft.com/azure/storage/files/storage-files-introduction |
| Azure Key Vault | https://learn.microsoft.com/azure/key-vault/general/overview |
| Microsoft Learn – Work with Azure Cloud Shell | https://learn.microsoft.com/training/modules/work-azure-cloud-shell/ |
