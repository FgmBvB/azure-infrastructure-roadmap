# Service Principal

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains the purpose of Service Principals and how they provide the security identity used by applications inside Microsoft Entra ID tenants.

---

## Identity Model

```text
          App Registration
                  │
                  ▼
         Application Object
                  │
         (Home Tenant Only)
                  │
      ┌───────────┼───────────┐
      │           │           │
      ▼           ▼           ▼
 Tenant A     Tenant B     Tenant C
      │           │           │
      ▼           ▼           ▼
Service      Service      Service
Principal    Principal    Principal
      │           │           │
      └───────────┼───────────┘
                  ▼
       Enterprise Applications
```

---

> [!TIP]
> **Key Concepts**
>
> - Every Enterprise Application is a Service Principal.
> - Service Principals represent application identities inside a tenant.
> - One Application Object can create multiple Service Principals.
> - Permissions and policies are assigned to the Service Principal.
> - Service Principals enable secure authentication without user credentials.

---

## Overview

A Service Principal is the security identity of an application within a Microsoft Entra ID tenant.

While the **Application Object** defines the application's global configuration, the **Service Principal** represents the application's local identity inside a specific tenant.

Every Enterprise Application is backed by a Service Principal.

---

## Relationship with the Application Object

An Application Object exists only in its home tenant.

Whenever the application is used inside a tenant, Microsoft Entra ID creates a corresponding Service Principal.

Each Service Principal maintains its own local configuration while referencing the same Application Object.

| Application Object | Service Principal |
|--------------------|-------------------|
| Global definition | Local identity |
| Exists once | One per tenant |
| Created by App Registration | Created automatically when needed |
| Stores application configuration | Stores tenant-specific configuration |

---

## Service Principal Responsibilities

The Service Principal enables Microsoft Entra ID to:

- Authenticate applications.
- Assign API permissions.
- Apply Azure RBAC roles.
- Apply Conditional Access policies.
- Configure Single Sign-On (SSO).
- Assign users and groups.
- Enable automatic provisioning.

---

## Service Principal Types

Microsoft Entra ID supports different types of Service Principals.

| Type | Description |
|------|-------------|
| Application | Created from an App Registration. |
| Managed Identity | Automatically created for Azure resources. |
| Legacy | Created through older application management models or legacy integration scenarios. |

Although their origin differs, all Service Principals represent identities managed by Microsoft Entra ID.

---

## Multi-Tenant Applications

A Multi-Tenant application has a single Application Object but can create multiple Service Principals.

```text
          Application Object
             (Home Tenant)
                   │
      ┌────────────┼────────────┐
      ▼            ▼            ▼
 Tenant A     Tenant B     Tenant C
      │            │            │
      ▼            ▼            ▼
Service      Service      Service
Principal    Principal    Principal
```

Each tenant manages its own Service Principal independently.

Permissions, Conditional Access policies, user assignments, and Azure RBAC roles are never shared between tenants.

---

## Azure RBAC

Service Principals can receive Azure Role-Based Access Control (Azure RBAC) assignments.

For example:

- Reader
- Contributor
- Virtual Machine Contributor
- Key Vault Secrets User

Azure resources evaluate these role assignments independently from Microsoft Entra ID API permissions.

---

## API Permissions

Service Principals can also receive API permissions.

These permissions allow applications to access services such as:

- Microsoft Graph
- Azure Resource Manager
- Azure Key Vault
- Microsoft 365 APIs
- Custom APIs

Depending on the scenario, permissions may be:

- Delegated Permissions
- Application Permissions

Administrator consent may be required before these permissions become effective.

---

## Lifecycle

The lifecycle of a Service Principal depends on its origin.

```text
App Registration
        │
        ▼
Application Object
        │
        ▼
Service Principal
        │
        ▼
Enterprise Application
        │
        ▼
Authentication
Authorization
Provisioning
```

If an Application Object is permanently deleted, its associated Service Principals are eventually removed as well.

---

## Enterprise Scenario

A company develops an internal inventory application.

The application is registered once in the home tenant.

When another subsidiary begins using the application, Microsoft Entra ID creates a new Service Principal in that tenant.

Each subsidiary independently assigns users, configures Conditional Access, grants API permissions, and applies Azure RBAC without affecting the original Application Object.

---

## Best Practices

- Assign least-privilege permissions.
- Review Azure RBAC assignments regularly.
- Audit Enterprise Applications periodically.
- Remove unused Service Principals.
- Monitor sign-in activity.
- Use Managed Identities whenever possible for Azure resources.

---

## Common Pitfalls

- Confusing the Application Object with the Service Principal.
- Assuming permissions are shared across tenants.
- Granting excessive Azure RBAC roles.
- Forgetting administrator consent.
- Leaving unused Enterprise Applications in the tenant.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Service Principals
> - Enterprise Applications
> - Application Objects
> - Azure RBAC assignments
> - API permissions
> - Multi-Tenant applications
> - Managed Identities

---

## Key Takeaways

- A Service Principal is the local identity of an application.
- Every Enterprise Application is backed by a Service Principal.
- One Application Object can create many Service Principals.
- Service Principals receive permissions and policies.
- Azure RBAC and API permissions are managed independently.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Application Objects and Service Principals](https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals) | Identity model |
| [Enterprise applications in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/enterprise-apps/what-is-application-management) | Enterprise Applications |
| [Assign Azure roles to Service Principals](https://learn.microsoft.com/azure/role-based-access-control/role-assignments-portal) | Azure RBAC |
| [Managed identities for Azure resources](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview) | Managed Identities |
| [Microsoft Learn – Describe the capabilities of Microsoft Entra ID](https://learn.microsoft.com/training/modules/explore-basic-services-identity-types/) | Microsoft Learn module |
