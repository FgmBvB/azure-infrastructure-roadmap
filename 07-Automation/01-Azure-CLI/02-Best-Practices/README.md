# Azure CLI Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for using Azure CLI efficiently, securely, and consistently in production environments.

---

# Overview

Azure CLI is a powerful automation tool that enables administrators to manage Azure resources consistently across Windows, Linux, macOS, Cloud Shell, and CI/CD platforms.

Microsoft recommends treating Azure CLI scripts as production code by applying security, validation, automation, and governance best practices.

---

# Authenticate Securely

Always use the appropriate authentication method for the environment.

Recommended methods include:

- Interactive login for administrators.
- Service Principals for automation.
- Managed Identities for Azure-hosted workloads.
- Azure Cloud Shell for browser-based administration.

Avoid embedding credentials directly into scripts.

---

# Verify the Active Subscription

Many Azure environments contain multiple subscriptions.

Always verify the current subscription before executing commands.

Example:

```bash
az account show
```

Switch subscriptions when necessary:

```bash
az account set --subscription "<subscription-name>"
```

Deploying resources into the wrong subscription is one of the most common administrative mistakes.

---

# Configure Default Values

Reduce repetitive parameters by configuring default settings.

Example:

```bash
az configure
```

Typical defaults include:

- Resource Group
- Location
- Output format

This improves script readability and consistency.

---

# Use Resource Groups Consistently

Organize related resources into Resource Groups.

Benefits include:

- Simplified deployments.
- Easier lifecycle management.
- Better governance.
- Simplified RBAC assignments.
- Improved Cost Management reporting.

---

# Prefer Automation Over Manual Operations

Repeatable administrative tasks should be automated.

Typical candidates include:

- Resource provisioning.
- VM management.
- Storage configuration.
- RBAC assignments.
- Network deployment.
- Resource cleanup.

Automation reduces human error and improves consistency.

---

# Use JMESPath Queries

Avoid processing large JSON outputs manually.

Instead, filter results directly using JMESPath.

Example:

```bash
az vm list \
  --query "[].{VM:name, ResourceGroup:resourceGroup}"
```

Benefits include:

- Faster scripts.
- Smaller output.
- Easier reporting.
- Reduced parsing.

---

# Choose the Appropriate Output Format

Azure CLI supports multiple output formats.

Choose the one that best fits the task.

| Format | Typical Use |
|----------|-------------|
| json | Automation |
| table | Interactive administration |
| yaml | Configuration review |
| tsv | Shell scripting |
| none | Silent execution |

Selecting the appropriate output format simplifies automation.

---

# Using TSV Output for Automation

The **tsv** (Tab-Separated Values) output format is particularly useful for shell scripting.

Unlike JSON or table output, TSV removes:

- Quotes
- Brackets
- Property names
- Formatting characters

Example:

```bash
VNET_ID=$(az network vnet show \
  --resource-group MyRG \
  --name MyVNet \
  --query id \
  --output tsv)
```

The captured value can then be reused directly in subsequent Azure CLI commands.

Typical use cases include:

- Bash variables
- Loops
- CI/CD pipelines
- Resource IDs
- Automation scripts

> [!TIP]
> Use `--output tsv` whenever command output will be consumed by another command or stored in shell variables.

---

# Validate Resources Before Creating Them

Avoid creating duplicate resources.

Verify that a resource does not already exist before deployment.

Typical validation includes:

- Resource Groups.
- Storage Accounts.
- Virtual Machines.
- Virtual Networks.

Validation improves deployment reliability.

---

# Handle Long-Running Operations

Some Azure resources require several minutes to provision.

Examples include:

- VPN Gateway
- Azure Firewall
- AKS
- ExpressRoute Gateway

Use:

```bash
--no-wait
```

when appropriate to improve script efficiency.

Wait commands should only be used when later steps depend on successful resource creation.

---

# Waiting for Long-Running Operations

Long-running Azure deployments are often executed asynchronously using `--no-wait`.

However, later steps in an automation script may depend on the resource being fully provisioned.

Azure CLI provides dedicated **wait commands** that poll Azure Resource Manager until a resource reaches the desired state.

Example:

```bash
az vm wait \
  --resource-group MyRG \
  --name MyVM \
  --created
```

Typical wait conditions include:

- Created
- Deleted
- Exists
- Updated

Using wait commands makes automation more reliable by ensuring that dependent operations execute only after Azure has completed the requested deployment.

> [!TIP]
> A common automation pattern is to start several long-running deployments with `--no-wait` and synchronize only when later steps require those resources.

---

# Store Scripts in Source Control

Treat Azure CLI scripts as infrastructure code.

Use Git repositories to:

- Track changes.
- Review modifications.
- Collaborate with teams.
- Roll back changes.
- Version deployments.

Infrastructure automation should follow the same lifecycle as application code.

---

# Use Parameters Instead of Hardcoding

Avoid embedding environment-specific values.

