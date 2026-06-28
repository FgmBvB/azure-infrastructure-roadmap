# Managed Identity Best Practices

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It summarizes Microsoft's recommended practices for securely implementing and managing Managed Identities in Azure.

---

## Security Lifecycle

```text
Create Managed Identity
           │
           ▼
Assign Azure RBAC Roles
           │
           ▼
Use Credential-Free Authentication
           │
           ▼
Monitor Identity Activity
           │
           ▼
Review Permissions
           │
           ▼
Remove Unused Identities
```

---

> [!TIP]
> **Key Concepts**
>
> - Prefer Managed Identities over Client Secrets.
> - Apply the principle of least privilege.
> - Assign Azure RBAC roles at the lowest practical scope.
> - Monitor identity usage regularly.
> - Remove unused identities and permissions.

---

## Overview

Managed Identities eliminate the need to store credentials inside Azure applications.

Following Microsoft's recommended practices improves security, simplifies administration, and reduces the attack surface by replacing manually managed secrets with identities managed automatically by Azure.

---

## Prefer Managed Identities

Whenever supported, use Managed Identities instead of:

- Client Secrets
- Certificates
- Embedded credentials
- Storage Account Keys

Credential-free authentication reduces operational overhead and minimizes the risk of credential exposure.

---

## Choose the Appropriate Identity Type

Select the identity type according to the workload.

| Scenario | Recommended Identity |
|----------|----------------------|
| One Azure resource | System-Assigned |
| Multiple Azure resources sharing permissions | User-Assigned |
| Temporary workloads | System-Assigned |
| Shared application identity | User-Assigned |

Choosing the correct identity type simplifies lifecycle management.

---

## Apply Least Privilege

Grant only the permissions required.

Recommendations include:

- Assign Azure RBAC roles at the lowest practical scope.
- Prefer built-in roles.
- Avoid Contributor or Owner unless required.
- Review inherited permissions regularly.

---

## Secure Azure RBAC

Azure RBAC controls authorization after authentication.

Microsoft recommends:

- Assign roles only to required identities.
- Review role assignments periodically.
- Remove unnecessary permissions.
- Avoid assigning broad permissions at the Subscription scope.

---

## Protect Sensitive Resources

Managed Identities should be used to access services such as:

- Azure Key Vault
- Azure Storage
- Azure SQL Database
- Azure Resource Manager
- Microsoft Graph

Avoid storing credentials inside configuration files, source code, or deployment pipelines.

---

## Monitor Identity Activity

Administrators should regularly review:

- Sign-in Logs
- Audit Logs
- Azure RBAC assignments
- Credential configuration
- Failed authentication attempts

Continuous monitoring helps detect misconfigurations and suspicious activity.

---

## Governance

Organizations should establish governance policies for Managed Identities.

Recommended activities include:

- Document identity ownership.
- Review Azure RBAC assignments periodically.
- Remove unused Managed Identities.
- Audit privileged identities.
- Review access to sensitive resources.

---

## Lifecycle Management

Managed Identities should be managed throughout their lifecycle.

```text
Create
   │
   ▼
Assign Permissions
   │
   ▼
Use
   │
   ▼
Monitor
   │
   ▼
Review
   │
   ▼
Remove
```

Unused identities and unnecessary role assignments should be removed promptly.

---

## Enterprise Scenario

A company migrates several internal applications to Azure App Service.

Instead of storing Client Secrets in application settings, each App Service uses a Managed Identity.

Azure RBAC grants only the permissions required for Azure Key Vault and Azure Storage.

Regular reviews ensure that unused identities and excessive permissions are removed.

---

## Best Practices Checklist

- Prefer Managed Identities over Client Secrets.
- Use System-Assigned identities whenever sharing is unnecessary.
- Use User-Assigned identities only when multiple resources require the same identity.
- Apply the principle of least privilege.
- Assign Azure RBAC roles at the lowest practical scope.
- Prefer built-in Azure RBAC roles.
- Monitor Sign-in and Audit Logs.
- Review Azure RBAC assignments regularly.
- Remove unused Managed Identities.
- Document ownership and business purpose.
- Audit privileged identities periodically.

---

## Common Pitfalls

- Storing credentials unnecessarily.
- Granting excessive Azure RBAC permissions.
- Forgetting to review role assignments.
- Leaving unused Managed Identities deployed.
- Confusing authentication with authorization.
- Using User-Assigned identities when System-Assigned identities are sufficient.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Managed Identity governance
> - Azure RBAC best practices
> - Least privilege
> - Identity lifecycle
> - Monitoring and auditing
> - Choosing the appropriate Managed Identity type

---

## Key Takeaways

- Managed Identities eliminate credential management.
- Azure RBAC controls authorization.
- Least privilege reduces security risks.
- Continuous monitoring improves operational security.
- Proper lifecycle management reduces unnecessary identities and permissions.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Managed Identities overview](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview) | Managed Identities overview |
| [Managed Identities FAQ](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/managed-identities-faq) | Managed Identity concepts and lifecycle |
| [Azure RBAC overview](https://learn.microsoft.com/azure/role-based-access-control/overview) | Azure RBAC fundamentals |
| [Managed identities best practices](https://learn.microsoft.com/azure/well-architected/service-guides/managed-identities) | Microsoft Well-Architected guidance |
| [Microsoft Learn – Managed Identities](https://learn.microsoft.com/training/modules/managed-identities-azure-resources/) | Microsoft Learn module |
