# ARM Templates Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for designing, deploying, and maintaining Azure Resource Manager (ARM) Templates in production environments.

---

# Overview

ARM Templates provide a consistent and repeatable way to deploy Azure infrastructure.

Following Microsoft's best practices improves deployment reliability, simplifies maintenance, reduces configuration drift, and minimizes operational risk.

---

# Prefer Incremental Deployments

Use **Incremental** deployment mode whenever possible.

Incremental mode:

- Creates missing resources.
- Updates existing resources.
- Leaves unmanaged resources unchanged.

This is the default and recommended deployment mode for production environments.

Complete mode should only be used after carefully validating its impact.

---

# Parameterize Everything

Avoid hardcoding environment-specific values.

Use parameters for:

- Resource names
- Regions
- VM sizes
- Storage SKUs
- Network configuration
- Tags

Parameterization makes templates reusable across multiple environments.

---

# Separate Templates from Parameter Files

Microsoft recommends keeping infrastructure definitions separate from environment-specific configuration.

A common structure is:

```text
azuredeploy.json

azuredeploy.parameters.dev.json

azuredeploy.parameters.test.json

azuredeploy.parameters.prod.json
```

The ARM template defines the infrastructure once, while each parameter file supplies the values required for a specific environment.

Benefits include:

- Infrastructure reuse.
- Simpler environment management.
- Reduced duplication.
- Easier CI/CD integration.
- Lower risk of configuration errors.

This approach allows the same template to be deployed consistently across Development, Test, and Production.

---

# Use Variables to Reduce Duplication

Store repeated expressions inside variables.

Variables improve:

- Readability
- Maintainability
- Consistency

Avoid repeating identical values throughout a template.

---

# Use ARM Template Functions

ARM Template functions generate dynamic values during deployment.

Frequently used functions include:

- `concat()`
- `uniqueString()`
- `resourceId()`
- `subscription()`
- `resourceGroup()`

These functions eliminate hardcoded values and improve template portability.

---

# Keep Templates Modular

Large templates become difficult to maintain.

Whenever appropriate:

- Separate independent workloads.
- Reuse common building blocks.
- Organize deployments logically.

Smaller templates are easier to troubleshoot and version.

---

# Validate Before Deployment

Always validate templates before deploying.

Validation checks:

- JSON syntax
- Parameter values
- Resource types
- API versions
- Permissions
- Resource dependencies

Validation reduces deployment failures.

---

# Use What-If Before Deployment

Template validation confirms that a deployment is syntactically correct, but it does not show how existing resources will be affected.

The **What-If** operation compares the current Azure environment with the desired state defined in the template before deployment.

Typical results include:

- Resources to be created.
- Resources to be modified.
- Resources with no changes.
- Resources that may be deleted.

What-If helps administrators understand the expected impact of a deployment before applying changes.

It is especially valuable when reviewing production deployments or evaluating the effects of Complete deployment mode.

> [!TIP]
> Running a What-If operation before production deployments reduces the risk of unintended infrastructure changes.

---

# Use Latest Stable API Versions

Each Azure resource uses a specific API version.

Benefits of current API versions include:

- New features
- Bug fixes
- Improved compatibility
- Better security

Avoid deprecated API versions whenever possible.

---

# Protect Sensitive Information

Never store secrets directly inside templates.

Avoid embedding:

- Passwords
- Client Secrets
- Storage Keys
- SAS Tokens
- Connection Strings

Instead use:

- Azure Key Vault
- Secure parameters
- Managed Identities

Sensitive information should remain outside template code.

---

# Use Key Vault References

Sensitive values should never be stored directly inside ARM templates or parameter files.

Instead, use **Azure Key Vault** together with secure parameters and Key Vault references.

Sensitive parameters should use the **secureString** (or **secureObject**) data type so their values are masked during deployment.

Parameter files can reference secrets stored in Azure Key Vault instead of containing the secret itself.

Benefits include:

- Secrets remain outside template code.
- Passwords are not stored in source control.
- Deployment logs do not expose sensitive values.
- Centralized secret management.

> [!IMPORTANT]
> Azure Resource Manager retrieves the secret directly from Azure Key Vault during deployment. Appropriate permissions are required for the deployment to access the referenced secret.

---

# Minimize Explicit Dependencies

Azure Resource Manager automatically determines many deployment dependencies.

Use:

```json
dependsOn
```

only when required.

Excessive dependencies reduce deployment parallelism and increase deployment time.

---

# Use Outputs Effectively

