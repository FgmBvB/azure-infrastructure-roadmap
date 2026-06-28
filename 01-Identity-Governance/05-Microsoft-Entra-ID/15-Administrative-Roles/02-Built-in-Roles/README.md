# Microsoft Entra Built-in Administrative Roles

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains the most important built-in administrative roles in Microsoft Entra ID and their responsibilities for the AZ-104 certification.

---

## Built-in Roles Overview

```text
              Microsoft Entra ID
                     │
                     ▼
          Built-in Administrative Roles
                     │
 ┌──────────┬──────────┬──────────┬──────────┐
 │          │          │          │
 ▼          ▼          ▼          ▼
Identity   Users    Applications Security
                     │
                     ▼
               Devices & Intune
```

---

> [!TIP]
> **Key Concepts**
>
> - Microsoft Entra ID provides predefined administrative roles.
> - Each role grants only the permissions required for a specific administrative function.
> - Built-in roles simplify administration while following the principle of least privilege.
> - Global Administrator should be assigned only when absolutely necessary.
> - Most organizations use multiple specialized roles instead of one highly privileged role.

---

## Overview

Microsoft Entra ID includes dozens of built-in administrative roles.

Each role is designed for a specific operational responsibility and grants only the permissions required to perform that job.

Using specialized roles reduces security risks and simplifies governance.

---

## Most Common Administrative Roles

| Role | Primary Responsibility |
|------|-------------------------|
| **Global Administrator** | Full administrative control over Microsoft Entra ID. |
| **User Administrator** | Manage users, reset passwords, and manage user properties. |
| **Groups Administrator** | Manage Microsoft Entra groups and memberships. |
| **Helpdesk Administrator** | Reset passwords for non-administrative users and provide user support. |
| **Authentication Administrator** | Manage authentication methods for users. |
| **Privileged Authentication Administrator** | Manage authentication methods for privileged accounts. |
| **Cloud Application Administrator** | Manage Enterprise Applications and Application Registrations. |
| **Application Administrator** | Manage application registrations without broader application administration permissions. |
| **Security Administrator** | Configure and manage Microsoft security settings. |
| **Security Reader** | View security information without making changes. |
| **Global Reader** | Read tenant-wide configuration without administrative permissions. |
| **Cloud Device Administrator** | Manage Microsoft Entra registered, joined, and hybrid joined devices. |
| **Intune Administrator** | Manage Microsoft Intune and device management policies. |
| **Billing Administrator** | Manage subscriptions, licenses, and billing information. |

---

## Global Administrator

The **Global Administrator** role provides unrestricted administrative access across Microsoft Entra ID.

Responsibilities include:

- Manage all users and groups.
- Manage applications.
- Configure Conditional Access.
- Assign administrative roles.
- Configure authentication methods.
- Manage tenant-wide settings.

Microsoft recommends limiting the number of Global Administrators.

---

## User Administrator

User Administrators manage user identities.

Typical responsibilities include:

- Create users.
- Update user properties.
- Reset passwords.
- Manage licenses.
- Manage user lifecycle.

They cannot perform tenant-wide administrative tasks.

---

### Helpdesk Administrator vs User Administrator

Although both roles can perform password-related operations, their permissions are different.

| Capability | Helpdesk Administrator | User Administrator |
|------------|------------------------|--------------------|
| Reset passwords for standard users | Yes | Yes |
| Reset passwords for Helpdesk Administrators | No | Yes |
| Reset passwords for User Administrators | No | Yes |
| Reset passwords for privileged administrators (for example, Global Administrator) | No | No |

The Helpdesk Administrator role is intended for first-line support and cannot manage privileged administrative accounts.

The User Administrator role has broader user management capabilities but is still restricted from managing highly privileged administrator accounts.

## Groups Administrator

---

Groups Administrators manage:

- Security Groups.
- Microsoft 365 Groups.
- Group memberships.
- Group ownership.

This role is commonly delegated to collaboration teams.

---

## Cloud Application Administrator

Cloud Application Administrators manage:

- Enterprise Applications.
- Application Registrations.
- Single Sign-On (SSO).
- Application permissions.
- Provisioning configuration.

They cannot assign administrative roles.

---

### Application Administrator vs Cloud Application Administrator

Both roles can manage application registrations and enterprise applications.

The primary difference is the scope of administration.

| Capability | Application Administrator | Cloud Application Administrator |
|------------|--------------------------|---------------------------------|
| Manage App Registrations | Yes | Yes |
| Manage Enterprise Applications | Limited | Yes |
| Configure Single Sign-On | Limited | Yes |
| Manage application credentials (where permitted) | Limited | Yes |

