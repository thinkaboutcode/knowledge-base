# OAuth 2.0 Flows Cheat Sheet

## 1. Authorization Code Flow (Most Secure)

| **Use Case** | Traditional web applications (server-side), where the client can securely store secrets |
|--------------|----------------------------------------------------------------------------------------|
| **Flow Steps** | 1. **User Authorization**: The user is redirected to the authorization server, where they log in and authorize the client. <br> 2. **Authorization Code**: Upon success, the server redirects the user back to the client with an authorization code. <br> 3. **Token Exchange**: The client sends the code (with client ID and secret) to the authorization server to exchange it for access and refresh tokens. <br> 4. **Resource Access**: The client uses the access token to access protected resources. |
| **Advantages** | - Secure as tokens are never exposed to the browser. <br> - Server-side only. |

## 2. Implicit Flow (Deprecated for Public Clients)

| **Use Case**  | Single-page applications (SPAs), mobile apps, or public clients that can’t securely store secrets (historically) |
|---------------|----------------------------------------------------------------------------------------------------------------|
| **Flow Steps** | 1. **User Authorization**: User is redirected to the authorization server, authenticates, and consents. <br> 2. **Access Token Returned**: The access token is returned directly in the redirect URI. <br> 3. **Resource Access**: The client uses the access token to access resources. |
| **Disadvantages** | - Access token is exposed in URLs and browser history. <br> - Prone to token interception. |

> **Note**: Implicit Flow is deprecated in favor of **PKCE** for SPAs due to security concerns.

## 3. Authorization Code Flow with PKCE (Recommended for SPAs & Mobile)

| **Use Case**  | Single-page applications (SPAs) and mobile apps where secrets can't be securely stored |
|---------------|--------------------------------------------------------------------------------------|
| **Flow Steps** | 1. **Code Challenge Generation**: Before redirecting, the client generates a random code challenge and stores the corresponding verifier. <br> 2. **User Authorization**: User is redirected to the authorization server to log in and authorize. <br> 3. **Authorization Code**: The server redirects the user back to the client with an authorization code. <br> 4. **Token Exchange**: The client sends the authorization code and the code verifier to the server to exchange for access/refresh tokens. <br> 5. **Resource Access**: The client uses the access token to access protected resources. |
| **Advantages** | - More secure than implicit flow. <br> - Does not require client secrets. |

## 4. Client Credentials Flow

| **Use Case**  | Machine-to-machine communication, where no user is involved (e.g., microservices, back-end APIs) |
|---------------|------------------------------------------------------------------------------------------------|
| **Flow Steps** | 1. **Client Authentication**: The client sends a POST request with its client ID and secret to the authorization server. <br> 2. **Access Token**: The authorization server issues an access token. <br> 3. **Resource Access**: The client uses the access token to access protected resources. |
| **Advantages** | Simple and direct for system-to-system communication. |
| **Disadvantages** | No user context (no delegation of rights from a user). |

## 5. Resource Owner Password Credentials Flow

| **Use Case**  | Trusted clients, typically used in legacy systems or highly trusted environments (not recommended for modern apps) |
|---------------|-------------------------------------------------------------------------------------------------------------------|
| **Flow Steps** | 1. **User Credentials**: The user provides their username and password directly to the client. <br> 2. **Access Token**: The client exchanges the credentials for an access token. <br> 3. **Resource Access**: The client uses the access token to access protected resources. |
| **Advantages** | Simple and easy to implement. |
| **Disadvantages** | Insecure as it requires exposing user credentials to the client. |

## 6. Device Authorization Flow (Device Flow)

| **Use Case**  | Devices with limited input capabilities (e.g., smart TVs, IoT devices) |
|---------------|----------------------------------------------------------------------|
| **Flow Steps** | 1. **Device Code Request**: The client requests a device code and user code from the authorization server. <br> 2. **User Authorization**: The user visits a URL on another device and enters the user code to authorize the client. <br> 3. **Polling for Authorization**: The client polls the authorization server to check if the user has completed authorization. <br> 4. **Access Token**: Once the user authorizes, the client receives an access token. <br> 5. **Resource Access**: The client uses the access token to access protected resources. |
| **Advantages** | Allows authorization on devices with limited input. |
| **Disadvantages** | Requires continuous polling to check for authorization completion. |

---

## Token Types

| **Token Type** | **Description** |
|----------------|-----------------|
| **Access Token** | Short-lived token used to access protected resources. |
| **Refresh Token** | Long-lived token used to obtain new access tokens without requiring user re-authentication. |

---

## Key Concepts

| **Term**             | **Description**                                                                 |
|----------------------|---------------------------------------------------------------------------------|
| **Client ID/Secret**  | Identifies the client application.                                              |
| **Redirect URI**      | The URI where the authorization server redirects the user after authorization.  |
| **Scopes**            | Define the access privileges (e.g., read, write).                               |
| **Consent Screen**    | Where the user grants permission for the requested scopes.                      |

---

## Security Recommendations

- Use **Authorization Code with PKCE** for public clients (SPAs and mobile apps).
- Avoid using **Resource Owner Password Credentials Flow** due to security risks.
- Secure tokens in transit using **HTTPS**.
- Implement **refresh token rotation** to minimize risk if a refresh token is compromised.
- Store tokens securely in client storage (e.g., use HTTP-only cookies for web apps).

---
