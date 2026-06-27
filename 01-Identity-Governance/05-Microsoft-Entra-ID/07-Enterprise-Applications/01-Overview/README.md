# Enterprise Applications Overview

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It introduces Microsoft Entra ID Enterprise Applications and explains how they represent the local identity of applications inside a tenant.

---

## Enterprise Application Model

```text
              Application
                    │
                    ▼
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
        Authentication & SSO
                    │
                    ▼
     Users, Groups & Policies
```

---

> [!TIP]
> **Key Concepts**
>
> - Enterprise Applications are Service Principals.
> - Every Enterprise Application represents an application inside a tenant.
> - Enterprise Applications enable Single Sign-On (SSO).
> - Permissions, assignments, and Conditional Access are managed through Enterprise Applications.
> - Multi-Tenant applications create one Enterprise Application per tenant.

---

## Overview

An Enterprise Application is the local representation of an application inside a Microsoft Entra ID tenant.

Technically, every Enterprise Application is a **Service Principal**.

While an **Application Object** defines how an application is built, the Enterprise Application represents how that application operates inside a specific tenant.

Enterprise Applications allow administrators to control authentication, authorization, user assignments, provisioning, and Single Sign-On without modifying the original application.

---

## Why Enterprise Applications Exist

Applications often need tenant-specific configuration.

Each organization may require different:

- Users
- Groups
- Permissions
- Conditional Access policies
- Single Sign-On configuration
- Provisioning settings

Enterprise Applications provide this local administrative layer while keeping the original Application Object unchanged.

---

## Relationship with App Registrations

Although App Registrations and Enterprise Applications are closely related, they serve different purposes.

| App Registration | Enterprise Application |
|------------------|------------------------|
| Global application definition | Local application instance |
| Creates the Application Object | Represents the Service Principal |
| Exists in the home tenant | Exists in every tenant where the application is used |
| Managed mainly by developers | Managed mainly by administrators |

Both objects are required for applications to authenticate and operate within Microsoft Entra ID.

---

## Assignment Required

Enterprise Applications can require explicit user or group assignments before users are allowed to sign in.

| Setting | Behavior |
|---------|----------|
| **Yes** | Only assigned users or groups can access the application. |
| **No** | Any user in the tenant can sign in, provided other access requirements are met. |

Requiring assignments helps implement the principle of least privilege and is recommended for most enterprise applications.

---

## Visibility

Enterprise Applications can be configured to appear in the Microsoft Entra **My Apps** portal.

| Setting | Behavior |
|---------|----------|
| **Yes** | Assigned users see the application in the My Apps portal. |
| **No** | The application is hidden from My Apps but remains accessible through direct links or automated processes. |

Applications such as APIs, background services, or infrastructure components are commonly hidden from end users.

---

## Service Principal

Every Enterprise Application is backed by a **Service Principal**.

The Service Principal is the security identity used by Microsoft Entra ID to:

- Authenticate applications
- Assign permissions
- Apply Conditional Access policies
- Configure Single Sign-On (SSO)
- Assign users and groups
- Enable application provisioning

The Service Principal exists independently within each Microsoft Entra ID tenant.

---

## Service Principal Types

Microsoft Entra ID creates different types of Service Principals depending on how an application or workload is introduced into a tenant.

| Type | Description |
|------|-------------|
| **Application** | Created from an App Registration and represents an application within a tenant. |
| **Managed Identity** | Automatically created for Azure resources, such as Virtual Machines or App Services, to provide passwordless authentication. |
| **Legacy** | Created through older application management models or legacy integration scenarios. |

Although they have different origins, all Service Principals represent security identities managed by Microsoft Entra ID.

---

## Common Scenarios

Enterprise Applications are commonly used for:

| Scenario | Example |
|----------|---------|
| Single Sign-On | Microsoft 365, Salesforce |
| SaaS Integration | ServiceNow, Workday |
| Internal Applications | Corporate HR systems |
| User Provisioning | Automatic account lifecycle |
| Conditional Access | MFA and device compliance |
| Application Proxy | Publishing on-premises applications |

---

## Enterprise Application Lifecycle

```text
Application Registered
          │
          ▼
Service Principal Created
          │
          ▼
Enterprise Application
          │
          ▼
Configure SSO
          │
          ▼
Assign Users & Groups
          │
          ▼
Grant Permissions
          │
          ▼
Apply Policies
          │
          ▼
Monitor & Maintain
```

---

## Enterprise Scenario

A company purchases Salesforce.

When the application is added to Microsoft Entra ID, an Enterprise Application is created in the tenant.

Administrators configure Single Sign-On, assign employees to the application, enable automatic user provisioning, and enforce Multi-Factor Authentication through Conditional Access.

Salesforce itself remains unchanged, while the Enterprise Application stores the organization's local configuration.

---

## Best Practices

- Assign users through groups whenever possible.
- Apply Conditional Access policies.
- Enable Single Sign-On.
- Review application permissions regularly.
- Remove unused Enterprise Applications.
- Audit application sign-ins periodically.

---

## Common Pitfalls

- Confusing Enterprise Applications with App Registrations.
- Assigning users individually instead of using groups.
- Granting excessive permissions.
- Forgetting to review unused applications.
- Ignoring sign-in and audit logs.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Enterprise Applications
> - Service Principals
> - Single Sign-On (SSO)
> - User and Group Assignments
> - Provisioning
> - Conditional Access integration
> - Relationship with App Registrations

---

## Key Takeaways

