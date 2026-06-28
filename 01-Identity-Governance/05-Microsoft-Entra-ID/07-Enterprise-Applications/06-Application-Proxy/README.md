# Application Proxy

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Microsoft Entra Application Proxy securely publishes on-premises web applications without exposing the internal network directly to the Internet.

---

## Application Proxy Architecture

```text
                Internet
                    │
                    ▼
         Microsoft Entra ID
                    │
        Pre-Authentication
                    │
                    ▼
        Application Proxy Service
                    │
        Outbound HTTPS Connection
                    │
                    ▼
     Application Proxy Connector
      (On-Premises Network)
                    │
                    ▼
      Internal Web Application
```

---

> [!TIP]
> **Key Concepts**
>
> - Application Proxy securely publishes internal web applications.
> - No inbound firewall ports are required.
> - Authentication is performed by Microsoft Entra ID.
> - Connectors maintain outbound HTTPS connections.
> - Conditional Access and Single Sign-On are fully supported.

---

## Overview

Microsoft Entra Application Proxy enables organizations to provide secure remote access to on-premises web applications.

Instead of exposing internal applications directly to the Internet through reverse proxies or VPNs, Microsoft Entra ID brokers the connection between authenticated users and internal applications.

This approach improves security while simplifying remote access.

---

## Why Application Proxy Exists

Organizations often need to provide remote access to internal web applications.

Traditional solutions usually require:

- VPN connections
- Reverse proxies
- Firewall port forwarding
- DMZ infrastructure

Application Proxy eliminates these requirements by using Microsoft Entra ID as the secure access gateway.

---

## Components

Application Proxy consists of several components.

| Component | Purpose |
|-----------|---------|
| Microsoft Entra ID | Authenticates users. |
| Application Proxy Service | Secure cloud gateway. |
| Application Proxy Connector | Maintains outbound connectivity from the internal network. |
| Internal Application | Published on-premises web application. |

---

## Connector

The Application Proxy Connector is installed inside the internal network.

It establishes an outbound HTTPS connection to Microsoft Entra ID.

Because the connector initiates the connection, organizations typically do not need to open inbound firewall ports.

Multiple connectors can be deployed for redundancy and load balancing.

---

## Authentication Flow

```text
User
 │
 ▼
External URL
 │
 ▼
Microsoft Entra ID
 │
 ▼
User Authentication
 │
 ▼
Conditional Access
 │
 ▼
Application Proxy Service
 │
 ▼
Proxy Connector
 │
 ▼
Internal Application
```

Only authenticated users are allowed to reach the internal application.

---

## Pre-Authentication

Application Proxy supports different authentication models.

| Method | Description |
|--------|-------------|
| Microsoft Entra ID | Users authenticate before accessing the application. |
| Passthrough | Authentication is handled directly by the application. |

Microsoft Entra ID pre-authentication provides stronger security because Conditional Access, MFA, and identity-based policies are evaluated before traffic reaches the internal application.

---

## Single Sign-On

Application Proxy integrates with Microsoft Entra Single Sign-On.

Depending on the application, supported methods include:

- Kerberos Constrained Delegation (KCD)
- Header-based authentication
- Password-based Single Sign-On
- Integrated Windows Authentication (IWA)

This allows users to access internal applications without entering additional credentials.

---

## Conditional Access

Because authentication occurs through Microsoft Entra ID, Application Proxy supports:

- Multi-Factor Authentication (MFA)
- Device compliance
- Named locations
- Sign-in risk policies
- User risk policies

Conditional Access policies are evaluated before users reach the application.

---

## Enterprise Scenario

A company hosts an internal HR portal in its on-premises datacenter.

Employees working remotely need secure access without using a VPN.

The organization publishes the application through Microsoft Entra Application Proxy.

Users authenticate with Microsoft Entra ID, complete MFA, and are securely connected to the internal application through the Application Proxy Connector.

---

## Best Practices

- Prefer Microsoft Entra ID pre-authentication.
- Deploy multiple connectors for high availability.
- Protect applications with Conditional Access.
- Enable Single Sign-On whenever possible.
- Monitor connector health regularly.
- Publish only required applications.

---

## Common Pitfalls

- Installing only one connector.
- Using Passthrough authentication unnecessarily.
- Forgetting Conditional Access policies.
- Publishing unnecessary internal applications.
- Ignoring connector health monitoring.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Microsoft Entra Application Proxy
> - Connector
> - Pre-authentication
> - Conditional Access integration
> - Single Sign-On
> - Secure remote access

---

## Key Takeaways

- Application Proxy securely publishes internal web applications.
- No inbound firewall ports are required.
- Connectors establish outbound HTTPS connections.
- Microsoft Entra ID authenticates users before application access.
- Conditional Access and SSO integrate natively with Application Proxy.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [What is Microsoft Entra Application Proxy?](https://learn.microsoft.com/entra/identity/app-proxy/what-is-app-proxy) | Application Proxy overview |
| [Application Proxy connectors](https://learn.microsoft.com/entra/identity/app-proxy/application-proxy-connectors) | Connector architecture |
| [Plan an Application Proxy deployment](https://learn.microsoft.com/entra/identity/app-proxy/application-proxy-deployment-plan) | Deployment planning |
| [Configure Microsoft Entra Application Proxy](https://learn.microsoft.com/entra/identity/app-proxy/application-proxy-add-on-premises-application) | Publishing on-premises applications |
| [Microsoft Learn – Secure remote access with Microsoft Entra Application Proxy](https://learn.microsoft.com/training/modules/publish-app-with-azure-ad-application-proxy/) | Microsoft Learn module |
