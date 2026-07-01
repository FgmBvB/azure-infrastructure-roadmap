# Identity Security Best Practices

> [!NOTE]
> This document is part of the Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It summarizes Microsoft's recommended practices for protecting identities, managing privileged access, enforcing least privilege, and implementing Zero Trust principles across Azure environments.

---

# Overview

Identity is the primary security boundary in Azure.

Compromised identities are one of the most common attack vectors in cloud environments. Microsoft therefore recommends implementing layered identity protection using Microsoft Entra ID, Azure RBAC, Conditional Access, Multi-Factor Authentication (MFA), Managed Identities, and Privileged Identity Management (PIM).

Identity security should always follow Zero Trust principles by continuously verifying access requests and granting only the minimum permissions required.

---

# Follow the Zero Trust Model

Microsoft recommends applying the three core Zero Trust principles:

- Verify explicitly.
- Use least privilege.
- Assume breach.

Never trust users or devices based solely on network location.

Every authentication and authorization request should be evaluated independently.

---

# Enforce Multi-Factor Authentication

Enable MFA for all privileged accounts.

Prioritize MFA for:

- Global Administrators
- Subscription Owners
- Azure Administrators
- Privileged Identity Management users

Whenever possible, use phishing-resistant authentication methods such as:

- Microsoft Authenticator
- FIDO2 Security Keys
- Windows Hello for Business

Avoid relying solely on passwords.

---

# Apply Conditional Access

Use Conditional Access to evaluate sign-in conditions before granting access.

Policies may enforce:

- MFA
- Device compliance
- Trusted locations
- Risk-based authentication
- Session controls

Apply Conditional Access broadly while maintaining emergency access accounts.

---

# Validate Conditional Access Policies

Incorrect Conditional Access policies can unintentionally block legitimate users or administrators.

Microsoft recommends validating every new policy before enforcing it.

## Report-only Mode

Conditional Access policies can initially be deployed in **Report-only** mode.

In this mode:

- Policies are evaluated.
- Sign-ins are recorded in the logs.
- No access is blocked.
- MFA is not enforced.

This allows administrators to verify the policy's impact before enabling enforcement.

---

## What If Tool

Microsoft Entra ID includes a built-in **What If** tool for Conditional Access.

Administrators can simulate sign-in scenarios by specifying:

- User
- Group
- Application
- Device
- Location
- Risk level

The simulator predicts which Conditional Access policies would apply without affecting production users.

> [!IMPORTANT]
> Microsoft recommends testing new Conditional Access policies using **Report-only** mode and the **What If** tool before enabling them in production.

---

# Apply Least Privilege

Grant only the permissions required to perform administrative tasks.

Prefer:

- Reader
- Contributor
- Resource-specific roles

Avoid assigning:

- Owner

unless full administrative control is genuinely required.

Review permissions regularly.

---

# Use Privileged Identity Management (PIM)

Avoid permanent administrator assignments.

Instead:

- Assign eligible roles.
- Require approval where appropriate.
- Require MFA during activation.
- Configure activation time limits.
- Review privileged assignments regularly.

PIM significantly reduces standing administrative privileges.

---

# Privileged Identity Management Activation

Privileged Identity Management distinguishes between **Eligible** and **Active** role assignments.

## Eligible

An eligible assignment does not grant administrative permissions immediately.

The user must activate the role before performing privileged operations.

Activation may require:

- Multi-Factor Authentication (MFA)
- Business justification
- Approval workflow

---

## Active

After successful activation, the role becomes active for a limited period.

Once the activation expires, Azure automatically revokes the elevated permissions and the assignment returns to the **Eligible** state.

Activation duration is configurable by administrators through PIM settings.

> [!NOTE]
> Just-in-time activation minimizes standing administrative privileges and is one of Microsoft's core Zero Trust recommendations.

---

# Separate Directory Roles from Resource Roles

Understand the distinction between Microsoft Entra ID roles and Azure RBAC roles.

Examples:

**Microsoft Entra ID**

- Global Administrator
- User Administrator
- Groups Administrator

**Azure RBAC**

- Owner
- Contributor
- Reader
- Virtual Machine Contributor

Assign directory permissions only when directory administration is required.

Assign Azure RBAC roles only for Azure resource management.

---

# Use Managed Identities

Avoid storing credentials inside applications.

Prefer Managed Identities for Azure resources accessing:

- Azure Key Vault
- Storage Accounts
- Azure SQL Database
- Azure Resource Manager
- Azure App Configuration

Whenever possible:

- Use System-Assigned identities for single-resource scenarios.
- Use User-Assigned identities when multiple resources require the same identity.

---

# Protect Secrets with Azure Key Vault

Never store:

- Passwords
- Client secrets
- Certificates
- Storage keys
- Connection strings

inside application code or deployment templates.

Store sensitive information in Azure Key Vault and retrieve it securely at runtime.

---

# Use Groups Instead of Individual Assignments

Assign RBAC roles to Microsoft Entra security groups rather than individual users whenever possible.

Benefits include:

- Easier administration
- Consistent permissions
- Simpler onboarding
- Simplified offboarding

Avoid managing permissions user by user.

---

# Assign Roles at the Lowest Possible Scope

Apply permissions using the smallest appropriate scope.

Preferred order:

```text
Resource

↓

Resource Group

↓

Subscription

↓

Management Group
```

