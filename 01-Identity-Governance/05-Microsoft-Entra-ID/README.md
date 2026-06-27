# Microsoft Entra ID

> [!NOTE]
> This section covers Microsoft Entra ID concepts required for the Microsoft AZ-104 certification and for working as an Azure Administrator or Cloud Engineer.
>
> Microsoft Entra ID is the identity and access management platform used across Azure. Understanding how identities, authentication, authorization, and access control work is essential before managing Azure resources securely.

---

## Learning Path

| Topic | Status | Description |
|--------|:------:|-------------|
| [01 - Tenant and Identity](./01-Tenant-and-Identity/) | ⬜ | Understand tenants, directories and identity concepts. |
| [02 - Authentication](./02-Authentication/) | ⬜ | Learn how Microsoft Entra ID authenticates users and workloads. |
| [03 - Authorization](./03-Authorization/) | ⬜ | Understand Azure RBAC and access control concepts. |
| [04 - Users](./04-Users/) | ⬜ | Create and manage cloud, guest and synchronized users. |
| [05 - Groups](./05-Groups/) | ⬜ | Manage Security Groups and Microsoft 365 Groups. |
| [06 - App Registrations](./06-App-Registrations/) | ⬜ | Register applications in Microsoft Entra ID. |
| [07 - Enterprise Applications](./07-Enterprise-Applications/) | ⬜ | Manage SaaS applications and service integrations. |
| [08 - Service Principals](./08-Service-Principals/) | ⬜ | Understand application identities used in Azure. |
| [09 - Managed Identities](./09-Managed-Identities/) | ⬜ | Secure Azure resources without storing credentials. |
| [10 - Devices](./10-Devices/) | ⬜ | Register and manage devices in Microsoft Entra ID. |
| [11 - Hybrid Identity](./11-Hybrid-Identity/) | ⬜ | Understand hybrid identity architectures. |
| [12 - Microsoft Entra Connect](./12-Microsoft-Entra-Connect/) | ⬜ | Synchronize on-premises Active Directory with Microsoft Entra ID. |
| [13 - Multi-Factor Authentication (MFA)](./13-MFA/) | ⬜ | Strengthen authentication using MFA. |
| [14 - Conditional Access](./14-Conditional-Access/) | ⬜ | Control access based on conditions and risk. |
| [15 - Administrative Roles](./15-Administrative-Roles/) | ⬜ | Learn the built-in administrative roles in Microsoft Entra ID. |

---

## Microsoft Entra ID Overview

```text
                        Microsoft Entra ID
                                │
                           Entra Tenant
                                │
       ┌──────────┬──────────┬──────────┬──────────┐
       │          │          │          │          │
     Users     Groups    Devices   Applications  Identities
                                                │
                                   ┌────────────┴────────────┐
                                   │                         │
                          Service Principals     Managed Identities
```

---

## Learning Objectives

After completing this section, you should be able to:

- Explain the role of Microsoft Entra ID in Azure.
- Understand authentication and authorization.
- Manage identities securely.
- Configure user and group access.
- Secure Azure resources using RBAC and Managed Identities.
- Understand hybrid identity scenarios.
- Configure authentication security features such as MFA and Conditional Access.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| https://learn.microsoft.com/entra/ | Microsoft Entra documentation |
| https://learn.microsoft.com/training/browse/?products=entra | Microsoft Learn |
| https://learn.microsoft.com/azure/role-based-access-control/overview | Azure RBAC |
