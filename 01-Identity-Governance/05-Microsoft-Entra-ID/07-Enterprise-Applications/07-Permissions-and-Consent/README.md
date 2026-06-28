# Permissions and Consent

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra ID controls application permissions and how users or administrators grant consent to Enterprise Applications.

---

## Permission Model

```text
          Enterprise Application
                   │
                   ▼
          Requests Permissions
                   │
                   ▼
        Microsoft Entra ID
                   │
        ┌──────────┴──────────┐
        │                     │
        ▼                     ▼
   User Consent        Admin Consent
        │                     │
        └──────────┬──────────┘
                   ▼
          Access Token Issued
                   │
                   ▼
          Protected Resource
```

---

> [!TIP]
> **Key Concepts**
>
> - Enterprise Applications request permissions to access protected resources.
> - Consent determines whether requested permissions are granted.
> - Some permissions require administrator approval.
> - API permissions and Azure RBAC are different authorization models.
> - Consent is managed independently by each tenant.

---

## Overview

Enterprise Applications frequently require access to Microsoft services, Azure resources, or custom APIs.

Before access is granted, Microsoft Entra ID evaluates whether the requested permissions have been approved through the consent framework.

This ensures organizations retain full control over which applications can access their resources.

---

## API Permissions

Enterprise Applications commonly request access to:

- Microsoft Graph
- Microsoft 365 services
- Azure Resource Manager
- Azure Key Vault
- Custom APIs

Permissions are declared by the application and evaluated whenever an Access Token is requested.

---

## Permission Types

Microsoft Entra ID supports two permission models.

| Permission Type | Description |
|-----------------|-------------|
| **Delegated Permissions** | The application acts on behalf of a signed-in user. |
| **Application Permissions** | The application acts without a signed-in user. |

The selected permission model depends on the application's architecture.

---

## Delegated Permissions

Delegated permissions require an authenticated user.

The application's effective permissions are limited by:

- The user's privileges.
- The delegated permissions granted to the application.

```text
Effective Permissions
        =
User Privileges
        ∩
Delegated Permissions
```

The application cannot perform operations that the signed-in user is not allowed to perform.

---

## Application Permissions

Application permissions are used when no interactive user is present.

Typical scenarios include:

- Background services
- Scheduled automation
- Azure Automation
- Azure Functions
- Daemon applications

Because these permissions can grant broad access, administrator consent is usually required.

---

## User Consent

User Consent allows individual users to approve delegated permissions for their own accounts.

Whether users are allowed to grant consent depends on the organization's Microsoft Entra ID consent policies.

Organizations commonly restrict User Consent to reduce security risks associated with third-party applications.

---

## Administrator Consent

Administrator Consent grants permissions for the entire tenant.

Typical administrative roles that can grant tenant-wide consent include:

- Global Administrator
- Application Administrator
- Cloud Application Administrator

Once administrator consent has been granted, users are no longer prompted individually for those permissions.

---

## Admin Consent Workflow

Organizations can enable the **Admin Consent Workflow**.

If users attempt to access an application that requires administrator approval, Microsoft Entra ID can generate a consent request instead of immediately denying access.

The workflow includes:

- Business justification submitted by the user.
- Designated reviewers.
- Email notifications.
- Request expiration.

This allows organizations to centralize approval while avoiding unnecessary administrator involvement during daily operations.

---

## Azure RBAC vs API Permissions

API permissions authorize access to protected APIs such as Microsoft Graph.

Azure RBAC authorizes management of Azure resources.

| API Permissions | Azure RBAC |
|-----------------|------------|
| Microsoft Graph | Azure Resources |
| Access Tokens | Azure Role Assignments |
| Microsoft Entra ID | Azure Resource Manager |
| OAuth 2.0 permissions | Azure built-in or custom roles |

Although both models control authorization, they operate independently.

---

## Consent Evaluation

```text
Application Requests Permission
              │
              ▼
Microsoft Entra ID
              │
              ▼
Permission Already Granted?
      │                  │
      ▼                  ▼
    Yes                  No
      │                  │
      ▼                  ▼
 Issue Token      User/Admin Consent
      │                  │
      └──────────┬───────┘
                 ▼
          Protected Resource
```

---

## Enterprise Scenario

A third-party reporting application requires access to Microsoft Graph.

The application requests delegated permissions to read user profiles.

Because the organization has disabled User Consent, Microsoft Entra ID generates an administrator consent request.

After approval, all authorized users can access the application without additional consent prompts.

---

## Best Practices

- Apply the principle of least privilege.
- Review granted permissions regularly.
- Restrict User Consent when appropriate.
- Enable the Admin Consent Workflow.
- Audit administrator consent periodically.
- Remove unused API permissions.

---

## Common Pitfalls

- Confusing API permissions with Azure RBAC.
- Granting excessive permissions.
- Forgetting to review administrator consent.
- Assuming delegated permissions bypass user privileges.
- Allowing unrestricted User Consent without governance.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - API Permissions
> - Delegated Permissions
> - Application Permissions
> - User Consent
> - Administrator Consent
> - Admin Consent Workflow
> - Azure RBAC versus API Permissions

---

## Key Takeaways

- Consent controls whether Enterprise Applications receive requested permissions.
- Delegated Permissions depend on the signed-in user.
- Application Permissions are used without user interaction.
- Administrator Consent grants permissions across the tenant.
- Azure RBAC and API Permissions are independent authorization models.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Microsoft identity platform permissions and consent overview](https://learn.microsoft.com/entra/identity-platform/permissions-consent-overview) | Permissions and consent framework |
| [Configure user consent settings](https://learn.microsoft.com/entra/identity/enterprise-apps/configure-user-consent) | User Consent policies |
| [Configure the admin consent workflow](https://learn.microsoft.com/entra/identity/enterprise-apps/configure-admin-consent-workflow) | Admin Consent Workflow |
| [Assign Azure roles using Azure RBAC](https://learn.microsoft.com/azure/role-based-access-control/role-assignments-portal) | Azure RBAC |
| [Microsoft Learn – Permissions and consent](https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/) | Microsoft Learn module |