Parameterize values such as:

- Subscription IDs
- Resource Groups
- Regions
- VM names
- Storage Account names

Reusable scripts are easier to maintain.

---

# Protect Sensitive Information

Never expose:

- Passwords
- Client Secrets
- Connection Strings
- SAS Tokens
- Access Keys

Use:

- Azure Key Vault
- Managed Identities
- Secure CI/CD secrets

Sensitive values should never appear in source code repositories.

---

# Log Important Operations

Production scripts should generate useful logs.

Examples include:

- Resources created.
- Resources deleted.
- Deployment duration.
- Errors.
- Exit status.

Logging simplifies troubleshooting.

---

# Implement Error Handling

Always validate command success.

Typical techniques include:

- Exit code validation.
- Conditional execution.
- Retry logic.
- Meaningful error messages.

Robust scripts are more reliable.

---

# Use Azure Cloud Shell When Appropriate

Cloud Shell provides:

- Preinstalled Azure CLI.
- Automatic authentication.
- Persistent storage.
- Browser-based access.
- No local installation.

It is ideal for administrative tasks from any workstation.

---

# Azure Cloud Shell Persistence

Azure Cloud Shell provides persistent storage by mounting an Azure Files share into the Cloud Shell environment.

The mounted directory is:

```text
$HOME/clouddrive
```

This location stores:

- Scripts
- Configuration files
- Templates
- Downloaded resources

If the associated Storage Account or Azure File Share is removed, Cloud Shell loses its persistent storage and will require a new storage location to be configured before persistence is restored.

> [!IMPORTANT]
> Cloud Shell itself is temporary, but files stored under **$HOME/clouddrive** persist across sessions because they are backed by Azure Files.

---

# Follow the Principle of Least Privilege

Grant only the permissions required.

Automation accounts should receive:

- Minimum RBAC roles.
- Limited scope.
- Temporary elevation when required.

Reducing privileges minimizes security risks.

---

# Review Scripts Regularly

Azure evolves continuously.

Periodically review scripts to:

- Remove deprecated commands.
- Update API versions.
- Improve performance.
- Apply new Azure capabilities.
- Improve readability.

Maintenance is part of automation.

---

# Enterprise Scenario

A multinational company manages hundreds of Azure subscriptions.

Administrators:

- Authenticate using Managed Identities.
- Store scripts in Git.
- Use Azure DevOps pipelines.
- Retrieve secrets from Key Vault.
- Filter outputs using JMESPath.
- Configure default CLI values.
- Review scripts after Azure feature updates.

This approach produces secure, repeatable, and maintainable automation.

---

# Best Practices Checklist

- Authenticate securely.
- Verify the active subscription.
- Configure default values.
- Organize resources consistently.
- Automate repetitive tasks.
- Use JMESPath queries.
- Select the correct output format.
- Validate resources before deployment.
- Handle long-running operations efficiently.
- Store scripts in source control.
- Parameterize scripts.
- Protect sensitive information.
- Implement logging.
- Handle errors properly.
- Apply least privilege.
- Review automation regularly.

---

# Common Pitfalls

- Running commands in the wrong subscription.
- Hardcoding credentials.
- Ignoring command failures.
- Creating duplicate resources.
- Parsing JSON manually instead of using JMESPath.
- Executing long-running operations synchronously when unnecessary.
- Not storing scripts in version control.
- Using excessive RBAC permissions.
- Forgetting to update scripts after Azure service changes.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Secure authentication
> - Subscription management
> - Default CLI configuration
> - JMESPath filtering
> - Output formats
> - Automation best practices
> - Error handling
> - Source control
> - Azure Cloud Shell
> - Least privilege
> - Long-running operations

---

# Key Takeaways

- Azure CLI is most effective when used as part of a repeatable automation strategy rather than for isolated manual tasks.
- Secure authentication, parameterized scripts, version control, and proper error handling improve both reliability and maintainability.
- Features such as JMESPath queries, configurable defaults, and appropriate output formats simplify scripting and reduce operational complexity.
- Azure Cloud Shell, Managed Identities, and Azure Key Vault provide secure ways to administer Azure without exposing sensitive credentials.
- Applying Microsoft's recommended practices helps create automation that is secure, scalable, consistent, and aligned with production environments.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Azure CLI documentation | https://learn.microsoft.com/cli/azure/ |
| Azure CLI command reference | https://learn.microsoft.com/cli/azure/reference-index |
| Azure Cloud Shell | https://learn.microsoft.com/azure/cloud-shell/overview |
| Azure Key Vault | https://learn.microsoft.com/azure/key-vault/general/overview |
| Managed Identities | https://learn.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview |
| Azure Resource Manager | https://learn.microsoft.com/azure/azure-resource-manager/management/overview |
| Microsoft Learn – Introduction to Azure CLI | https://learn.microsoft.com/training/modules/intro-to-azure-cli/ |
```
