# Multi-Factor Authentication (MFA) Overview

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It introduces Multi-Factor Authentication (MFA), explains its purpose, authentication factors, and its role in protecting Microsoft Entra ID identities.

---

## Authentication Process

```text
User Sign-in
      │
      ▼
Username + Password
      │
      ▼
Primary Authentication
      │
      ▼
MFA Challenge
      │
      ▼
Second Authentication Factor
      │
      ▼
Access Granted
```

---

> [!TIP]
> **Key Concepts**
>
> - Multi-Factor Authentication (MFA) requires more than one authentication factor.
> - MFA significantly reduces the risk of compromised credentials.
> - Microsoft Entra ID supports multiple verification methods.
> - MFA can be required through Security Defaults or Conditional Access.
> - Passwordless authentication is built on MFA technologies.

---

## Overview

Multi-Factor Authentication (MFA) is an authentication mechanism that requires users to verify their identity using two or more independent authentication factors.

Even if a password is compromised, attackers cannot successfully authenticate without the additional verification factor.

Microsoft Entra ID integrates MFA with cloud applications, Microsoft 365, Azure, and thousands of third-party applications.

---

## Authentication Factors

Authentication factors are grouped into three categories.

| Factor | Example |
|---------|---------|
| **Something you know** | Password, PIN |
| **Something you have** | Mobile phone, Microsoft Authenticator, Security Key |
| **Something you are** | Fingerprint, Face recognition |

A secure authentication combines factors from different categories.

---

## Why MFA Matters

Passwords alone are vulnerable to:

- Password spraying
- Credential stuffing
- Phishing attacks
- Password reuse
- Brute-force attacks

Adding a second authentication factor significantly reduces the likelihood of unauthorized access.

---

## Supported Authentication Methods

Microsoft Entra ID supports several MFA methods, including:

- Microsoft Authenticator
- SMS verification
- Voice calls
- FIDO2 Security Keys
- Windows Hello for Business
- OATH hardware and software tokens
- Temporary Access Pass (TAP)

The available methods depend on the organization's authentication policies.

---

## Security Defaults vs Conditional Access

Microsoft Entra ID can require MFA using different mechanisms.

| Feature | Description |
|---------|-------------|
| **Security Defaults** | Microsoft's recommended baseline security configuration for smaller environments. |
| **Conditional Access** | Provides granular control over when and how MFA is required based on users, devices, applications, locations, and risk conditions. |

Conditional Access offers significantly greater flexibility for enterprise environments.

---

## Authentication Flow

```text
User
 │
 ▼
Primary Authentication
 │
 ▼
Microsoft Entra ID
 │
 ▼
MFA Challenge
 │
 ▼
Authentication Method
 │
 ▼
Access Granted
```

---

## Passwordless Authentication

Microsoft Entra ID also supports passwordless authentication.

Instead of verifying a password followed by MFA, users authenticate directly using methods such as:

- Microsoft Authenticator
- Windows Hello for Business
- FIDO2 Security Keys

Passwordless authentication improves both security and user experience.

---

## Enterprise Scenario

A company protects Microsoft 365 with Conditional Access.

Employees authenticate using their username and password, followed by a Microsoft Authenticator approval on their mobile device.

Only after successful completion of both authentication factors is access granted to corporate resources.

---

## Best Practices

- Require MFA for all privileged accounts.
- Prefer Microsoft Authenticator over SMS when possible.
- Protect remote access with MFA.
- Use Conditional Access for flexible MFA policies.
- Review authentication methods regularly.
- Encourage passwordless authentication where supported.

---

## Common Pitfalls

- Relying only on passwords.
- Using SMS as the only authentication method.
- Excluding privileged accounts from MFA.
- Forgetting to register backup authentication methods.
- Assuming MFA replaces strong password policies.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Authentication factors
> - Supported MFA methods
> - Security Defaults
> - Conditional Access integration
> - Passwordless authentication
> - Microsoft Authenticator

---

## Key Takeaways

- MFA requires multiple authentication factors.
- It significantly reduces the risk of compromised credentials.
- Microsoft Entra ID supports several authentication methods.
- Conditional Access provides flexible MFA enforcement.
- Passwordless authentication builds upon MFA technologies.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Microsoft Entra Multifactor Authentication](https://learn.microsoft.com/entra/identity/authentication/concept-mfa-howitworks) | MFA overview |
| [Authentication methods in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/authentication/concept-authentication-methods) | Supported authentication methods |
| [Security defaults](https://learn.microsoft.com/entra/fundamentals/security-defaults) | Security Defaults overview |
| [Conditional Access overview](https://learn.microsoft.com/entra/identity/conditional-access/overview) | Conditional Access and MFA |
| [Microsoft Learn – Describe Microsoft Entra multifactor authentication](https://learn.microsoft.com/training/modules/describe-authentication-capabilities-azure-ad/) | Microsoft Learn module |
