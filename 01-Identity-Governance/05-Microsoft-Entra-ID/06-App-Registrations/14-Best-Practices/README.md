# Best Practices

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It summarizes Microsoft's recommended best practices for securely managing App Registrations in Microsoft Entra ID.

---

## Secure Application Lifecycle

```text
        Register Application
                │
                ▼
      Configure Authentication
                │
                ▼
      Configure Authorization
                │
                ▼
      Protect Credentials
                │
                ▼
      Monitor & Audit
                │
                ▼
      Review Permissions
                │
                ▼
      Remove Unused Apps
```

---

> [!TIP]
> **Key Concepts**
>
> - Apply the principle of least privilege.
> - Prefer modern authentication methods.
> - Protect application credentials.
> - Review permissions regularly.
> - Remove unused applications.

---

## Overview

App Registrations are security identities that often have access to critical Microsoft 365 services, Azure resources, and custom APIs.

Misconfigured applications can become a significant security risk.

Following Microsoft's security recommendations helps reduce the attack surface while improving governance and operational security.

---

## Authentication

Microsoft recommends using the most secure authentication method available.

Authentication preference:

| Method | Recommendation |
|---------|----------------|
| Managed Identity | Recommended for Azure resources |
| Workload Identity Federation | Recommended for external workloads |
| Certificates | Preferred over Client Secrets |
| Client Secrets | Use only when necessary |

Avoid long-lived credentials whenever possible.

---

## Authorization

Applications should receive only the permissions required to perform their tasks.

Recommendations:

- Apply the principle of least privilege.
- Prefer Delegated Permissions when possible.
- Use Application Permissions only when required.
- Review API permissions periodically.
- Remove unnecessary permissions.

---

## Consent

Administrator consent should be carefully controlled.

Recommendations:

- Limit User Consent according to organizational policies.
- Review tenant-wide Admin Consent regularly.
- Use the Admin Consent Workflow when appropriate.
- Monitor newly approved applications.

---

## Credentials

Protect all application credentials.

Recommendations:

- Prefer certificates over Client Secrets.
- Rotate secrets before expiration.
- Store secrets in Azure Key Vault.
- Monitor credential expiration dates.
- Remove unused credentials.

---

## Redirect URIs

Incorrect Redirect URI configuration can introduce security risks.

Recommendations:

- Register only required Redirect URIs.
- Use HTTPS in production.
- Remove obsolete Redirect URIs.
- Validate Redirect URI configuration regularly.

---

## API Permissions

Applications should expose and consume APIs securely.

Recommendations:

- Define only necessary Scopes.
- Use App Roles for application-to-application authorization.
- Require administrator consent for privileged permissions.
- Review exposed APIs periodically.

---

## Monitoring

Application identities should be continuously monitored.

Recommendations:

- Audit sign-in logs.
- Monitor application activity.
- Review Service Principals regularly.
- Detect unused App Registrations.
- Remove abandoned applications.

---

## Enterprise Scenario

A company develops several internal business applications.

Instead of using Client Secrets stored in configuration files, the applications authenticate using Managed Identities or Workload Identity Federation whenever possible.

Permissions are granted following the principle of least privilege, administrator consent is reviewed periodically, and all credentials are monitored for expiration.

This approach reduces operational risk while improving security and governance.

---

## Common Pitfalls

- Using Client Secrets when Managed Identities are available.
- Granting excessive API permissions.
- Leaving expired credentials configured.
- Forgetting to review Admin Consent.
- Reusing the same App Registration for unrelated applications.
- Leaving unused Redirect URIs configured.
- Never reviewing application permissions.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Least privilege
> - Modern authentication methods
> - Credential management
> - API permission management
> - Consent governance
> - Application lifecycle management

---

## Key Takeaways

- Protect application identities.
- Prefer passwordless authentication whenever possible.
- Grant only the required permissions.
- Rotate and monitor credentials.
- Review App Registrations regularly.
- Remove unused applications to reduce security risks.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Microsoft identity platform documentation](https://learn.microsoft.com/entra/identity-platform/) | Identity platform guidance |
| [Security best practices for Microsoft Entra ID](https://learn.microsoft.com/entra/identity/role-based-access-control/security-planning) | Security recommendations |
| [Managed identities for Azure resources](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview) | Passwordless authentication |
| [Workload identity federation](https://learn.microsoft.com/entra/workload-id/workload-identity-federation) | Federated authentication |
| [Microsoft Learn – Build applications that authenticate users](https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/) | Microsoft Learn module |
