# Best Practices

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It summarizes the recommended practices for securely managing Enterprise Applications in Microsoft Entra ID.

---

## Security Lifecycle

```text
        Enterprise Application
                 │
                 ▼
        User Assignments
                 │
                 ▼
     Conditional Access Policies
                 │
                 ▼
      Least Privilege Permissions
                 │
                 ▼
     Monitoring & Audit Logs
                 │
                 ▼
 Credential Rotation & Review
                 │
                 ▼
 Continuous Governance
```

---

> [!TIP]
> **Key Concepts**
>
> - Apply the principle of least privilege.
> - Restrict application access through assignments.
> - Protect applications with Conditional Access.
> - Monitor authentication and administrative activity.
> - Review permissions and credentials regularly.

---

## Overview

Enterprise Applications often provide access to critical business resources.

Proper governance reduces security risks, improves operational efficiency, and helps organizations maintain compliance with security and regulatory requirements.

Security should be considered throughout the entire application lifecycle.

---

## Restrict Access

Only authorized users should be able to access Enterprise Applications.

Microsoft recommends:

- Enable **Assignment required?**
- Assign groups instead of individual users.
- Remove unused assignments.
- Review assignments periodically.

---

## Apply Least Privilege

Grant only the permissions required.

Avoid assigning:

- Excessive API permissions.
- Unnecessary Azure RBAC roles.
- Global administrative roles.

Permissions should be reviewed regularly to minimize security risks.

---

## Protect Authentication

Protect Enterprise Applications using Microsoft Entra security features.

Recommended controls include:

- Multi-Factor Authentication (MFA)
- Conditional Access
- Passwordless authentication
- Identity Protection
- Risk-based policies

Authentication policies should reflect the organization's security requirements.

---

## Block Legacy Authentication

Legacy authentication protocols such as:

- IMAP
- POP3
- SMTP AUTH
- Older Office clients

do not support modern authentication features such as Multi-Factor Authentication (MFA).

Microsoft recommends blocking legacy authentication through **Conditional Access** by targeting legacy client applications.

Blocking these protocols significantly reduces the risk of password spraying and credential-based attacks.

---

## Secure Credentials

Applications should avoid long-lived credentials whenever possible.

Microsoft recommends:

- Use Managed Identities for Azure resources.
- Store secrets in Azure Key Vault.
- Prefer certificates over client secrets.
- Rotate credentials before expiration.
- Remove unused certificates and secrets.

---

## Monitor Activity

Administrators should continuously monitor:

- Sign-in Logs.
- Audit Logs.
- Provisioning Logs.
- Conditional Access results.
- Administrator consent.
- Credential expiration.

Monitoring enables early detection of security issues and configuration errors.

---

## Review Enterprise Applications

Organizations should periodically review:

- Unused applications.
- Disabled applications.
- Excessive permissions.
- Expired credentials.
- Stale user assignments.
- Legacy authentication methods.

Removing unnecessary applications reduces the attack surface.

---

## Access Reviews

Organizations should periodically validate who still requires access to Enterprise Applications.

Microsoft Entra ID **Access Reviews** automate this process by allowing administrators or Application Owners to review user and group assignments on a scheduled basis.

Typical review schedules include:

- Monthly
- Quarterly
- Annually

If access is no longer required, Microsoft Entra ID can automatically remove the assignment, helping prevent privilege creep and reducing unnecessary access.

---

## Governance

Enterprise Applications should follow a defined governance process.

Recommended activities include:

- Assign Application Owners.
- Document application purpose.
- Review permissions periodically.
- Audit administrator consent.
- Remove unused applications.
- Validate business ownership.

Good governance improves accountability and simplifies audits.

---

## Tenant Restrictions

Organizations may implement **Tenant Restrictions** to control which Microsoft Entra ID tenants users can access.

This helps ensure that users authenticate only to approved organizational tenants and prevents the use of unmanaged external tenants for business applications.

Tenant Restrictions support organizational governance and help reduce the risk of data exfiltration through unauthorized external tenants.

---

## Lifecycle Management

Application management should include the full lifecycle.

```text
Register
    │
    ▼
Deploy
    │
    ▼
Assign Users
    │
    ▼
Protect
    │
    ▼
Monitor
    │
    ▼
Review
    │
    ▼
Retire
```

Applications that are no longer required should be removed promptly.

---

## Enterprise Scenario

A company reviews its Enterprise Applications every quarter.

Administrators identify unused applications, remove unnecessary permissions, rotate expiring certificates, verify application owners, and validate Conditional Access policies.

This periodic review improves security while reducing operational risk.

---

## Best Practices Checklist

- Enable **Assignment required?**
- Assign groups instead of individual users.
- Apply Conditional Access policies.
- Enforce Multi-Factor Authentication (MFA).
- Apply the principle of least privilege.
- Use Managed Identities whenever possible.
- Store secrets in Azure Key Vault.
- Rotate certificates and secrets regularly.
- Monitor Sign-in, Audit, and Provisioning Logs.
- Review administrator consent periodically.
- Remove unused Enterprise Applications.
- Assign Application Owners.
- Audit permissions regularly.
- Document business ownership.
- Remove legacy authentication where possible.

---

## Common Pitfalls

- Leaving applications accessible to all users.
- Granting excessive API permissions.
- Forgetting credential rotation.
- Ignoring monitoring and audit logs.
- Keeping unused Enterprise Applications.
- Not reviewing administrator consent.
- Missing business ownership documentation.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Least privilege
> - User assignments
> - Conditional Access
> - Monitoring
> - Credential management
> - Governance
> - Lifecycle management

---

## Key Takeaways

- Enterprise Applications should follow the principle of least privilege.
- Authentication should be protected with Conditional Access and MFA.
- Credentials require regular rotation and monitoring.
- Continuous monitoring improves security and compliance.
- Governance is an ongoing process throughout the application lifecycle.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Best practices for managing application access](https://learn.microsoft.com/entra/identity/enterprise-apps/secure-service-principal) | Enterprise Application security |
| [Application management best practices](https://learn.microsoft.com/entra/identity/enterprise-apps/what-is-application-management) | Application governance |
| [Conditional Access overview](https://learn.microsoft.com/entra/identity/conditional-access/overview) | Conditional Access |
| [Managed identities for Azure resources](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview) | Managed Identities |
| [Microsoft Learn – Secure application access](https://learn.microsoft.com/training/modules/secure-applications/) | Microsoft Learn module |