- Enterprise Applications are Service Principals.
- Every tenant has its own Enterprise Application.
- Enterprise Applications store tenant-specific configuration.
- Administrators manage access through Enterprise Applications.
- Enterprise Applications enable SSO, provisioning, and Conditional Access.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Enterprise applications in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/enterprise-apps/what-is-application-management) | Enterprise Applications overview |
| [Application Objects and Service Principals](https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals) | Identity model |
| [Single sign-on in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/enterprise-apps/what-is-single-sign-on) | Single Sign-On overview |
| [Application provisioning](https://learn.microsoft.com/entra/identity/app-provisioning/user-provisioning) | User provisioning |
| [Microsoft Learn – Describe the capabilities of Microsoft Entra ID](https://learn.microsoft.com/training/modules/explore-basic-services-identity-types/) | Microsoft Learn module |# Enterprise Applications Overview

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It introduces Microsoft Entra ID Enterprise Applications and explains how they represent the local identity of applications inside a tenant.

---

## Enterprise Application Model

```text
              Application
                    │
                    ▼
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
        Authentication & SSO
                    │
                    ▼
     Users, Groups & Policies
```

---

> [!TIP]
> **Key Concepts**
>
> - Enterprise Applications are Service Principals.
> - Every Enterprise Application represents an application inside a tenant.
> - Enterprise Applications enable Single Sign-On (SSO).
> - Permissions, assignments, and Conditional Access are managed through Enterprise Applications.
> - Multi-Tenant applications create one Enterprise Application per tenant.

---

## Overview

An Enterprise Application is the local representation of an application inside a Microsoft Entra ID tenant.

Technically, every Enterprise Application is a **Service Principal**.

While an **Application Object** defines how an application is built, the Enterprise Application represents how that application operates inside a specific tenant.

Enterprise Applications allow administrators to control authentication, authorization, user assignments, provisioning, and Single Sign-On without modifying the original application.

---

## Why Enterprise Applications Exist

Applications often need tenant-specific configuration.

Each organization may require different:

- Users
- Groups
- Permissions
- Conditional Access policies
- Single Sign-On configuration
- Provisioning settings

Enterprise Applications provide this local administrative layer while keeping the original Application Object unchanged.

---

## Relationship with App Registrations

Although App Registrations and Enterprise Applications are closely related, they serve different purposes.

| App Registration | Enterprise Application |
|------------------|------------------------|
| Global application definition | Local application instance |
| Creates the Application Object | Represents the Service Principal |
| Exists in the home tenant | Exists in every tenant where the application is used |
| Managed mainly by developers | Managed mainly by administrators |

Both objects are required for applications to authenticate and operate within Microsoft Entra ID.

---

## Service Principal

Every Enterprise Application is backed by a **Service Principal**.

The Service Principal is the security identity used by Microsoft Entra ID to:

- Authenticate applications
- Assign permissions
- Apply Conditional Access
- Configure Single Sign-On
- Assign users and groups
- Enable provisioning

The Service Principal exists independently inside each tenant.

---

## Common Scenarios

Enterprise Applications are commonly used for:

| Scenario | Example |
|----------|---------|
| Single Sign-On | Microsoft 365, Salesforce |
| SaaS Integration | ServiceNow, Workday |
| Internal Applications | Corporate HR systems |
| User Provisioning | Automatic account lifecycle |
| Conditional Access | MFA and device compliance |
| Application Proxy | Publishing on-premises applications |

---

## Enterprise Application Lifecycle

```text
Application Registered
          │
          ▼
Service Principal Created
          │
          ▼
Enterprise Application
          │
          ▼
Configure SSO
          │
          ▼
Assign Users & Groups
          │
          ▼
Grant Permissions
          │
          ▼
Apply Policies
          │
          ▼
Monitor & Maintain
```

---

## Enterprise Scenario

A company purchases Salesforce.

When the application is added to Microsoft Entra ID, an Enterprise Application is created in the tenant.

Administrators configure Single Sign-On, assign employees to the application, enable automatic user provisioning, and enforce Multi-Factor Authentication through Conditional Access.

Salesforce itself remains unchanged, while the Enterprise Application stores the organization's local configuration.

---

## Best Practices

- Assign users through groups whenever possible.
- Apply Conditional Access policies.
- Enable Single Sign-On.
- Review application permissions regularly.
- Remove unused Enterprise Applications.
- Audit application sign-ins periodically.

---

## Common Pitfalls

- Confusing Enterprise Applications with App Registrations.
- Assigning users individually instead of using groups.
- Granting excessive permissions.
- Forgetting to review unused applications.
- Ignoring sign-in and audit logs.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Enterprise Applications
> - Service Principals
> - Single Sign-On (SSO)
> - User and Group Assignments
> - Provisioning
> - Conditional Access integration
> - Relationship with App Registrations

---

## Key Takeaways

- Enterprise Applications are Service Principals.
- Every tenant has its own Enterprise Application.
- Enterprise Applications store tenant-specific configuration.
- Administrators manage access through Enterprise Applications.
- Enterprise Applications enable SSO, provisioning, and Conditional Access.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Enterprise applications in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/enterprise-apps/what-is-application-management) | Enterprise Applications overview |
| [Application Objects and Service Principals](https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals) | Identity model |
| [Single sign-on in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/enterprise-apps/what-is-single-sign-on) | Single Sign-On overview |
| [Application provisioning](https://learn.microsoft.com/entra/identity/app-provisioning/user-provisioning) | User provisioning |
| [Microsoft Learn – Describe the capabilities of Microsoft Entra ID](https://learn.microsoft.com/training/modules/explore-basic-services-identity-types/) | Microsoft Learn module |
