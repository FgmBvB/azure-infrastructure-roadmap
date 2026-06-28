# Multi-Factor Authentication (MFA) Best Practices

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It summarizes Microsoft's recommended practices for designing, deploying, and maintaining Multi-Factor Authentication (MFA) in Microsoft Entra ID.

---

## MFA Deployment Lifecycle

```text
Plan MFA
    │
    ▼
Enable Authentication Methods
    │
    ▼
Register Users
    │
    ▼
Apply Conditional Access
    │
    ▼
Monitor Sign-ins
    │
    ▼
Review and Improve
```

---

> [!TIP]
> **Key Concepts**
>
> - Protect every privileged account with MFA.
> - Prefer phishing-resistant authentication methods.
> - Enforce MFA through Conditional Access.
> - Require users to register multiple authentication methods.
> - Continuously monitor authentication activity.

---

## Overview

Multi-Factor Authentication is one of the most effective security controls available in Microsoft Entra ID.

Microsoft recommends combining MFA with Conditional Access, modern authentication, and passwordless technologies as part of a Zero Trust security strategy.

---

## Protect Privileged Accounts

Administrative accounts should always require strong authentication.

Recommendations include:

- Require MFA for all administrator accounts.
- Use phishing-resistant authentication methods whenever possible.
- Protect privileged roles with Conditional Access.
- Review privileged sign-ins regularly.

Privileged accounts are frequent targets for attackers and require additional protection.

---

## Prefer Modern Authentication Methods

Microsoft recommends using modern authentication methods instead of legacy verification mechanisms.

Recommended order:

1. FIDO2 Security Keys
2. Windows Hello for Business
3. Microsoft Authenticator
4. OATH Tokens
5. SMS
6. Voice Call

Phishing-resistant authentication provides the highest level of protection.

---

## Use Conditional Access

Microsoft recommends enforcing MFA through Conditional Access instead of legacy per-user MFA.

Conditional Access enables administrators to require MFA based on:

- Users or groups
- Applications
- Device state
- Locations
- Risk conditions
- Authentication strengths

This provides flexible, risk-based authentication.

---

## Register Multiple Authentication Methods

Users should register more than one authentication method.

Examples include:

- Microsoft Authenticator
- FIDO2 Security Key
- Windows Hello for Business
- Temporary Access Pass
- SMS (backup only)

Multiple methods simplify recovery when a primary device is unavailable.

---

## Enable Combined Registration

Microsoft recommends enabling **Combined Security Information Registration**.

This allows users to register authentication methods and Self-Service Password Reset (SSPR) information through a single registration experience.

Combined registration simplifies onboarding and improves the user experience.

---

## Protect Emergency Access Accounts

Organizations should maintain emergency (break-glass) accounts.

Recommendations:

- Exclude them from Conditional Access policies.
- Use long, complex passwords.
- Monitor sign-in activity.
- Store credentials securely.
- Test access regularly.

Emergency accounts should only be used when normal authentication mechanisms are unavailable.

---

## Monitor Authentication Activity

Administrators should regularly review:

- Sign-in Logs
- Authentication Methods registration
- MFA failures
- Risk detections
- Conditional Access results
- Suspicious sign-in activity

Monitoring helps detect compromised identities and configuration issues.

---

## Support Passwordless Authentication

Where supported, organizations should adopt passwordless authentication.

Benefits include:

- Improved user experience.
- Reduced phishing risk.
- Fewer password-related support requests.
- Stronger authentication.

Passwordless authentication aligns with Microsoft's Zero Trust recommendations.

---

## Enterprise Scenario

A company secures Microsoft 365 using Conditional Access.

All privileged accounts authenticate with FIDO2 Security Keys or Microsoft Authenticator, while standard users register Microsoft Authenticator and a backup authentication method through Combined Registration.

Conditional Access requires MFA only when organizational policies determine that additional verification is necessary, and Sign-in Logs are reviewed regularly to detect suspicious authentication attempts.

---

## Best Practices Checklist

- Require MFA for all privileged accounts.
- Prefer phishing-resistant authentication methods.
- Use Conditional Access instead of per-user MFA.
- Enable Combined Registration.
- Register multiple authentication methods.
- Deploy passwordless authentication where possible.
- Protect emergency access accounts.
- Monitor Sign-in Logs regularly.
- Review Authentication Methods policies periodically.
- Educate users about phishing and MFA fatigue attacks.

---

## Common Pitfalls

- Using SMS as the primary authentication method.
- Relying on legacy per-user MFA.
- Registering only one authentication method.
- Forgetting emergency access accounts.
- Ignoring Sign-in Logs.
- Failing to review Conditional Access policies regularly.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - MFA deployment recommendations
> - Authentication method selection
> - Conditional Access integration
> - Combined Registration
> - Passwordless authentication
> - Emergency access accounts

---

## Key Takeaways

- Multi-Factor Authentication is a core security control in Microsoft Entra ID.
- Microsoft recommends enforcing MFA through Conditional Access.
- Phishing-resistant authentication methods provide the strongest protection.
- Multiple authentication methods improve resilience and recovery.
- Continuous monitoring and periodic policy reviews strengthen organizational security.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Microsoft Entra Multifactor Authentication](https://learn.microsoft.com/entra/identity/authentication/concept-mfa-howitworks) | MFA overview |
| [Authentication methods in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/authentication/concept-authentication-methods) | Authentication methods |
| [Authentication strengths](https://learn.microsoft.com/entra/identity/authentication/concept-authentication-strengths) | Phishing-resistant authentication |
| [Combined security information registration](https://learn.microsoft.com/entra/identity/authentication/concept-registration-mfa-sspr-combined) | Combined Registration |
| [Emergency access accounts](https://learn.microsoft.com/entra/identity/role-based-access-control/security-emergency-access) | Break-glass accounts |
| [Microsoft Learn – Describe Microsoft Entra multifactor authentication](https://learn.microsoft.com/training/modules/describe-authentication-capabilities-azure-ad/) | Microsoft Learn module |
