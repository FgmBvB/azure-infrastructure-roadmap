# Hybrid Authentication Methods

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains the authentication methods available for Hybrid Identity deployments and compares their architecture, advantages, and typical use cases.

---

## Authentication Models

```text
                  User
                    │
                    ▼
          Microsoft Entra ID
                    │
        ┌───────────┼───────────┐
        │           │           │
        ▼           ▼           ▼
       PHS         PTA      Federation
        │           │           │
        ▼           ▼           ▼
 Password      Active       AD FS /
 Hash Sync     Directory    Federation Service
```

---

> [!TIP]
> **Key Concepts**
>
> - Hybrid Identity supports multiple authentication methods.
> - Authentication methods determine where passwords are validated.
> - All methods support Single Sign-On (SSO).
> - The appropriate method depends on business and security requirements.
> - Password Hash Synchronization is Microsoft's recommended option for most organizations.

---

## Overview

Microsoft Entra ID supports several authentication methods for hybrid environments.

Although all methods allow users to authenticate to cloud services using their corporate identities, they differ in where authentication occurs and which infrastructure is required.

---

## Password Hash Synchronization (PHS)

Password Hash Synchronization synchronizes a hash of the user's password hash from Active Directory to Microsoft Entra ID.

Authentication occurs entirely in Microsoft Entra ID.

---

### Password Hash Synchronization Security

Password Hash Synchronization does not synchronize the user's plain-text password to Microsoft Entra ID.

It also does not synchronize the original Active Directory password hash directly.

Microsoft Entra Connect processes the on-premises password hash before synchronizing it to Microsoft Entra ID, making the cloud-stored hash different from the original Active Directory hash.

Password Hash Synchronization can also be enabled as a backup authentication method when using Pass-through Authentication or Federation.

This provides resilience if on-premises authentication infrastructure becomes unavailable.

---

### Advantages

- Simplest deployment.
- High availability.
- No dependency on on-premises infrastructure during authentication.
- Supports modern Microsoft Entra security features.

### Considerations

- Password hashes are synchronized.
- Authentication is performed in the cloud.

---

## Pass-through Authentication (PTA)

Pass-through Authentication validates passwords directly against the on-premises Active Directory.

Microsoft Entra ID forwards the authentication request to a PTA agent installed on-premises.

---

### PTA Network Requirements

Pass-through Authentication agents establish outbound connections to Microsoft services.

No inbound firewall ports are required from the Internet to the on-premises network.

PTA agents communicate with Microsoft Entra ID using outbound HTTPS traffic, typically over TCP port 443.

This reduces perimeter network exposure compared with traditional federation infrastructure.

---

### Advantages

- Passwords remain on-premises.
- No password hashes stored for authentication in the cloud.
- Supports seamless integration with existing Active Directory environments.

### Considerations

- Requires one or more PTA agents.
- Authentication depends on connectivity with the on-premises environment.

---

## Federation

Federation delegates authentication to an external identity provider, typically Active Directory Federation Services (AD FS).

Microsoft Entra ID redirects authentication requests to the federation service.

### Advantages

- Full control over authentication policies.
- Supports advanced authentication scenarios.
- Existing federation infrastructures can be reused.

### Considerations

- Highest infrastructure complexity.
- Requires federation servers and additional maintenance.
- Microsoft generally recommends simpler authentication methods unless federation features are specifically required.

---

## Authentication Comparison

| Feature | PHS | PTA | Federation |
|---------|-----|-----|------------|
| Password validation | Microsoft Entra ID | Active Directory | Federation service |
| Internet dependency | No on-premises dependency | PTA Agent required | Federation infrastructure required |
| Infrastructure complexity | Low | Medium | High |
| High availability | High | Agent redundancy recommended | Requires highly available federation infrastructure |
| Microsoft recommendation | Yes (most scenarios) | Supported | Specific business requirements |

---

## Seamless Single Sign-On

**Seamless Single Sign-On (Seamless SSO)** allows users on domain-joined corporate devices to access Microsoft Entra ID integrated applications without repeatedly entering credentials.

It is commonly used together with Password Hash Synchronization or Pass-through Authentication.

During configuration, Microsoft Entra Connect creates a computer account in on-premises Active Directory named `AZUREADSSOACC`.

Seamless SSO uses Kerberos to authenticate users silently when they access supported Microsoft Entra ID services from the corporate network.

For browser-based SSO, administrators typically configure Group Policy so that the following URL is part of the Local Intranet zone:

```text
https://autologon.microsoftazuread-sso.com
```

This enables Integrated Windows Authentication for supported browsers and clients.

---

## Authentication Flow

```text
          User
            │
            ▼
 Microsoft Entra ID
            │
   ┌────────┼─────────┐
   │        │         │
   ▼        ▼         ▼
  PHS      PTA   Federation
   │        │         │
   ▼        ▼         ▼
Cloud     AD DS     AD FS
```

---

## Choosing the Right Method

| Requirement | Recommended Method |
|------------|--------------------|
| Cloud-first deployment | Password Hash Synchronization |
| Password validation must remain on-premises | Pass-through Authentication |
| Existing AD FS deployment | Federation |
| Lowest operational complexity | Password Hash Synchronization |
| Highest customization of authentication | Federation |

---

## Enterprise Scenario

A company migrates from an on-premises Active Directory environment to Microsoft 365.

To minimize infrastructure and improve resiliency, the organization deploys Password Hash Synchronization.

Employees continue using their existing corporate credentials while authentication is handled directly by Microsoft Entra ID.

---

## Best Practices

- Prefer Password Hash Synchronization unless business requirements dictate otherwise.
- Deploy multiple PTA agents when using Pass-through Authentication.
- Use Federation only when advanced federation capabilities are required.
- Monitor authentication health regularly.
- Protect privileged accounts with Multi-Factor Authentication.
- Test authentication before migrating production users.

---

## Common Pitfalls

- Choosing Federation without a business requirement.
- Deploying only one PTA agent.
- Assuming all authentication methods provide identical infrastructure requirements.
- Failing to monitor authentication services.
- Underestimating federation maintenance requirements.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> - Password Hash Synchronization (PHS)
> - Pass-through Authentication (PTA)
> - Federation
> - Authentication flow
> - Authentication method selection
> - Microsoft recommendations

---

## Key Takeaways

- Microsoft Entra ID supports multiple hybrid authentication methods.
- Password Hash Synchronization is the recommended option for most organizations.
- Pass-through Authentication validates passwords on-premises.
- Federation delegates authentication to an external identity provider.
- Authentication method selection should balance security, availability, and operational complexity.

---

## References

| Microsoft Documentation | Purpose |
|-------------------------|---------|
| [Choose the right authentication method](https://learn.microsoft.com/entra/identity/hybrid/connect/choose-ad-authn) | Compare PHS, PTA, and Federation |
| [Password Hash Synchronization](https://learn.microsoft.com/entra/identity/hybrid/connect/how-to-connect-password-hash-synchronization) | PHS architecture and configuration |
| [Pass-through Authentication](https://learn.microsoft.com/entra/identity/hybrid/connect/how-to-connect-pta) | PTA architecture and deployment |
| [Federation with AD FS](https://learn.microsoft.com/entra/identity/hybrid/connect/how-to-connect-fed-whatis) | Federation concepts |
| [Microsoft Learn – Plan a hybrid identity solution](https://learn.microsoft.com/training/modules/plan-design-identity-solution/) | Microsoft Learn module |
