# Monitoring and Logs

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra ID provides monitoring, auditing, and troubleshooting capabilities for Enterprise Applications.

---

## Monitoring Overview

```text
           Enterprise Application
                     │
                     ▼
             User Activity
                     │
                     ▼
        Microsoft Entra ID Logs
                     │
     ┌───────────────┼───────────────┐
     │               │               │
     ▼               ▼               ▼
 Sign-in Logs   Audit Logs   Provisioning Logs
     │               │               │
     └───────────────┼───────────────┘
                     ▼
        Investigation & Monitoring
```

---

> [!TIP]
> **Key Concepts**
>
> - Microsoft Entra ID records authentication and administrative events.
> - Sign-in Logs capture authentication activity.
> - Audit Logs record configuration changes.
> - Provisioning Logs track synchronization events.
> - Monitoring supports security, compliance, and troubleshooting.

---

## Overview

Microsoft Entra ID continuously records events related to Enterprise Applications.

These logs help administrators:

- Investigate authentication failures.
- Review administrative changes.
- Monitor provisioning operations.
- Detect suspicious activity.
- Support compliance and auditing.

---

## Sign-in Logs

Sign-in Logs record every authentication attempt.

Typical information includes:

- User
- Application
- Timestamp
- IP address
- Device information
- Authentication method
- Conditional Access result
- Sign-in status

Sign-in Logs are the primary source for investigating authentication issues.

---

## Audit Logs

Audit Logs record administrative changes made within Microsoft Entra ID.

Examples include:

- Application creation
- Enterprise Application configuration
- User assignments
- Group assignments
- Consent granted
- Conditional Access modifications
- Credential updates

Audit Logs help administrators understand who changed what and when.

---

## Provisioning Logs

Provisioning Logs record synchronization activity between Microsoft Entra ID and connected applications.

Typical events include:

- User creation
- Attribute updates
- Group synchronization
- Account disablement
- Account deletion
- Provisioning failures

Provisioning Logs are essential when troubleshooting SCIM synchronization.

---

## Log Retention

Microsoft Entra ID stores logs for a limited period depending on the organization's licensing.

| Log Type | Microsoft Entra ID Free | Microsoft Entra ID P1 / P2 |
|----------|-------------------------|----------------------------|
| **Sign-in Logs** | 7 days | 30 days |
| **Audit Logs** | 30 days | 30 days |
| **Provisioning Logs** | 30 days | 30 days |

Organizations requiring longer retention should export logs to external Azure services before the native retention period expires.

---

## Diagnostic Settings

To retain Microsoft Entra ID logs beyond the native retention period, administrators can configure **Diagnostic Settings**.

Diagnostic Settings allow selected log categories, such as:

- SignInLogs
- AuditLogs
- ProvisioningLogs

to be sent to one or more Azure destinations.

| Destination | Typical Use Case |
|-------------|------------------|
| **Log Analytics Workspace** | KQL queries, dashboards, alerts, and investigations. |
| **Azure Storage Account** | Long-term archival at low cost. |
| **Azure Event Hubs** | Streaming logs to external SIEM platforms such as Microsoft Sentinel or Splunk. |

This enables long-term monitoring, compliance, and advanced security analytics.

---

## Troubleshooting

Administrators commonly use Microsoft Entra ID logs to investigate:

- Failed sign-ins
- MFA failures
- Conditional Access blocks
- Consent failures
- Provisioning errors
- Application access issues

Combining multiple log sources often provides the complete picture.

---

## Conditional Access Insights

Sign-in Logs include Conditional Access evaluation results.

Administrators can determine whether access was:

- Granted
- Blocked
- Interrupted by MFA
- Blocked by device compliance
- Blocked by sign-in risk
- Blocked by user risk

This information is critical when troubleshooting authentication issues.

---

## Report-only Policies

Conditional Access policies can operate in **Report-only** mode.

When enabled, Microsoft Entra ID evaluates the policy during sign-in but does not enforce its controls.

Administrators can review the Sign-in Logs to determine whether the policy would have:

- Granted access
- Required Multi-Factor Authentication (MFA)
- Blocked the sign-in

Report-only mode allows organizations to validate Conditional Access policies before enabling them in production.

---

## Monitoring Enterprise Applications

Administrators should regularly review:

- Sign-in frequency
- Failed authentication attempts
- Administrator consent changes
- Unused Enterprise Applications
- Expiring certificates
- Expiring client secrets

Routine monitoring improves security and operational stability.

---

## Enterprise Scenario

A user reports that access to an internal HR application suddenly stopped working.

The administrator reviews the Sign-in Logs and discovers that Conditional Access blocked the sign-in because the device was no longer compliant.

After the device regains compliance, authentication succeeds without modifying the Enterprise Application.

---

## Best Practices

- Review Sign-in Logs regularly.
- Monitor Audit Logs for administrative changes.
- Investigate repeated authentication failures.
- Export logs for long-term retention.
- Review expiring credentials.
- Monitor provisioning synchronization.

---

## Common Pitfalls

- Ignoring failed sign-ins.
- Not reviewing administrator activity.
- Forgetting log retention limitations.
- Troubleshooting without checking Conditional Access results.
- Leaving unused Enterprise Applications unmanaged.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Sign-in Logs
> - Audit Logs
> - Provisioning Logs
> - Conditional Access reporting
> - Troubleshooting Enterprise Applications
> - Monitoring authentication activity

---

## Key Takeaways

- Sign-in Logs record authentication activity.
- Audit Logs record administrative changes.
- Provisioning Logs record identity synchronization.
- Conditional Access results appear in Sign-in Logs.
- Monitoring improves security, compliance, and troubleshooting.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Sign-in logs in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/monitoring-health/concept-sign-ins) | Sign-in Logs |
| [Audit logs in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/monitoring-health/concept-audit-logs) | Audit Logs |
| [Provisioning logs in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/monitoring-health/concept-provisioning-logs) | Provisioning Logs |
| [Integrate Microsoft Entra logs with Azure Monitor](https://learn.microsoft.com/entra/identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs) | Azure Monitor integration |
| [Microsoft Learn – Monitor and troubleshoot Microsoft Entra ID](https://learn.microsoft.com/training/modules/monitor-troubleshoot-azure-active-directory/) | Microsoft Learn module |
