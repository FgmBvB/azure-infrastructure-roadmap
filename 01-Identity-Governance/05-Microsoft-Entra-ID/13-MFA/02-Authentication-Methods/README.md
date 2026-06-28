# Microsoft Entra Authentication Methods

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains the authentication methods supported by Microsoft Entra ID for Multi-Factor Authentication (MFA) and passwordless authentication.

---

## Authentication Methods Overview

```text
                User
                  │
                  ▼
      Microsoft Entra ID
                  │
 ┌────────────────┼─────────────────┐
 │                │                 │
 ▼                ▼                 ▼
Possession     Biometrics       Knowledge
Factor          Factor            Factor
 │                │                 │
 ▼                ▼                 ▼
Authenticator  Windows Hello     OATH
FIDO2          Biometrics        SMS
TAP                             Voice Call
```

---

> [!TIP]
> **Key Concepts**
>
> - Microsoft Entra ID supports multiple authentication methods.
> - Organizations decide which methods users can register.
> - Some methods support MFA only, while others support passwordless authentication.
> - Microsoft recommends phishing-resistant authentication methods whenever possible.
> - Users should register multiple authentication methods for account recovery.

---

## Overview

Microsoft Entra ID provides several authentication methods that can be used for Multi-Factor Authentication (MFA), Self-Service Password Reset (SSPR), and passwordless authentication.

Administrators enable or restrict these methods through Authentication Methods policies.

---

## Microsoft Authenticator

Microsoft Authenticator is Microsoft's recommended authentication method.

It supports:

- Push notifications
- Number matching
- One-time passcodes (OTP)
- Passwordless sign-in

Advantages include:

- Strong security
- Excellent user experience
- Protection against MFA fatigue through number matching

---

## FIDO2 Security Keys

FIDO2 Security Keys are hardware-based authentication devices.

Characteristics include:

- Phishing-resistant authentication
- Passwordless sign-in
- Public key cryptography
- USB, NFC, or Bluetooth support

Microsoft recommends FIDO2 keys for high-security environments.

---

## Windows Hello for Business

Windows Hello for Business enables passwordless authentication using:

- Fingerprint recognition
- Facial recognition
- Device PIN protected by the Trusted Platform Module (TPM)

Authentication credentials remain protected by the device.

---

## Temporary Access Pass (TAP)

Temporary Access Pass (TAP) is a time-limited authentication method.

Typical uses include:

- Onboarding new users
- Recovering authentication methods
- Registering passwordless authentication
- Replacing lost authentication devices

TAP helps administrators bootstrap strong authentication without requiring an existing MFA method.

---

## SMS Authentication

SMS authentication sends a verification code to the user's registered mobile phone.

Advantages:

- Easy to deploy
- Broad device compatibility

Limitations:

- Vulnerable to SIM swap attacks
- Less resistant to phishing
- Not recommended as the primary authentication method

---

## Voice Call

Voice Call authentication verifies users through an automated telephone call.

Although supported, Microsoft recommends stronger authentication methods whenever possible.

---

## OATH Tokens

Microsoft Entra ID supports OATH-based authentication.

Supported token types include:

- Hardware OATH tokens
- Software OATH applications

These generate time-based one-time passwords (TOTP).

---

## Authentication Method Comparison

| Method | MFA | Passwordless | Phishing Resistant |
|---------|-----|--------------|--------------------|
| Microsoft Authenticator | Yes | Yes | High (number matching) |
| FIDO2 Security Keys | Yes | Yes | Yes |
| Windows Hello for Business | Yes | Yes | Yes |
| Temporary Access Pass | Yes | Temporary bootstrap | No |
| SMS | Yes | No | No |
| Voice Call | Yes | No | No |
| OATH Tokens | Yes | No | Moderate |

---

## Authentication Method Policies

Administrators manage authentication methods through Microsoft Entra ID policies.

Policies determine:

- Which methods are enabled.
- Which users or groups may use them.
- Registration requirements.
- Passwordless authentication availability.

Authentication Methods policies centralize authentication management across the organization.

---

## Registration Process

```text
User
 │
 ▼
Authentication Methods Policy
 │
 ▼
Method Registration
 │
 ▼
Verification
 │
 ▼
Authentication Ready
```

Users typically register their authentication methods through the Microsoft Entra authentication registration portal.

---

## Enterprise Scenario

A company enables Microsoft Authenticator, FIDO2 Security Keys, and Temporary Access Pass.

New employees receive a Temporary Access Pass during onboarding, use it to register Microsoft Authenticator and a FIDO2 Security Key, and then authenticate without relying on passwords.

SMS authentication remains available only as a recovery option for selected users.

---

## Best Practices

- Prefer phishing-resistant authentication methods.
- Use Microsoft Authenticator whenever possible.
- Deploy FIDO2 Security Keys for privileged users.
- Enable Temporary Access Pass for secure onboarding.
- Limit SMS and Voice Call usage.
- Require users to register multiple authentication methods.

---

## Common Pitfalls

- Relying only on SMS authentication.
- Allowing users to register only one authentication method.
- Forgetting backup authentication methods.
- Using weak authentication methods for privileged accounts.
- Not reviewing Authentication Methods policies regularly.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Microsoft Authenticator
> - FIDO2 Security Keys
> - Windows Hello for Business
> - Temporary Access Pass (TAP)
> - SMS and Voice Call authentication
> - Authentication Methods policies

---

## Key Takeaways

- Microsoft Entra ID supports multiple authentication methods.
- Passwordless authentication improves both security and usability.
- Microsoft recommends phishing-resistant authentication methods.
- Authentication Methods policies determine which methods users may register.
- Registering multiple authentication methods improves resilience and account recovery.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Authentication methods in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/authentication/concept-authentication-methods) | Authentication methods overview |
| [Microsoft Authenticator](https://learn.microsoft.com/entra/identity/authentication/concept-authentication-authenticator-app) | Microsoft Authenticator |
| [FIDO2 security keys](https://learn.microsoft.com/entra/identity/authentication/concept-authentication-passwordless) | Passwordless authentication methods |
| [Temporary Access Pass](https://learn.microsoft.com/entra/identity/authentication/howto-authentication-temporary-access-pass) | TAP overview |
| [Authentication methods policy](https://learn.microsoft.com/entra/identity/authentication/concept-authentication-methods-manage) | Managing authentication methods |
| [Microsoft Learn – Authentication methods](https://learn.microsoft.com/training/modules/describe-authentication-capabilities-azure-ad/) | Microsoft Learn module |
