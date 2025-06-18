OAuth defines different **flows (grants)** for how clients obtain tokens to access APIs. The right flow depends on the **application type** and **whether there's a user involved**.

---

**1. Authorization Code Flow (with PKCE)**

- **Best for:** Web apps and mobile apps **with user interaction**.
- **Actors involved:** Resource owner (user), client, resource server, and authorization server.
- **Steps:**
    - User is redirected to the `/authorize` endpoint (front-channel).
    - They authenticate (login process is out of scope for OAuth).
    - Authorization server redirects back with a **code** and **state**.
    - Client uses the **code** and a **code verifier** (PKCE) to POST to `/token` endpoint (back-channel).
    - If valid, client receives an **access token** (short-lived) and **refresh token** (longer-lived).
- **Use PKCE** for security to bind request/response.

---

 **2. Refresh Token Flow**
- **Purpose:** Obtain a new access token **without user re-authentication**.
- **Steps:**
    - POST to `/token` endpoint with `grant_type=refresh_token`, client credentials, and refresh token.
    - If valid, a new access token (and optionally a new refresh token) is returned.
- **Refresh token TTL** varies (from hours to years).

---

### **3. Client Credentials Flow**

- **Best for:** **Machine-to-machine** communication where no user is involved (e.g. cron jobs, microservices).
- **Steps:**
    - POST to `/token` with `grant_type=client_credentials`, client ID/secret, and requested scopes.
    - Get an access token.
- **No refresh token** is issued. Just repeat the request when needed.

---

### **Key Takeaways**
- OAuth flows are  client interaction patterns.
- **Use Authorization Code Flow** for apps with user logins; this make it the most commonly used.
- **Use Refresh Flow** to avoid frequent re-logins.
- **Use Client Credentials Flow** for backend-only systems.
- **Pick the flow that matches your application type and required security level.**