# Conditional Access

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the **Microsoft AZ-104: Microsoft Azure Administrator** certification.
>
> It covers Microsoft Entra Conditional Access, including policy design, assignments, conditions, Grant Controls, Session Controls, monitoring, and security best practices.

---

## Overview

Microsoft Entra Conditional Access is Microsoft's policy engine for identity-based access control.

It evaluates every authentication request using identity, device, application, location, and risk signals before determining whether access should be granted, blocked, or require additional security controls.

Conditional Access is one of the core security features of Microsoft Entra ID and a fundamental component of Microsoft's Zero Trust architecture.

---

## Learning Objectives

After completing this section you should be able to:

- Understand the Conditional Access evaluation process.
- Configure policy assignments and conditions.
- Apply Grant Controls and Session Controls.
- Deploy Conditional Access safely using Report-only mode.
- Protect identities using risk-based policies.
- Apply Microsoft's security best practices.

---

## Module Structure

| Module | Description |
|---------|-------------|
| **01 - Overview** | Conditional Access architecture, policy evaluation, Zero Trust, and Report-only mode. |
| **02 - Policies and Conditions** | Assignments, users, groups, applications, locations, client applications, risk conditions, and Device Filters. |
| **03 - Grant and Session Controls** | Grant Controls, Authentication Strengths, Session Controls, Continuous Access Evaluation (CAE), and Application-Enforced Restrictions. |
| **04 - Best Practices** | Deployment recommendations, emergency access accounts, monitoring, and operational guidance. |

---

## Architecture

```text
              User Sign-in
                    │
                    ▼
         Microsoft Entra ID
                    │
                    ▼
        Conditional Access Policy
                    │
        ┌───────────┼───────────┐
        │           │           │
        ▼           ▼           ▼
 Assignments   Conditions   Risk Signals
                    │
                    ▼
      Grant & Session Controls
                    │
                    ▼
      Access Granted / Blocked
```

---

## Skills Covered

This section includes:

- Conditional Access
- Zero Trust
- Policy Assignments
- Policy Conditions
- Named Locations
- Client Applications
- Device Filters
- Sign-in Risk
- User Risk
- Grant Controls
- Session Controls
- Authentication Strengths
- Report-only Mode
- Continuous Access Evaluation (CAE)
- Application-Enforced Restrictions
- Emergency Access Accounts

---

## AZ-104 Exam Focus

This section aligns with the Microsoft AZ-104 objectives related to:

- Configure Conditional Access policies.
- Protect users and applications.
- Configure policy assignments and conditions.
- Require Multi-Factor Authentication (MFA).
- Configure Grant Controls and Session Controls.
- Monitor and troubleshoot Conditional Access policies.

---

## Key Takeaways

- Conditional Access evaluates every sign-in before access is granted.
- Policies combine assignments, conditions, and security controls.
- Report-only mode enables safe policy validation before production deployment.
- Grant Controls determine whether access is allowed, while Session Controls secure authenticated sessions.
- Conditional Access is a fundamental pillar of Microsoft's Zero Trust security model.
