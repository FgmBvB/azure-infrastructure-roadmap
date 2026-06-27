# Single Sign-On (SSO)

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra ID enables Single Sign-On (SSO) to provide secure authentication across cloud and on-premises applications.

---

## Single Sign-On Flow

```text
              User
                │
                ▼
     Microsoft Entra ID
(Authentication)
                │
                ▼
      Security Token
                │
                ▼
 Enterprise Application
                │
                ▼
 User Access Granted
```

---

> [!TIP]
> **Key Concepts**
>
> - Single Sign-On (SSO) allows users to authenticate once and access multiple applications.
> - Microsoft Entra ID acts as the Identity Provider (IdP).
> - Applications trust Microsoft Entra ID to authenticate users.
> - SSO improves security and user experience.
> - Different SSO protocols are available depending on the application.

---

## Overview

Single Sign-On (SSO) allows users to authenticate once with Microsoft Entra ID and access multiple applications without signing in again.

Instead of every application managing usernames and passwords independently, applications trust Microsoft Entra ID to perform authentication.

After successful authentication, Microsoft Entra ID issues the appropriate security token required by the application.

---

## Why Single Sign-On Exists

Without Single Sign-On:

- Users maintain multiple passwords.
- Password reuse becomes common.
- Help desk password reset requests increase.
- User experience is degraded.

Single Sign-On centralizes authentication while allowing each application to maintain its own authorization model.

---

## Supported SSO Methods

Microsoft Entra ID supports several authentication methods.

| Method | Typical Scenario |
|---------|------------------|
| OpenID Connect (OIDC) | Modern cloud applications |
| OAuth 2.0 | API authorization |
| SAML 2.0 | Enterprise SaaS applications |
| Password-based SSO | Legacy web applications |
| Linked Sign-On | External applications |
| Header-based SSO | Legacy web applications using Application Proxy |
| Integrated Windows Authentication (IWA) | On-premises Active Directory applications |

Each method is designed for different application architectures.

---

## Authentication Flow

A typical authentication process follows these steps:

1. User opens an application.
2. The application redirects the user to Microsoft Entra ID.
3. Microsoft Entra ID authenticates the user.
4. A security token is issued.
5. The application validates the token.
6. Access is granted.

Authentication occurs only once while the session remains valid.

---

## Identity Provider

In a Single Sign-On environment:

- Microsoft Entra ID acts as the **Identity Provider (IdP)**.
- The application acts as the **Service Provider (SP)** or **Relying Party (RP)** depending on the protocol.
- Microsoft Entra ID is responsible for verifying the user's identity.

Applications trust Microsoft Entra ID instead of storing user passwords.

---

## User Assignments

Enterprise Applications can restrict access through user or group assignments.

If **Assignment required?** is enabled:

- Only assigned users or groups can sign in.

If disabled:

- Any user in the tenant may authenticate, subject to other access policies.

---

## Conditional Access

Single Sign-On integrates with Microsoft Entra Conditional Access.

Administrators can require:

- Multi-Factor Authentication (MFA)
- Compliant devices
- Approved locations
- Sign-in risk evaluation
- Device state requirements

Authentication succeeds only if all configured policies are satisfied.

---

## Enterprise Scenario

A company uses Microsoft 365, Salesforce, ServiceNow, and Workday.

Employees authenticate once using Microsoft Entra ID.

After signing in, users can access each application without entering additional passwords.

Conditional Access policies enforce Multi-Factor Authentication and device compliance before access is granted.

---

## Best Practices

- Enable Single Sign-On whenever supported.
- Use modern protocols such as OpenID Connect or SAML.
- Assign applications through groups.
- Protect access with Conditional Access.
- Monitor sign-in activity regularly.
- Remove unused Enterprise Applications.

---

## Common Pitfalls

- Confusing authentication with authorization.
- Forgetting to assign users when required.
- Leaving legacy password authentication enabled unnecessarily.
- Ignoring Conditional Access policies.
- Misconfiguring SAML or Redirect URIs.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Single Sign-On (SSO)
> - Identity Provider (IdP)
> - Service Provider (SP)
> - OpenID Connect
> - SAML
> - OAuth 2.0
> - User assignments
> - Conditional Access integration

---

## Key Takeaways

- Single Sign-On centralizes authentication.
- Microsoft Entra ID acts as the Identity Provider.
- Applications trust Microsoft Entra ID to authenticate users.
- Multiple SSO protocols are supported.
- Conditional Access strengthens authentication security.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Single sign-on in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/enterprise-apps/what-is-single-sign-on) | Single Sign-On overview |
| [Plan a Microsoft Entra single sign-on deployment](https://learn.microsoft.com/entra/identity/enterprise-apps/plan-sso-deployment) | SSO planning |
| [SAML-based Single Sign-On](https://learn.microsoft.com/entra/identity/enterprise-apps/configure-saml-single-sign-on) | SAML configuration |
| [OpenID Connect and OAuth 2.0](https://learn.microsoft.com/entra/identity-platform/v2-protocols) | Modern authentication protocols |
| [Microsoft Learn – Describe the capabilities of Microsoft Entra ID](https://learn.microsoft.com/training/modules/explore-basic-services-identity-types/) | Microsoft Learn module |
