# Authentication

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra ID verifies identities before granting access to cloud resources and applications.

---

## Authentication Flow

```text
          User
            │
     Enter Credentials
            │
            ▼
   Microsoft Entra ID
            │
   Verify Identity
            │
            ▼
 Authentication Success
            │
            ▼
 Access Token Issued
            │
            ▼
 Azure Resource / Application
```

---

> [!TIP]
> **Key Concepts**
>
> - Authentication verifies the identity of a user or workload.
> - Authentication occurs before authorization.
> - Microsoft Entra ID acts as the Identity Provider (IdP).
> - Successful authentication results in the issuance of security tokens.
> - Azure RBAC evaluates permissions after authentication.

---

## Overview

Authentication is the process of verifying the identity of a user, device, application, or workload before access is granted to cloud resources.

Microsoft Entra ID acts as the Identity Provider (IdP) for Microsoft cloud services. It validates credentials, evaluates authentication requirements, and issues security tokens that applications use to establish trust.

Authentication only answers one question:

> **Who are you?**

Authorization is a separate process that determines what an authenticated identity is allowed to access.

---

## Authentication Flow

A typical authentication process consists of the following steps:

1. The user attempts to access an application or Azure resource.
2. The application redirects the authentication request to Microsoft Entra ID.
3. Microsoft Entra ID validates the user's identity.
4. Additional security requirements, such as Multi-Factor Authentication or Conditional Access policies, are evaluated if applicable.
5. After successful authentication, Microsoft Entra ID issues a security token.
6. The application validates the token and grants access.

Authentication does not grant permissions by itself. Authorization mechanisms such as Azure RBAC determine which actions the authenticated identity can perform.

---

## Authentication Factors

Authentication can rely on one or more independent factors:

- Something you know (password or PIN)
- Something you have (phone, FIDO2 security key, smart card)
- Something you are (fingerprint, facial recognition)

Combining multiple factors significantly increases security and reduces the risk of credential compromise.

---

## Authentication Methods

Microsoft Entra ID supports multiple authentication methods, including:

- Password
- Microsoft Authenticator
- FIDO2 Security Keys
- Windows Hello for Business
- Passkeys
- Temporary Access Pass (TAP)
- Certificate-Based Authentication
- SMS (legacy scenarios)
- Voice Call (legacy scenarios)

The availability of authentication methods depends on organizational policies and licensing.

---

## Passwordless Authentication

Passwordless authentication eliminates the need for traditional passwords.

Instead, users authenticate using trusted devices or cryptographic credentials such as Windows Hello for Business, FIDO2 security keys, Microsoft Authenticator, or Passkeys.

Microsoft recommends passwordless authentication whenever possible because passwords remain one of the primary attack vectors in modern environments.

---

## Single Sign-On (SSO)

Single Sign-On allows users to authenticate once and access multiple trusted applications without signing in repeatedly.

Microsoft Entra ID provides SSO for Azure, Microsoft 365, and thousands of third-party SaaS applications.

SSO improves both user experience and security by reducing password usage.

---

## Authentication Protocols

Microsoft Entra ID supports several industry-standard authentication protocols.

| Protocol | Typical Use |
|----------|-------------|
| OAuth 2.0 | Authorization delegation |
| OpenID Connect (OIDC) | User authentication |
| SAML 2.0 | Enterprise Single Sign-On |
| WS-Federation | Legacy Microsoft applications |

These protocols enable secure authentication across cloud and hybrid environments.

---

## Enterprise Scenario

An employee opens Microsoft Teams from a corporate laptop.

The application redirects the authentication request to Microsoft Entra ID.

After verifying the employee's identity and evaluating security requirements, Microsoft Entra ID issues a security token.

Teams validates the token and grants access without requesting additional credentials.

The same identity can then be reused to access other Microsoft services through Single Sign-On.

---

## Best Practices

- Enable Multi-Factor Authentication.
- Prefer passwordless authentication whenever possible.
- Use Single Sign-On to reduce password usage.
- Disable legacy authentication protocols when possible.
- Monitor authentication logs regularly.
- Apply Conditional Access policies to protect identities.

---

## Common Pitfalls

- Confusing authentication with authorization.
- Assuming successful authentication automatically grants permissions.
- Relying exclusively on passwords.
- Leaving legacy authentication enabled.
- Ignoring sign-in risk monitoring.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Authentication concepts
> - Authentication flow
> - Authentication factors
> - Authentication methods
> - Passwordless authentication
> - Single Sign-On (SSO)
> - Security tokens
> - Authentication protocols
> - Authentication versus authorization

---

## Key Takeaways

- Authentication verifies identity.
- Microsoft Entra ID is the Identity Provider (IdP).
- Authentication always occurs before authorization.
- Successful authentication results in security tokens.
- Azure RBAC authorizes authenticated identities.
- Passwordless authentication is Microsoft's recommended approach.
- Single Sign-On improves both security and user experience.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| https://learn.microsoft.com/entra/identity/authentication/overview-authentication | Authentication overview |
| https://learn.microsoft.com/entra/identity/authentication/concept-authentication-methods | Authentication methods |
| https://learn.microsoft.com/entra/identity/authentication/concept-authentication-passwordless | Passwordless authentication |
| https://learn.microsoft.com/entra/identity-platform/v2-protocols | OAuth 2.0, OpenID Connect and protocols |
| https://learn.microsoft.com/training/modules/explore-basic-services-identity-types/ | Microsoft Learn – Authentication concepts |
