# Tokens

> [!NOTE]
> This document is part of the Microsoft Entra ID section of my Azure Infrastructure Roadmap while preparing for the Microsoft AZ-104 certification.
> It explains the security tokens issued by Microsoft Entra ID and their role in authentication and authorization.

---

## Token Flow

```text
          Application
                │
                ▼
      Microsoft Entra ID
                │
      Authentication
                │
                ▼
         Security Tokens
      ┌─────────┼─────────┐
      ▼         ▼         ▼
 ID Token  Access Token  Refresh Token
      │         │         │
      ▼         ▼         ▼
 Application   API    New Access Token
```

---

> [!TIP]
> **Key Concepts**
>
> * Tokens are issued after successful authentication.
> * Tokens prove identity and authorization.
> * Microsoft Entra ID issues different token types for different purposes.
> * APIs validate tokens before granting access.
> * Tokens have limited lifetimes.

---

## Overview

Microsoft Entra ID issues security tokens after successfully authenticating users or applications.

These tokens allow applications to verify identity and securely access protected resources without repeatedly sending credentials.

Each token type serves a different purpose during the authentication process.

---

## Why Tokens Exist

Without tokens, applications would need to send usernames, passwords, or other credentials with every request.

Instead, Microsoft Entra ID authenticates the identity once and issues signed security tokens.

Applications and APIs trust these tokens instead of storing or repeatedly validating user credentials.

---

## Token Types

Microsoft Entra ID commonly issues three token types.

| Token         | Purpose                                                                      |
| ------------- | ---------------------------------------------------------------------------- |
| ID Token      | Identifies the authenticated user to the application.                        |
| Access Token  | Authorizes access to protected APIs and resources.                           |
| Refresh Token | Requests new Access Tokens without requiring the user to authenticate again. |

---

## ID Token

An ID Token contains information about the authenticated user.

It is intended for the client application and confirms that authentication was successful.

Applications commonly use ID Tokens to establish user sessions.

---

## Access Token

Access Tokens are presented to APIs when requesting protected resources.

The target API validates the token before authorizing the request.

Access Tokens contain claims describing the authenticated identity and the permissions granted.

Microsoft Entra ID typically issues Access Tokens with a default lifetime of approximately one hour.

---

## Refresh Token

Refresh Tokens allow applications to request new Access Tokens without requiring the user to sign in again.

This improves user experience while maintaining security.

Refresh Tokens are never sent to protected APIs; they are only presented to Microsoft Entra ID.

---

## Token Validation

Protected resources validate several aspects of every Access Token before granting access.

Typical validation includes:

* Digital signature
* Token expiration
* Issuer
* Audience
* Required permissions
* Tenant policies

Only valid tokens are accepted.

---

## Token Signature Validation

Protected APIs do not contact Microsoft Entra ID every time they receive an Access Token.

Instead, Microsoft Entra ID publishes its public signing keys through its OpenID Connect metadata endpoint.

Applications and APIs download and periodically refresh these public keys to validate JWT signatures locally.

This allows token validation to be performed efficiently without requiring a network request for every API call.

---

## Continuous Access Evaluation (CAE)

Some Microsoft services support **Continuous Access Evaluation (CAE)**.

With CAE, compatible services can respond immediately to critical security events instead of waiting for the Access Token to expire.

Examples include:

- User account disabled.
- Password changed or reset.
- High-risk user detected.
- Conditional Access policy changes.

This improves security by reducing the time during which previously issued tokens remain usable after significant identity changes.

---

## Token Claims

Tokens contain claims that describe the authenticated identity.

Common claims include:

| Claim   | Description                              |
| ------- | ---------------------------------------- |
| `iss`   | Token issuer.                            |
| `aud`   | Intended audience.                       |
| `sub`   | Subject identifier.                      |
| `exp`   | Expiration time.                         |
| `iat`   | Issued-at time.                          |
| `tid`   | Microsoft Entra ID tenant identifier.    |
| `oid`   | Object ID of the authenticated identity. |
| `scp`   | Delegated permissions (Scopes).          |
| `roles` | Application permissions or App Roles.    |

Applications and APIs use these claims during authorization.

---

## JSON Web Tokens (JWT)

Microsoft Entra ID issues ID Tokens and Access Tokens as JSON Web Tokens (JWTs).

A JWT consists of three Base64URL-encoded sections:

| Section | Purpose |
|----------|---------|
| Header | Identifies the token type and signing algorithm (typically RS256). |
| Payload | Contains claims describing the authenticated identity and granted permissions. |
| Signature | Cryptographically protects the token against tampering using Microsoft Entra ID's signing key. |

Applications can decode JWTs for inspection, but only trusted resources should validate and rely on their contents.

---

## Token Lifetime

Tokens are intentionally short-lived to reduce security risks.

* Access Tokens typically expire after about one hour.
* Refresh Tokens can obtain new Access Tokens without requiring interactive sign-in.
* Expired Access Tokens cannot be reused.

Applications should never assume that an Access Token is valid indefinitely.

---

## Enterprise Scenario

A user signs in to an internal web application.

Microsoft Entra ID authenticates the user and issues an ID Token and an Access Token.

The application uses the ID Token to establish the user session and presents the Access Token when calling Microsoft Graph.

Microsoft Graph validates the token before returning the requested information.

---

## Best Practices

* Always validate Access Tokens.
* Use the principle of least privilege.
* Never store tokens in source code.
* Protect Refresh Tokens carefully.
* Use HTTPS for all token exchanges.
* Allow applications to request new Access Tokens instead of extending token lifetimes.

---

## Common Pitfalls

* Confusing ID Tokens with Access Tokens.
* Sending Refresh Tokens to APIs.
* Assuming decoded JWTs are automatically trustworthy.
* Ignoring token expiration.
* Storing tokens insecurely.

---

> [!IMPORTANT]
> **AZ-104 Focus**
>
> You should understand:
>
> * ID Tokens
> * Access Tokens
> * Refresh Tokens
> * JWT structure
> * Token claims
> * Token validation
> * Token lifetime

---

## Key Takeaways

* Microsoft Entra ID issues security tokens after successful authentication.
* Different token types serve different purposes.
* APIs validate Access Tokens before granting access.
* JWTs contain claims describing the authenticated identity.
* Tokens reduce the need to repeatedly send credentials.
* Short-lived tokens improve security.

---

## References

| Microsoft Documentation                                                                                                         | Purpose                            |
| ------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| [Security tokens](https://learn.microsoft.com/entra/identity-platform/security-tokens)                                          | Microsoft identity platform tokens |
| [Access tokens](https://learn.microsoft.com/entra/identity-platform/access-tokens)                                              | Access Token overview              |
| [ID tokens](https://learn.microsoft.com/entra/identity-platform/id-tokens)                                                      | ID Token overview                  |
| [JSON Web Tokens (JWT)](https://learn.microsoft.com/entra/identity-platform/access-tokens#validate-tokens)                      | Token validation                   |
| [Microsoft Learn – Authentication and tokens](https://learn.microsoft.com/training/modules/build-app-that-authenticates-users/) | Microsoft Learn module             |

