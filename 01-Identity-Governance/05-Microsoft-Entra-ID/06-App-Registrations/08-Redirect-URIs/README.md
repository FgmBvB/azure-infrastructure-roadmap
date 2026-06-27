# Redirect URIs

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains how Redirect URIs allow Microsoft Entra ID to securely return authentication responses to registered applications.

---

## Authentication Flow

```text
        User
          │
          ▼
 Application
          │
Redirect to
Microsoft Entra ID
          │
          ▼
User Authentication
          │
          ▼
Authentication Response
          │
          ▼
Registered Redirect URI
          │
          ▼
Application
```

---

> [!TIP]
> **Key Concepts**
>
> * Redirect URIs identify where Microsoft Entra ID returns authentication responses.
> * Every Redirect URI must be registered in the App Registration.
> * Exact URI matching is required.
> * Redirect URIs help prevent redirection attacks.
> * Different application types require different Redirect URI formats.

---

## Overview

A Redirect URI (also called a Reply URL) specifies the destination where Microsoft Entra ID sends the authentication response after a user successfully signs in.

Before redirecting the user, Microsoft Entra ID validates that the destination exactly matches one of the Redirect URIs configured in the App Registration.

If no matching Redirect URI exists, authentication is rejected.

---

## Why Redirect URIs Exist

Without Redirect URIs, Microsoft Entra ID would have no trusted destination for returning authentication responses.

An attacker could attempt to redirect authentication responses to a malicious application.

By validating the Redirect URI against the registered values, Microsoft Entra ID ensures that authentication responses are returned only to trusted locations.

---

## Redirect URI Validation

Microsoft Entra ID validates Redirect URIs using exact matching.

The following components must match the registered value:

* Protocol (HTTPS)
* Domain
* Port (when applicable)
* Path

Any mismatch causes the authentication request to fail.

---

## Redirect URI Restrictions

For security reasons, Redirect URIs must be explicitly defined.

Microsoft Entra ID does not support wildcard (`*`) characters in Redirect URIs because they could allow open redirect attacks.

Each Redirect URI must be individually registered.

Redirect URIs are also subject to platform-specific length and formatting limitations.

---

## Local Development

Microsoft Entra ID requires HTTPS for Redirect URIs in production environments.

However, an exception exists for local development.

Applications can use HTTP when the Redirect URI points to `localhost`, for example:

```text
http://localhost:3000/signin-oidc
```

This allows developers to test applications locally without configuring SSL certificates.

Microsoft recommends using HTTPS for all production deployments.

---

## Supported Application Types

Different application types use different Redirect URI formats.

| Application Type              | Typical Redirect URI                       |
| ----------------------------- | ------------------------------------------ |
| Web Application               | `https://contoso.com/signin-oidc`          |
| Single-Page Application (SPA) | `https://contoso.com`                      |
| Mobile/Desktop Application    | `http://localhost` or custom URI scheme    |
| Native Client                 | Loopback or platform-specific redirect URI |

The available Redirect URI options depend on the application platform selected during registration.

---

## Security Considerations

Redirect URIs are a critical security control.

Microsoft recommends:

* Register only trusted Redirect URIs.
* Use HTTPS whenever possible.
* Remove unused Redirect URIs.
* Avoid overly broad redirect configurations.

Applications should never accept arbitrary Redirect URIs supplied by users.

---

## Enterprise Scenario

A company deploys an internal web application hosted at:

```text
https://portal.contoso.com
```

The App Registration includes:

```text
https://portal.contoso.com/signin-oidc
```

After users authenticate with Microsoft Entra ID, they are redirected only to the registered URI.

If an attacker attempts to modify the destination, Microsoft Entra ID rejects the authentication request because the Redirect URI does not match the registered value.

---

## Best Practices

* Register only required Redirect URIs.
* Use HTTPS in production.
* Remove obsolete Redirect URIs.
* Validate application URLs before registration.
* Separate development and production Redirect URIs.
* Review Redirect URI configuration periodically.

---

## Common Authentication Error

One of the most common Redirect URI configuration errors is:

```text
AADSTS50011

The reply URL specified in the request does not match the reply URLs configured for the application.
```

This error occurs when the Redirect URI sent by the application does not exactly match any Redirect URI registered in the App Registration.

Administrators should verify the protocol, domain, port, and path when troubleshooting this error.

---

## Common Pitfalls

* Forgetting to register the Redirect URI.
* Typographical errors in Redirect URIs.
* Using HTTP in production environments.
* Leaving unused Redirect URIs configured.
* Assuming partial URI matching is supported.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> * Redirect URIs
> * Reply URLs
> * Exact URI matching
> * Redirect URI validation
> * Supported application platforms
> * Redirect URI security

---

## Key Takeaways

* Redirect URIs define where Microsoft Entra ID returns authentication responses.
* Every Redirect URI must be registered in advance.
* Microsoft Entra ID validates Redirect URIs using exact matching.
* Redirect URIs help prevent authentication redirection attacks.
* Proper Redirect URI management improves application security.

---

## References

| Microsoft Documentation                                                                                                                          | Purpose                                         |
| ------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------- |
| [Redirect URI (reply URL) restrictions and limitations](https://learn.microsoft.com/entra/identity-platform/reply-url)                           | Redirect URI configuration and validation       |
| [Register an application](https://learn.microsoft.com/entra/identity-platform/quickstart-register-app)                                           | Configure Redirect URIs during App Registration |
| [Authentication and authorization basics](https://learn.microsoft.com/entra/identity-platform/authentication-vs-authorization)                   | Authentication process overview                 |
| [Microsoft Learn – Build applications that authenticate users](https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/) | Microsoft Learn module                          |

