# Conditional Access Best Practices

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It summarizes Microsoft's recommended practices for designing, deploying, and maintaining Conditional Access policies.

---

## Deployment Lifecycle

```text
Plan Policies
      │
      ▼
Create Assignments
      │
      ▼
Configure Conditions
      │
      ▼
Configure Grant Controls
      │
      ▼
Test with Report-only
      │
      ▼
Enable Policy
      │
      ▼
Monitor and Review
```

---

> [!TIP]
> **Key Concepts**
>
> - Follow the principle of least privilege.
> - Test policies before enforcement.
> - Protect privileged accounts.
> - Prefer modern authentication.
> - Review policies regularly.

---

## Overview

Conditional Access is one of the most important security controls in Microsoft Entra ID.

Well-designed policies improve security while minimizing disruption for end users.

---

## Build Policies Gradually

Microsoft recommends deploying Conditional Access incrementally.

Start with:

- Report-only mode
- Small pilot groups
- Validation through Sign-in Logs

Expand policies only after successful testing.

---

## Protect Administrative Accounts

Administrative accounts should receive the highest level of protection.

Recommendations include:

- Require phishing-resistant MFA whenever possible.
- Require strong Authentication Strengths.
- Monitor administrator sign-ins.
- Protect privileged roles with dedicated policies.

---

## Protect Emergency Access Accounts

Maintain at least two emergency (break-glass) accounts.

Recommendations:

- Exclude them from all Conditional Access policies.
- Store credentials securely.
- Monitor sign-ins.
- Test them regularly.

These accounts help prevent tenant lockout.

---

## Block Legacy Authentication

Legacy authentication protocols do not support modern security controls.

Microsoft recommends creating a dedicated Conditional Access policy that blocks legacy authentication clients.

---

## Use Named Locations Carefully

Use Named Locations to identify trusted corporate networks.

Avoid creating unnecessary exclusions based only on location.

Location should complement—not replace—other security controls.

---

## Use Authentication Strengths

Authentication Strengths allow organizations to require stronger authentication methods for sensitive applications and privileged accounts.

Prefer phishing-resistant authentication whenever possible.

---

## Monitor Policy Effectiveness

Regularly review:

- Sign-in Logs
- Conditional Access Insights
- Report-only results
- Risk detections
- Policy failures

Monitoring helps identify configuration issues and security risks.

---

## Enterprise Scenario

A company deploys Conditional Access in phases.

Policies are first tested using Report-only mode, validated through Sign-in Logs, and then enabled for progressively larger groups.

Administrative accounts require phishing-resistant MFA, while emergency access accounts remain excluded from all Conditional Access policies.

---

## Best Practices Checklist

- Deploy policies gradually.
- Use Report-only before production.
- Require MFA for privileged accounts.
- Prefer Authentication Strengths.
- Block legacy authentication.
- Protect emergency access accounts.
- Monitor Sign-in Logs regularly.
- Review policies periodically.
- Apply the principle of least privilege.

---

## Common Pitfalls

- Enabling policies without testing.
- Forgetting emergency access accounts.
- Allowing legacy authentication.
- Creating unnecessary policy overlap.
- Ignoring Sign-in Logs.
- Using broad exclusions.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Policy deployment strategy
> - Report-only mode
> - Authentication Strengths
> - Emergency access accounts
> - Legacy authentication
> - Conditional Access monitoring

---

## Key Takeaways

- Deploy Conditional Access policies gradually.
- Test policies using Report-only mode before enforcement.
- Protect privileged identities with strong authentication.
- Block legacy authentication whenever possible.
- Continuous monitoring ensures effective security.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Conditional Access overview](https://learn.microsoft.com/entra/identity/conditional-access/overview) | Conditional Access concepts |
| [Conditional Access best practices](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-best-practices) | Microsoft recommendations |
| [Authentication strengths](https://learn.microsoft.com/entra/identity/authentication/concept-authentication-strengths) | Strong authentication |
| [Emergency access accounts](https://learn.microsoft.com/entra/identity/role-based-access-control/security-emergency-access) | Break-glass accounts |
| [Microsoft Learn – Conditional Access](https://learn.microsoft.com/training/modules/describe-authentication-capabilities-azure-ad/) | Microsoft Learn module |
