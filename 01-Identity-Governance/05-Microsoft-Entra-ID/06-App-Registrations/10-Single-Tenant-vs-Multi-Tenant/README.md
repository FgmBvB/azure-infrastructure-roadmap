# Single-Tenant vs Multi-Tenant

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra ID determines which organizations or users can authenticate to an application through the Supported Account Types configuration.

---

## Tenant Scope

```text
                 App Registration
                        │
        Supported Account Types
                        │
      ┌─────────────────┴─────────────────┐
      │                                   │
      ▼                                   ▼
 Single-Tenant                     Multi-Tenant
      │                                   │
      ▼                                   ▼
 One Microsoft                  Multiple Microsoft
 Entra ID Tenant                Entra ID Tenants
```

---

> [!TIP]
> **Key Concepts**
>
> * Supported Account Types determine who can sign in to an application.
> * Single-Tenant applications are limited to one Microsoft Entra ID tenant.
> * Multi-Tenant applications can be used by multiple organizations.
> * External tenants receive their own Service Principal.
> * The Application Object always remains in the home tenant.

---

## Overview

When registering an application, administrators choose the **Supported Account Types**.

This setting determines which identities are allowed to authenticate to the application.

Choosing the correct tenant scope is an important architectural decision because it affects authentication, administration, and application distribution.

---

## Supported Account Types

Microsoft Entra ID provides four supported account types.

| Supported Account Type                                                   | Description                                    |
| ------------------------------------------------------------------------ | ---------------------------------------------- |
| Accounts in this organizational directory only                           | Single-Tenant application.                     |
| Accounts in any organizational directory                                 | Multi-Tenant application.                      |
| Accounts in any organizational directory and personal Microsoft accounts | Multi-Tenant plus Microsoft personal accounts. |
| Personal Microsoft accounts only                                         | Consumer Microsoft accounts only.              |

---

## Single-Tenant Applications

A Single-Tenant application accepts authentication requests only from identities that belong to its home Microsoft Entra ID tenant.

This model is commonly used for:

* Internal business applications
* Enterprise administration tools
* Corporate APIs
* Internal automation

Because authentication is limited to one organization, administration is generally simpler.

---

## Multi-Tenant Applications

A Multi-Tenant application can be used by multiple Microsoft Entra ID tenants.

When a user from another organization signs in for the first time, Microsoft Entra ID creates a **Service Principal** in that customer's tenant.

The Application Object remains only in the home tenant, while each customer tenant maintains its own local Service Principal.

---

## Identity Model

```text
              Home Tenant
                   │
        Application Object
                   │
      ┌────────────┼────────────┐
      │            │            │
      ▼            ▼            ▼
Tenant A      Tenant B      Tenant C
      │            │            │
Service       Service       Service
Principal     Principal     Principal
```

Each tenant independently manages its own Service Principal, including permissions, Conditional Access policies, and Azure RBAC assignments.

---

## Consent in Multi-Tenant Applications

Applications do not automatically receive permissions in external tenants.

Each organization must grant the required permissions through the Microsoft Entra ID consent process.

Depending on the requested permissions:

* Users may grant User Consent.
* Administrators may grant Admin Consent.

This ensures that every organization maintains control over its own resources.

---

## Choosing the Right Model

| Scenario                        | Recommended Model                                                  |
| ------------------------------- | ------------------------------------------------------------------ |
| Internal HR application         | Single-Tenant                                                      |
| Company intranet                | Single-Tenant                                                      |
| SaaS application                | Multi-Tenant                                                       |
| Commercial business application | Multi-Tenant                                                       |
| Consumer application            | Personal Microsoft accounts or Multi-Tenant with personal accounts |

---

## Security Considerations

Single-Tenant applications reduce exposure because only one organization can authenticate.

Multi-Tenant applications require additional planning because multiple organizations can create Service Principals and grant permissions.

Administrators should always:

* Apply least privilege.
* Review granted permissions.
* Review tenant-wide consent.
* Monitor external tenant access.

---

## Enterprise Scenario

A software company develops a SaaS inventory management platform.

The application is registered as a **Multi-Tenant** application.

Each customer signs in using its own Microsoft Entra ID tenant.

When the first administrator grants consent, Microsoft Entra ID creates a local Service Principal inside that customer's tenant.

The software company maintains only one Application Object while every customer manages its own Service Principal.

---

## Best Practices

* Use Single-Tenant for internal applications.
* Use Multi-Tenant only when external organizations require access.
* Review API permissions carefully.
* Require administrator consent for privileged permissions.
* Apply the principle of least privilege.
* Monitor external tenant usage.

---

## Common Pitfalls

* Confusing Application Objects with Service Principals.
* Assuming Multi-Tenant applications automatically receive permissions.
* Granting excessive API permissions.
* Selecting the wrong Supported Account Type during application registration.
* Forgetting that every external tenant creates its own Service Principal.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> * Supported Account Types
> * Single-Tenant applications
> * Multi-Tenant applications
> * Home Tenant
> * Service Principals
> * Consent across tenants

---

## Key Takeaways

* Supported Account Types determine who can authenticate.
* Single-Tenant applications are limited to one Microsoft Entra ID tenant.
* Multi-Tenant applications can be used across multiple organizations.
* The Application Object always remains in the home tenant.
* Each tenant receives its own Service Principal.
* Consent is managed independently by each tenant.

---

## References

| Microsoft Documentation                                                                  | Purpose                                     |
| ---------------------------------------------------------------------------------------- | ------------------------------------------- |
| https://learn.microsoft.com/entra/identity-platform/single-and-multi-tenant-apps         | Single-Tenant and Multi-Tenant applications |
| https://learn.microsoft.com/entra/identity-platform/howto-convert-app-to-be-multi-tenant | Configure a Multi-Tenant application        |
| https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals   | Application Objects and Service Principals  |
| https://learn.microsoft.com/entra/identity-platform/permissions-consent-overview         | Consent framework                           |
| https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/         | Microsoft Learn – Identity platform         |

