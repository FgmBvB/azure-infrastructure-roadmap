# Enterprise Applications

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Microsoft Entra Enterprise Applications, including Single Sign-On (SSO), Service Principals, provisioning, application access, permissions, consent, monitoring, and administrative best practices.

---

## Overview

Enterprise Applications represent the service identities of applications within a Microsoft Entra tenant.

They allow administrators to configure authentication, Single Sign-On (SSO), user assignments, provisioning, permissions, consent, and application access policies.

Enterprise Applications are created automatically when an application is registered in the tenant or when a user or administrator grants consent to a multi-tenant application.

---

## Learning Objectives

After completing this section you should be able to:

- Understand the purpose of Enterprise Applications.
- Explain the relationship between App Registrations and Service Principals.
- Configure Single Sign-On (SSO).
- Assign users and groups to applications.
- Configure automatic provisioning.
- Publish on-premises applications using Application Proxy.
- Manage API permissions and consent.
- Monitor application sign-ins and audit logs.
- Apply Microsoft security best practices.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Enterprise Applications fundamentals and architecture. |
| **02 - Service Principal** | Service Principals and their relationship with App Registrations. |
| **03 - Single Sign-On (SSO)** | SAML, OpenID Connect, OAuth, and SSO configuration. |
| **04 - User and Group Assignments** | Controlling application access through assignments. |
| **05 - Provisioning** | Automatic user provisioning and lifecycle management. |
| **06 - Application Proxy** | Secure remote access to on-premises web applications. |
| **07 - Permissions and Consent** | API permissions, delegated permissions, application permissions, and consent. |
| **08 - Monitoring and Logs** | Sign-in Logs, Audit Logs, and application monitoring. |
| **09 - Best Practices** | Security recommendations and operational guidance. |

---

## Architecture

```text
                    Microsoft Entra ID
                            │
                            ▼
                 Enterprise Application
                            │
        ┌───────────┬───────────┬───────────┐
        │           │           │
        ▼           ▼           ▼
      Users      Groups    Service Principal
        │                       │
        └───────────┬───────────┘
                    ▼
          Authentication & SSO
                    │
                    ▼
        Permissions • Provisioning
                    │
                    ▼
            Monitoring & Security
```

---

## Skills Covered

This section includes:

- Enterprise Applications
- Service Principals
- Single Sign-On (SSO)
- User Assignments
- Group Assignments
- Automatic Provisioning
- SCIM
- Application Proxy
- API Permissions
- Admin Consent
- User Consent
- Sign-in Logs
- Audit Logs
- Application Monitoring

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Manage Enterprise Applications.
- Configure Single Sign-On.
- Assign users and groups.
- Manage application permissions.
- Configure provisioning.
- Monitor application activity.
- Troubleshoot authentication issues.

---

## Key Takeaways

- Enterprise Applications represent applications inside a Microsoft Entra tenant.
- Every Enterprise Application is associated with a Service Principal.
- SSO simplifies user authentication across cloud and on-premises applications.
- Provisioning automates identity lifecycle management.
- Monitoring and auditing help secure application access and simplify troubleshooting.
