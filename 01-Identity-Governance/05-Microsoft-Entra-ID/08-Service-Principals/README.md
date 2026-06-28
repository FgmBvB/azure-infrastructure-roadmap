# Microsoft Entra ID

> [!NOTE]
> This section is part of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
>
> It covers the identity and access management capabilities provided by Microsoft Entra ID, following the Microsoft Learn learning path and official Microsoft documentation.

---

## Overview

Microsoft Entra ID is Microsoft's cloud-based Identity and Access Management (IAM) platform.

It enables organizations to manage identities, secure authentication, control authorization, protect applications, and govern access to Azure resources and third-party services.

Understanding Microsoft Entra ID is fundamental for Azure administrators because almost every Azure service relies on identity-based security.

---

## Learning Objectives

This section follows the official Microsoft Learn objectives for the AZ-104 certification.

Topics include:

- Microsoft Entra tenants
- Identity management
- Authentication
- Authorization
- Users and groups
- App Registrations
- Enterprise Applications
- Service Principals
- Managed Identities
- Devices
- Hybrid Identity
- Microsoft Entra Connect
- Multi-Factor Authentication (MFA)
- Conditional Access
- Administrative Roles

---

## Skills Covered

After completing this section, you should understand how to:

- Manage Microsoft Entra tenants.
- Create and manage users and groups.
- Configure authentication and authorization.
- Secure applications and identities.
- Deploy and manage application identities.
- Implement Conditional Access and MFA.
- Configure hybrid identity.
- Manage administrative roles.
- Troubleshoot authentication and access issues.

---

## Directory Structure

```text
05-Microsoft-Entra-ID
│
├── 01-Tenant-and-Identity
├── 02-Authentication
├── 03-Authorization
├── 04-Users
├── 05-Groups
├── 06-App-Registrations
├── 07-Enterprise-Applications
├── 08-Service-Principals
├── 09-Managed-Identities
├── 10-Devices
├── 11-Hybrid-Identity
├── 12-Microsoft-Entra-Connect
├── 13-MFA
├── 14-Conditional-Access
└── 15-Administrative-Roles
```

---

## AZ-104 Focus

> [!IMPORTANT]
>
> You should understand:
>
> - Microsoft Entra architecture
> - Identity lifecycle management
> - Authentication methods
> - Authorization models
> - Application identities
> - Enterprise Applications
> - Service Principals
> - Managed Identities
> - Hybrid Identity
> - Conditional Access
> - Multi-Factor Authentication
> - Administrative roles

---

## Key Takeaways

- Microsoft Entra ID is Azure's Identity and Access Management platform.
- Identity is the security foundation of Azure.
- Authentication verifies identity.
- Authorization determines resource access.
- Applications authenticate using App Registrations and Service Principals.
- Conditional Access and MFA strengthen identity security.
- Managed Identities eliminate the need to store credentials.
- Hybrid identity integrates on-premises Active Directory with Microsoft Entra ID.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| https://learn.microsoft.com/training/paths/az-104-manage-identities-governance-azure/ | Official AZ-104 Microsoft Learn learning path |
| https://learn.microsoft.com/entra/ | Microsoft Entra documentation |
| https://learn.microsoft.com/entra/fundamentals/whatis | Microsoft Entra overview |
| https://learn.microsoft.com/entra/identity/ | Identity management documentation |
| https://learn.microsoft.com/azure/architecture/guide/security/identity-management | Azure identity architecture |
