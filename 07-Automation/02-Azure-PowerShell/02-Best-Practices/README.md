# Azure PowerShell Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for using Azure PowerShell securely, efficiently, and consistently in production environments.

---

# Overview

Azure PowerShell is designed for repeatable, object-oriented administration of Azure resources.

Microsoft recommends treating PowerShell scripts as production code by following secure authentication practices, using reusable automation techniques, validating operations, and leveraging the PowerShell pipeline effectively.

---

# Authenticate Securely

Always use the most appropriate authentication method.

Recommended options include:

- Interactive login for administrators.
- Service Principals for automation.
- Managed Identities for Azure-hosted workloads.
- Azure Cloud Shell for browser-based administration.

Avoid storing credentials directly inside scripts.

---

# Verify the Active Context

Before executing Azure PowerShell cmdlets, always verify the active Azure context.

Example:

```powershell
Get-AzContext
```

Switch subscriptions when necessary:

```powershell
Set-AzContext -Subscription "<subscription-name>"
```

Running commands against the wrong subscription is one of the most common administrative mistakes.

---

# Use Named Parameters

Always use explicit parameter names whenever possible.

Example:

```powershell
Get-AzVM `
    -ResourceGroupName "Production-RG"
```

Named parameters improve:

- Readability
- Maintainability
- Script reliability

---

# Leverage the PowerShell Pipeline

Azure PowerShell is designed around object-oriented pipelines.

Example:

```powershell
Get-AzVM -ResourceGroupName "Production-RG" |
Stop-AzVM -Force
```

Benefits include:

- Cleaner code
- Bulk administration
- Reduced repetition
- Easier automation

Prefer passing objects through the pipeline instead of manually extracting values whenever supported.

---

# Use Select-Object and Where-Object

Avoid processing unnecessary data.

Examples:

```powershell
Get-AzVM |
Select-Object Name, Location
```

```powershell
Get-AzVM |
Where-Object {$_.Location -eq "East US"}
```

Filtering objects early improves script readability and efficiency.

---

# Store Reusable Values in Variables

Avoid repeating the same values throughout a script.

Example:

```powershell
$ResourceGroup = "Production-RG"

Get-AzVM -ResourceGroupName $ResourceGroup
```

Variables simplify maintenance and reduce typing errors.

---

# Handle Long-Running Operations Efficiently

Some Azure operations require several minutes to complete.

Examples include:

- Virtual Machine deployment
- VPN Gateway creation
- Azure Firewall deployment
- Resource Group deletion

When supported, use:

```powershell
-NoWait
```

to return control immediately.

For lengthy operations that should continue independently, use:

```powershell
-AsJob
```

This allows PowerShell to execute the operation as a background job while the current session continues with other tasks.

---

# Validate Resources Before Making Changes

Always verify that resources exist before attempting modifications.

Typical checks include:

- Resource Groups
- Virtual Machines
- Storage Accounts
- Virtual Networks

Validation improves script reliability and reduces unnecessary failures.

---

# Use Error Handling

Production scripts should always handle failures gracefully.

Typical techniques include:

```powershell
try
{
    # Azure operation
}
catch
{
    Write-Error $_
}
```

Good error handling improves troubleshooting and automation reliability.

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
- Secure CI/CD secret stores

---

# Store Scripts in Source Control

Treat PowerShell scripts as Infrastructure as Code.

Benefits include:

- Version history
- Code reviews
- Collaboration
- Rollback capability
- Auditability

Git repositories should be the standard location for production automation.

---

# Log Important Operations

Administrative scripts should generate meaningful logs.

Typical information includes:

- Resources created
- Resources modified
- Resources deleted
- Execution time
- Errors
- Exit status

Logging simplifies operational support.

---

# Keep Modules Updated

Microsoft continuously updates the Az module.

Regularly update installed modules.

Example:

```powershell
Update-Module Az
```

Keeping modules current ensures:

- Bug fixes
- Security improvements
- New Azure features
- Compatibility with Azure APIs

---

# Use Azure Cloud Shell When Appropriate

Cloud Shell provides:

- Azure PowerShell preinstalled
- Automatic authentication
- Persistent storage
- Browser-based administration
- Always up-to-date modules

It is ideal for administrative work from any location.

---

# Apply Least Privilege

Automation accounts should receive only the permissions required.

Prefer:

- Reader
- Contributor
- Virtual Machine Contributor
- Storage Account Contributor

rather than assigning Owner unnecessarily.

Least privilege reduces security risks.

---

# Review Scripts Regularly

Azure services evolve continuously.

Review scripts periodically to:

- Remove deprecated cmdlets
- Improve performance
- Simplify logic
- Adopt new Azure capabilities
- Improve readability

Automation should evolve with the Azure platform.

---

# Enterprise Scenario

A company manages hundreds of Azure Virtual Machines across multiple subscriptions.

Administrators:

- Authenticate using Managed Identities.
- Verify Azure contexts before execution.
- Use PowerShell pipelines for bulk operations.
- Retrieve secrets from Azure Key Vault.
- Store automation in Git.
- Execute long-running deployments using **-AsJob**.
- Keep Az modules updated regularly.

This approach produces secure, scalable, and maintainable automation.

---

# Best Practices Checklist

- Authenticate securely.
- Verify the active Azure context.
- Use named parameters.
- Leverage the PowerShell pipeline.
- Filter objects efficiently.
- Store reusable values in variables.
- Validate resources before making changes.
- Use error handling.
- Protect secrets.
- Store scripts in source control.
- Log important operations.
- Use **-NoWait** when appropriate.
- Use **-AsJob** for long-running tasks.
- Keep the Az module updated.
- Apply least privilege.
- Review automation regularly.

---

# Common Pitfalls

- Running commands in the wrong subscription.
- Forgetting to verify the Azure context.
- Mixing Azure CLI commands with Azure PowerShell cmdlets.
- Hardcoding credentials.
- Ignoring cmdlet errors.
- Using deprecated AzureRM cmdlets.
- Not updating the Az module.
- Overusing the Owner role.
- Writing scripts without logging or error handling.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Azure contexts
> - PowerShell pipeline
> - Named parameters
> - Error handling
> - Background jobs
> - Long-running operations
> - Authentication methods
> - Azure Cloud Shell
> - Az module management
> - Automation best practices

---

# Key Takeaways

- Azure PowerShell is most effective when used through reusable, object-oriented automation rather than isolated manual commands.
- Verifying the active Azure context, using the PowerShell pipeline, and handling errors correctly are essential for reliable administration.
- Features such as named parameters, background jobs, reusable variables, and the Az module simplify large-scale automation.
- Azure Cloud Shell, Managed Identities, and Azure Key Vault provide secure foundations for production-grade scripting.
- Following Microsoft's best practices results in automation that is secure, maintainable, scalable, and aligned with enterprise Azure environments.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure PowerShell documentation | https://learn.microsoft.com/powershell/azure/ |
| Az module reference | https://learn.microsoft.com/powershell/module/az/ |
| Install Azure PowerShell | https://learn.microsoft.com/powershell/azure/install-az-ps |
| Azure Cloud Shell | https://learn.microsoft.com/azure/cloud-shell/overview |
| Azure Key Vault | https://learn.microsoft.com/azure/key-vault/general/overview |
| Managed Identities | https://learn.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview |
| Microsoft Learn – Automate Azure tasks with PowerShell | https://learn.microsoft.com/training/modules/automate-azure-tasks-with-powershell/ |