Smaller scopes reduce security risks.

---

# Review Access Regularly

Periodically review:

- RBAC assignments
- PIM eligibility
- Conditional Access policies
- Guest users
- Managed Identities
- Application registrations

Remove unused permissions promptly.

---

# Protect Administrative Accounts

Separate administrative identities from daily user accounts.

Recommendations include:

- Dedicated administrator accounts
- MFA enforcement
- PIM activation
- No email usage from privileged accounts
- No web browsing from privileged accounts

Administrative identities should only be used for privileged operations.

---

# Secure Guest Access

Grant guest users only the permissions they require.

Review guest accounts periodically.

Remove inactive guest users and unnecessary external access.

---

# Monitor Identity Activity

Monitor authentication events using:

- Microsoft Entra sign-in logs
- Audit logs
- Azure Monitor
- Microsoft Defender for Cloud

Investigate:

- Failed sign-ins
- Impossible travel
- Risky sign-ins
- Privileged role activations
- Unusual administrative activity

---

# Use Emergency Access Accounts

Maintain a small number of emergency ("break-glass") administrator accounts.

Recommendations:

- Protect with strong credentials.
- Exclude from Conditional Access policies that could cause lockout.
- Monitor continuously.
- Test periodically.

Emergency accounts should only be used when normal administrative access is unavailable.

---

# Design Emergency Access Accounts Correctly

Emergency access ("break-glass") accounts provide administrative access when normal authentication mechanisms are unavailable.

Microsoft recommends maintaining at least two emergency accounts.

Best practices include:

- Create cloud-only accounts in Microsoft Entra ID.
- Do not synchronize them from on-premises Active Directory.
- Protect them with strong credentials.
- Monitor every sign-in.
- Test them periodically.
- Store credentials securely.
- Exclude them from Conditional Access policies that could prevent emergency access.

These accounts should only be used during exceptional circumstances such as identity outages or Conditional Access misconfigurations.

> [!IMPORTANT]
> Emergency access accounts should remain isolated from everyday administration and be continuously monitored to detect unauthorized use.

---

# Enterprise Scenario

A multinational company manages hundreds of Azure subscriptions.

Administrators implement:

- Microsoft Entra ID as the central identity provider.
- Conditional Access requiring MFA.
- PIM for privileged roles.
- Azure RBAC following least privilege.
- Managed Identities for Azure workloads.
- Azure Key Vault for secrets.
- Group-based RBAC assignments.
- Quarterly access reviews.
- Emergency access accounts for disaster recovery.

This architecture minimizes credential exposure while maintaining secure and scalable identity management.

---

# Best Practices Checklist

- Follow Zero Trust.
- Enforce MFA.
- Apply Conditional Access.
- Use least privilege.
- Separate Microsoft Entra ID roles from Azure RBAC roles.
- Use PIM instead of permanent administrator roles.
- Protect secrets with Azure Key Vault.
- Use Managed Identities.
- Assign permissions to groups.
- Apply roles at the lowest possible scope.
- Review access regularly.
- Protect privileged accounts.
- Monitor identity activity.
- Maintain emergency access accounts.

---

# Common Pitfalls

- Assigning Owner unnecessarily.
- Using permanent administrator roles.
- Disabling or bypassing MFA.
- Mixing Microsoft Entra ID roles with Azure RBAC roles.
- Storing credentials in source code.
- Assigning permissions directly to users instead of groups.
- Leaving inactive guest accounts enabled.
- Ignoring access reviews.
- Using privileged accounts for everyday activities.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Microsoft Entra ID
> - Azure RBAC
> - Least privilege
> - Conditional Access
> - Multi-Factor Authentication
> - Managed Identities
> - Privileged Identity Management
> - Azure Key Vault integration
> - Group-based access control
> - Zero Trust
> - Identity governance

---

# Key Takeaways

- Identity security is the foundation of Azure security and should follow Microsoft's Zero Trust model by continuously validating every authentication and authorization request.
- Microsoft Entra ID, Azure RBAC, Conditional Access, MFA, Managed Identities, and Privileged Identity Management work together to protect identities and control access to Azure resources.
- Organizations should enforce least privilege, separate directory administration from resource administration, protect secrets with Azure Key Vault, and use Managed Identities whenever possible.
- Regular access reviews, group-based role assignments, dedicated administrative accounts, and continuous monitoring significantly reduce the risk of identity compromise.
- Mastering Azure identity security best practices is essential for secure Azure administration and is a key objective of the AZ-104 certification.

---

# References

| Microsoft Documentation | URL |
|-------------------------|-----|
| Microsoft Entra ID | https://learn.microsoft.com/entra/fundamentals/ |
| Azure RBAC | https://learn.microsoft.com/azure/role-based-access-control/overview |
| Conditional Access | https://learn.microsoft.com/entra/identity/conditional-access/overview |
| Microsoft Entra MFA | https://learn.microsoft.com/entra/identity/authentication/concept-mfa-howitworks |
| Managed Identities | https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview |
| Privileged Identity Management | https://learn.microsoft.com/entra/id-governance/privileged-identity-management/ |
| Azure Key Vault | https://learn.microsoft.com/azure/key-vault/general/overview |
| Microsoft Learn – Secure access to Azure resources | https://learn.microsoft.com/training/modules/secure-access-azure-resources/ |