Outputs should expose only useful deployment information.

Typical outputs include:

- Resource IDs
- Public IP addresses
- Storage endpoints
- DNS names

Avoid exposing sensitive values.

---

# Store Templates in Source Control

Treat ARM Templates as Infrastructure as Code.

Benefits include:

- Version history
- Peer review
- Collaboration
- Rollback capability
- Change tracking

Git repositories should be the primary location for template management.

---

# Use Meaningful Naming Conventions

Apply consistent naming standards.

Resource names should clearly identify:

- Workload
- Environment
- Region
- Resource type

Consistent naming simplifies administration.

---

# Apply Resource Tags

Deploy tags as part of the template.

Typical tags include:

- Environment
- Owner
- CostCenter
- Application
- BusinessUnit

Tags improve governance and Cost Management.

---

# Test Before Production

Validate templates in:

- Development
- Test
- Staging

before deploying to Production.

Testing reduces operational risk.

---

# Document Templates

Include comments and documentation whenever appropriate.

Document:

- Parameters
- Variables
- Resource relationships
- Deployment requirements
- Dependencies

Good documentation simplifies long-term maintenance.

---

# Implement Idempotent Deployments

ARM Templates are designed to be idempotent.

Running the same template multiple times should:

- Create missing resources.
- Update configuration when necessary.
- Leave unchanged resources intact.

Avoid designing templates that require manual cleanup between deployments.

---

# Review Deployment Results

Always verify deployment status after execution.

Review:

- Deployment history
- Errors
- Outputs
- Provisioning state

Early validation simplifies troubleshooting.

---

# Enterprise Scenario

A multinational company deploys infrastructure across Development, Test, and Production.

Administrators:

- Store ARM Templates in Git.
- Parameterize every environment.
- Use Incremental deployments.
- Retrieve secrets from Azure Key Vault.
- Validate templates before deployment.
- Apply governance tags automatically.
- Review deployment history after every release.

This approach produces reliable, repeatable, and secure infrastructure deployments.

---

# Best Practices Checklist

- Prefer Incremental deployments.
- Parameterize environment-specific values.
- Use variables to reduce duplication.
- Use ARM Template functions.
- Keep templates modular.
- Validate before deployment.
- Use current API versions.
- Protect sensitive information.
- Minimize explicit dependencies.
- Use outputs appropriately.
- Store templates in source control.
- Apply consistent naming conventions.
- Deploy governance tags.
- Test before production.
- Document templates.
- Design idempotent deployments.
- Review deployment results.

---

# Common Pitfalls

- Using Complete mode unintentionally.
- Hardcoding resource names.
- Embedding secrets inside templates.
- Ignoring validation errors.
- Using deprecated API versions.
- Creating unnecessary dependencies.
- Forgetting governance tags.
- Producing oversized templates that are difficult to maintain.
- Not reviewing deployment outputs.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Incremental vs Complete deployments
> - Parameters
> - Variables
> - ARM Template functions
> - Deployment validation
> - API versions
> - Dependencies
> - Outputs
> - Infrastructure as Code
> - Template modularity
> - Idempotent deployments

---

# Key Takeaways

- ARM Templates enable consistent, repeatable, and idempotent Infrastructure as Code deployments through Azure Resource Manager.
- Microsoft recommends parameterizing deployments, using variables and built-in template functions, and validating templates before deployment.
- Incremental deployment mode is the preferred option for most production scenarios, while Complete mode should be used only after careful impact analysis.
- Secrets should be stored outside templates by using Azure Key Vault or other secure mechanisms, and templates should be version-controlled like application code.
- Following Microsoft's best practices results in secure, maintainable, scalable, and production-ready ARM Template deployments while covering key AZ-104 exam objectives.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| ARM Templates documentation | https://learn.microsoft.com/azure/azure-resource-manager/templates/ |
| ARM Template best practices | https://learn.microsoft.com/azure/azure-resource-manager/templates/best-practices |
| ARM Template reference | https://learn.microsoft.com/azure/templates/ |
| Deployment modes | https://learn.microsoft.com/azure/azure-resource-manager/templates/deployment-modes |
| Azure Key Vault | https://learn.microsoft.com/azure/key-vault/general/overview |
| Bicep documentation | https://learn.microsoft.com/azure/azure-resource-manager/bicep/ |
| Microsoft Learn – Deploy Azure resources by using ARM templates | https://learn.microsoft.com/training/modules/create-azure-resource-manager-template-vs-code/ |