Cloud Application Administrator provides broader permissions for enterprise application management, including Single Sign-On and application configuration across the tenant.

Application Administrator is typically assigned when organizations want to delegate application management with fewer permissions.

---

## Authentication Administrator

Authentication Administrators manage user authentication methods.

Examples include:

- Microsoft Authenticator.
- FIDO2 Security Keys.
- Temporary Access Pass.
- Password reset operations.

They cannot modify broader security policies.

---

## Authentication Administrator vs Privileged Authentication Administrator

Both roles manage authentication methods, but they differ in the scope of users they can administer.

| Capability | Authentication Administrator | Privileged Authentication Administrator |
|------------|-----------------------------|------------------------------------------|
| Manage authentication methods for standard users | Yes | Yes |
| Reset passwords for standard users | Yes | Yes |
| Manage authentication methods for privileged administrators | No | Yes |
| Reset authentication methods for privileged administrators | No | Yes |

Because the **Privileged Authentication Administrator** can manage authentication methods for highly privileged accounts, Microsoft considers it a highly sensitive administrative role.

Organizations should assign this role only to trusted administrators and protect it with Multi-Factor Authentication and Privileged Identity Management (PIM).

---

## Security Administrator

Security Administrators manage identity security features.

Examples include:

- Microsoft Defender integrations.
- Identity Protection.
- Security policies.
- Authentication security settings.

---

## Global Reader

Global Readers have read-only access across Microsoft Entra ID.

They can review:

- Users
- Groups
- Applications
- Security settings
- Administrative configuration

This role is useful for auditors.

---

## Cloud Device Administrator

Cloud Device Administrators manage:

- Microsoft Entra Joined devices.
- Microsoft Entra Registered devices.
- Hybrid Joined devices.
- Device lifecycle operations.
- BitLocker Recovery Keys (supported scenarios).

---

## Intune Administrator

Intune Administrators manage:

- Device enrollment.
- Compliance policies.
- Configuration profiles.
- Mobile application management.
- Endpoint security configuration.

---

## Billing Administrator

Billing Administrators manage:

- Azure subscriptions.
- Microsoft subscriptions.
- License assignments.
- Billing information.

They do not receive identity administration permissions.

---

## Choosing the Correct Role

```text
Need full tenant control?
        │
   Yes ─┴─ No
    │       │
Global     Select the
Admin      smallest role
               │
               ▼
      Least Privilege
```

---

## Enterprise Scenario

A company assigns administrative responsibilities according to operational roles.

Helpdesk staff receive the **Helpdesk Administrator** role, application engineers receive the **Cloud Application Administrator** role, security personnel receive the **Security Administrator** role, and only two infrastructure administrators permanently hold the **Global Administrator** role.

This separation of duties reduces operational risk while following Microsoft's least-privilege recommendations.

---

## Best Practices

- Assign the least privileged role possible.
- Limit the number of Global Administrators.
- Use specialized administrative roles.
- Protect privileged roles with MFA.
- Use Privileged Identity Management (PIM) where available.
- Review role assignments regularly.

---

## Common Pitfalls

- Assigning Global Administrator unnecessarily.
- Giving multiple overlapping administrative roles.
- Using Global Administrator for daily administration.
- Forgetting periodic access reviews.
- Not protecting privileged accounts with MFA.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Global Administrator
> - User Administrator
> - Groups Administrator
> - Cloud Application Administrator
> - Authentication Administrator
> - Security Administrator
> - Global Reader
> - Cloud Device Administrator
> - Intune Administrator
> - Least privilege

---

## Key Takeaways

- Microsoft Entra ID includes numerous built-in administrative roles.
- Each role is designed for a specific administrative responsibility.
- Global Administrator should be assigned sparingly.
- Specialized roles improve security through least privilege.
- Regular reviews help maintain secure administrative access.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Microsoft Entra built-in roles](https://learn.microsoft.com/entra/identity/role-based-access-control/permissions-reference) | Complete built-in roles reference |
| [Assign Microsoft Entra roles](https://learn.microsoft.com/entra/identity/role-based-access-control/manage-roles-portal) | Assigning administrative roles |
| [Administrative Units](https://learn.microsoft.com/entra/identity/role-based-access-control/administrative-units) | Delegated administration |
| [Microsoft Entra Privileged Identity Management](https://learn.microsoft.com/entra/id-governance/privileged-identity-management/pim-configure) | Just-in-Time administration |
| [Microsoft Learn – Manage Microsoft Entra permissions by using RBAC](https://learn.microsoft.com/training/modules/manage-permissions-entra-id/) | Microsoft Learn module |
