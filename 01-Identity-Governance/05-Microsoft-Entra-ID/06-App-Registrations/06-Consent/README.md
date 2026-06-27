# Consent

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra ID manages user and administrator consent for application permissions.

---

## Consent Flow

```text
        Application
              │
Requests API Permissions
              │
              ▼
 Microsoft Entra ID
              │
      Consent Required?
        │             │
       Yes            No
        │             │
        ▼             ▼
 User/Admin      Issue Access Token
 Grants Consent
        │
        ▼
 Issue Access Token
        │
        ▼
 Protected API
```

---

> [!TIP]
> **Key Concepts**
>
> * Consent allows an application to use granted API permissions.
> * Consent is required before an application can access protected resources.
> * Consent can be granted by users or administrators.
> * Some permissions always require administrator approval.
> * Consent follows the principle of least privilege.

---

## Overview

Consent is the process by which permission is granted for an application to access protected resources on behalf of a user or as the application itself.

Microsoft Entra ID evaluates whether consent is required before issuing an Access Token containing the requested permissions.

Without the appropriate consent, the requested permissions cannot be used.

---

## Why Consent Exists

Applications often need access to sensitive organizational data.

Rather than automatically granting permissions, Microsoft Entra ID requires explicit approval before an application can access protected APIs.

This prevents unauthorized applications from accessing corporate resources.

---

## Consent Types

Microsoft Entra ID supports two primary consent models.

| Consent Type  | Description                                                                |
| ------------- | -------------------------------------------------------------------------- |
| User Consent  | Granted by an individual user for permissions they are allowed to approve. |
| Admin Consent | Granted by an administrator on behalf of the entire tenant.                |

---

## User Consent

User Consent allows individual users to approve low-privilege delegated permissions for their own account.

Examples include:

* Reading the user's basic profile.
* Reading the user's email.
* Accessing the user's calendar.

Organizations can restrict or completely disable User Consent through tenant policies.

---

## Administrator Consent

Administrator Consent is required for permissions that affect organizational data or multiple users.

Typical Microsoft Entra ID roles that can grant administrator consent include:

* Global Administrator
* Cloud Application Administrator
* Application Administrator

Once granted, the consent applies across the tenant for the approved permissions.

---

## Consent Prompt

When consent is required, Microsoft Entra ID displays a consent prompt describing:

* The application requesting access.
* The requested permissions.
* Whether the application has been publisher verified.
* Whether administrator approval is required.

Users or administrators can approve or deny the request.

---

## Consent Policies

Organizations can configure consent policies to control who is allowed to grant consent.

Common options include:

* Allow User Consent.
* Restrict User Consent.
* Require Administrator Consent.
* Allow consent only for verified publishers.

These policies help reduce security risks and Shadow IT.

---

## Publisher Verification

Publisher Verification helps users identify applications published by verified organizations.

Applications from verified publishers display a verification badge during the consent process.

Although verification does not automatically grant trust, it helps users make informed consent decisions.

---

## Enterprise Scenario

An internal HR application requests permission to read employee profile information from Microsoft Graph.

The requested permission requires administrator approval.

A Global Administrator reviews the request, grants tenant-wide consent, and users can then sign in without individually approving the application.

---

## Best Practices

* Apply the principle of least privilege.
* Grant only the permissions required.
* Review tenant-wide consents regularly.
* Restrict User Consent where appropriate.
* Prefer verified publishers.
* Remove unused application permissions.

---

## Common Pitfalls

* Granting excessive permissions.
* Allowing unrestricted User Consent.
* Forgetting to review tenant-wide consents.
* Assuming consent grants Azure RBAC permissions.
* Confusing consent with authentication.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> * User Consent
> * Administrator Consent
> * Consent Policies
> * Publisher Verification
> * Tenant-wide Consent
> * Least Privilege

---

## Key Takeaways

* Consent authorizes the use of API permissions.
* User Consent applies only to the individual user.
* Administrator Consent applies across the tenant.
* Consent policies help control application access.
* Publisher Verification increases trust during the consent process.
* Consent does not replace Azure RBAC authorization.

---

## References

| Microsoft Documentation                                                                                                                          | Purpose                |
| ------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------- |
| [Permissions and consent in the Microsoft identity platform](https://learn.microsoft.com/entra/identity-platform/permissions-consent-overview)   | Consent overview       |
| [Configure how users consent to applications](https://learn.microsoft.com/entra/identity/enterprise-apps/configure-user-consent)                 | User Consent policies  |
| [Grant tenant-wide admin consent](https://learn.microsoft.com/entra/identity/enterprise-apps/grant-admin-consent)                                | Administrator Consent  |
| [Publisher verification](https://learn.microsoft.com/entra/identity-platform/publisher-verification-overview)                                    | Verified publishers    |
| [Microsoft Learn – Build applications that authenticate users](https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/) | Microsoft Learn module |

