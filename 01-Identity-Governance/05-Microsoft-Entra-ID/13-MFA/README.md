# Multi-Factor Authentication (MFA)

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Microsoft Entra Multi-Factor Authentication (MFA), authentication methods, Conditional Access integration, and Microsoft's recommended deployment practices.

---

## Overview

Microsoft Entra Multi-Factor Authentication (MFA) strengthens user authentication by requiring an additional verification factor beyond a password.

By combining something the user knows, has, or is, MFA significantly reduces the risk of credential theft, phishing attacks, and unauthorized access.

MFA is a fundamental component of Microsoft's Zero Trust security model and is one of the primary security controls evaluated in the AZ-104 certification.

---

## Learning Objectives

After completing this section you should be able to:

- Understand how Microsoft Entra MFA works.
- Configure supported authentication methods.
- Integrate MFA with Conditional Access.
- Deploy MFA securely across an organization.
- Troubleshoot common authentication issues.
- Apply Microsoft security recommendations.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | MFA architecture, authentication factors, and authentication flow. |
| **02 - Authentication Methods** | Microsoft Authenticator, FIDO2, Windows Hello for Business, SMS, Voice, TAP, and OATH tokens. |
| **03 - Conditional Access** | Requiring MFA through Conditional Access policies and authentication strengths. |
| **04 - Best Practices** | Deployment strategy, security recommendations, and operational guidance. |

---

## Architecture

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
      Multi-Factor Authentication
              │
      ┌───────┼────────┐
      │       │        │
      ▼       ▼        ▼
Authenticator FIDO2   Windows Hello
      │
      ▼
 Authentication Success
      │
      ▼
 Protected Resource
```

---

## Skills Covered

This section includes:

- Multi-Factor Authentication (MFA)
- Authentication Methods
- Microsoft Authenticator
- FIDO2 Security Keys
- Windows Hello for Business
- Temporary Access Pass (TAP)
- OATH Tokens
- SMS Authentication
- Voice Authentication
- Conditional Access
- Authentication Strengths
- Passwordless Authentication
- Zero Trust

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Configure Multi-Factor Authentication.
- Manage authentication methods.
- Protect privileged accounts.
- Integrate MFA with Conditional Access.
- Deploy passwordless authentication.
- Troubleshoot authentication challenges.

---

## Key Takeaways

- Multi-Factor Authentication significantly improves identity security.
- Microsoft Entra ID supports multiple authentication methods.
- Conditional Access is the recommended way to enforce MFA.
- Passwordless authentication improves both security and user experience.
- MFA is a core component of Microsoft's Zero Trust strategy.
