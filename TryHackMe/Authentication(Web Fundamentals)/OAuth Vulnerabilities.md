---
tags:
  - web-app
  - concept
  - auth
link: https://tryhackme.com/room/oauthvulnerabilities
---
# Key Concepts
## Resource Owner
The resource owner is the **person** or **system** that controls certain data and can authorize an application to access that data on their behalf. This concept is fundamental as it centres around user consent and control. For example, you are the resource owner as a coffee shop customer. You can control your account information and grant the coffee shop's mobile app permission to access your data.  
## Client  
The client can be a **mobile app** or a **server-side web application**. It acts as an intermediary, requesting access to resources and performing actions as permitted by the resource owner. For example, the coffee shop's web app, which you use to order and pay for coffee, is the client. Your authorization is needed to access your account details and payment information.
## Authorization Server
The authorization server is responsible for **issuing access tokens to the client** after successfully authenticating the resource owner and obtaining their authorization. The authorization server plays a crucial role in the OAuth process by ensuring the client is granted permission only after legitimate user authentication and consent. For example, the coffee shop's backend system that handles authentication and authorization is the authorization server. It verifies your credentials and grants the web app permission to access your account.  
## Resource Server
The server hosting the protected resources can **accept and respond** **to protected resource requests** using access tokens. This server ensures that only authenticated and authorized clients can access or manipulate the resource owner's data. For example, the resource server is the coffee shop's database that stores your account information, order history, and payment details. It responds to requests from the web app, allowing it to retrieve and modify your data.
## Authorization Grant
The client uses a credential representing the resource owner's authorization (to access their protected resources) to obtain an access token. The primary grant types are `Authorization Code`, `Implicit`, `Resource Owner Password Credentials`, and `Client Credentials`. For example, when you first log in to the coffee shop's app, you are given an authorization grant (like entering your username and password). The app uses this grant to get an access token from the authorization server. We will discuss it in detail in the next task.
## Access Token
A credential that the client can use to access protected resources on behalf of the resource owner. It has a limited lifespan and scope. Access tokens are essential for maintaining secure and protected communication between the client and resource server without repeatedly asking the resource owner for credentials. For example, once you log in to the coffee shop's app, it receives an access token, which allows the app to access your account to place orders and make payments without asking you to log in again for a specific period. 
## Refresh Token
A credential that the client can use to obtain a new access token without requiring the resource owner to re-authenticate. Refresh tokens are typically long-lived and provide a way to maintain user sessions without frequent login interruptions. For example, when your access token expires, the web app will use a refresh token to get a new access token, so you don’t have to log in again.
## Redirect URI
The URI to which the authorization server will redirect the resource owner’s user-agent after the grant or denial of the authorization. It checks if the client for which the authorization response has been requested is correct. For instance, after interacting with the coffee shop app and logging in, you will be redirected to the authorization server by the app page in the coffee shop’s app, commonly known as the redirect URI, to confirm that you successfully logged in.
## Scope
Scopes are a mechanism for limiting an application's access to a user's account. They allow the client to specify the level of access needed and the authorization server to inform the user what access levels the application is requesting. Scopes help enforce the `principle of least privilege`. For example, the coffee shop's app may request different scopes, such as access to your order history and payment details. As the resource owner, you can see what information the app requests access to and grant or deny permissions.  
## State Parameter
An **optional** parameter maintains the state between the client and the authorization server. It can help prevent CSRF attacks by ensuring the response matches the client's request. The state parameter is a crucial part of securing the OAuth flow. For example, when you initiate the login process, the coffee shop's app sends a state parameter to the authorization server. This parameter helps ensure that the response you receive is linked to your original request, protecting against certain types of attacks.
## Token & Authorization Endpoint
The authorization server's endpoint is where the client exchanges the authorization grant (or refresh token) for an access token. In contrast, the authorization endpoint is where the resource owner is authenticated and authorizes the client to access the protected resources.
# OAuth Grant Types
OAuth 2.0 provides several grant types to accommodate various scenarios and client types. These grant types define how an application can obtain an access token to access protected resources on behalf of the resource owner. In this task, we will discuss four primary OAuth 2.0 grant types.  
## Authorization Code Grant  
The Authorization Code grant is the most commonly used OAuth 2.0 flow suited for server-side applications (PHP, JAVA, .NET etc). In this flow, the **client redirects the user to the authorization server, where the user authenticates and grants authorization**. The authorization server then redirects the user to the client with an **authorization code**. The client exchanges the authorization code for an access token by requesting the authorization server's token endpoint.
![](Authorisation%20Code%20Grant.png)
This grant type is known for its enhanced security, as the authorization code is exchanged for an access token server-to-server, meaning the access token is not exposed to the user agent (e.g., browser), thus reducing the risk of token leakage. It also supports using refresh tokens to maintain long-term access without repeated user authentication.
## Implicit Grant
The Implicit grant is primarily designed for mobile and web applications where clients cannot securely store secrets. It **directly issues the access token to the client without requiring an authorization code exchange**. In this flow, the client redirects the user to the authorization server. After the user authenticates and grants authorization, the authorization server returns an access **token in the URL fragment**.
![](Implicit%20Grant.png)
This grant type is simplified and suitable for clients who cannot securely store client secrets. It is faster as it involves fewer steps than the authorization code grant. However, it is less secure as the access token is exposed to the user agent and can be logged in the browser history. It also **does not support refresh tokens**.   
## Resource Owner Password Credentials Grant  
The Resource Owner Password Credentials grant is used when the client is **highly trusted by the resource owner**, such as first-party applications. The client collects the user’s credentials (username and password) directly and exchanges them for an access token, as shown below:
![](Resource%20Owner%20Passowrd%20Grant.png)
In this flow, the user provides their credentials directly to the client. The client then sends the credentials to the authorization server, which verifies the credentials and issues an access token. This grant type is direct, requiring fewer interactions, making it suitable for highly trusted applications where the user is confident in providing their credentials. However, it is less secure because it involves sharing credentials directly with the client and is unsuitable for third-party applications.
## Client Credentials Grant  
The Client Credentials grant is used for server-to-server interactions without user involvement. The client uses his credentials to authenticate with the authorization server and obtain an access token. In this flow, the client authenticates with the authorization server using its client credentials (client ID and secret), and the authorization server issues an access token directly to the client, as shown below:
![](Client%20Credentials%20Grant.png)
This grant type is suitable for backend services and server-to-server communication as it does not involve user credentials, thus reducing security risks related to user data exposure.
# How OAuth Works
The OAuth 2.0 flow begins when a user (Resource Owner) interacts with a client application (Client) and requests access to a specific resource. The client redirects the user to an authorization server, where the user is prompted to log in and grant access. If the user consents, the authorization server issues an authorization code, which the client can exchange for an access token. This access token allows the client to access the resource server and retrieve the requested resource on behalf of the user.
# Identifying OAuth Usage in an Application
The first indication that an application uses OAuth is often found in the login process. Look for options allowing users to log in using external service providers like Google, Facebook, and GitHub. These options typically redirect users to the service provider's authorization page, which strongly signals that OAuth is in use.
## Detecting OAuth Implementation
When analyzing the network traffic during the login process, pay attention to HTTP redirects. OAuth implementations will generally redirect the browser to an authorization server's URL. This URL often contains specific query parameters, such as `response_type`, `client_id`, `redirect_uri`, `scope`, and `state`. These parameters are indicative of an OAuth flow in progress. For example, a URL might look like this:  

`https://dev.coffee.thm/authorize?response_type=code&client_id=AppClientID&redirect_uri=https://dev.coffee.thm/callback&scope=profile&state=xyzSecure123`

## Identifying the OAuth Framework
Once you have confirmed that OAuth is being used, the next step is to identify the specific framework or library the application employs. This can provide insights into potential vulnerabilities and the appropriate security assessments. Here are some strategies to identify the OAuth framework:

- **HTTP Headers and Responses**: Inspect HTTP headers and response bodies for unique identifiers or comments referencing specific OAuth libraries or frameworks.
- **Source Code Analysis**: If you can access the application's source code, search for specific keywords and import statements that can reveal the framework in use. For instance, libraries like `django-oauth-toolkit`, `oauthlib`, `spring-security-oauth`, or `passport` in `Node.js`, each have unique characteristics and naming conventions.
- **Authorization and Token Endpoints**: Analyze the endpoints used to obtain authorization codes and access tokens. Different OAuth implementations might have unique endpoint patterns or structures. For example, the `Django OAuth Toolkit` typically follows the pattern `/oauth/authorize/` and `/oauth/token/`, while other frameworks might use different paths.
- **Error Messages**: Custom error messages and debug output can inadvertently reveal the underlying technology stack. Detailed error messages might include references to specific OAuth libraries or frameworks.
# Exploiting OAuth - Stealing OAuth Token
Tokens play a critical role in the OAuth 2.0 framework, acting as digital keys that grant access to protected resources. These tokens are issued by the authorization server and redirected to the client application based on the `redirect_uri` parameter. This redirection is crucial in the OAuth flow, ensuring that tokens are securely transmitted to the intended recipient. However, if the `redirect_uri` is not well protected, attackers can exploit it to hijack tokens.
## Role of Redirect_URI
The `redirect_uri` parameter is specified during the OAuth flow to direct where the authorization server should send the token after authorization. This URI must be pre-registered in the application settings to prevent open redirect vulnerabilities. During the OAuth process, the server checks that the provided `redirect_uri` matches one of the registered URIs.
## Vulnerability
An insecure `redirect_uri` can lead to severe security issues. If attackers gain control over any domain or URI listed in the `redirect_uri`, they can manipulate the flow to intercept tokens. Here’s how this can be exploited:

- Consider an OAuth application with registered redirect URIs: `http://coffee.thm:8000/oauthdemo/oauth_login/` `http://dev.bistro.thm:8002/malicious_redirect.html`
- **Attacker's Strategy**: If an attacker gains control over `dev.bistro.thm`, they can exploit the OAuth flow. By setting the `redirect_uri` to `http://dev.bistro.thm/callback`, the authorization server will send the token to this controlled domain.
- **Crafted Attack:** The attacker initiates an OAuth flow and ensures the `redirect_uri` points to their controlled domain. After the user authorizes the application, the token is sent to `http://dev.bistro.thm/callback`. The attacker can now capture this token and use it to access protected resources.
# Exploiting OAuth - CSRF in OAuth
The **state** parameter in the OAuth 2.0 framework protects against [CSRF](CSRF.md) attacks, which occur when an attacker tricks a user into executing unwanted actions on a web application where they are currently authenticated. In the context of OAuth, CSRF attacks can lead to unauthorized access to sensitive resources by hijacking the OAuth flow. The state parameter helps mitigate this risk by maintaining the integrity of the authorization process.  
## Vulnerability of Weak or Missing State Parameter
The state parameter is an arbitrary string that the client application includes in the authorization request. When the authorization server redirects the user back to the client application with the authorization code, it also includes the state parameter. The client application then verifies that the state parameter in the response matches the one it initially sent. This validation ensures that the response is not a result of a CSRF attack but a legitimate continuation of the OAuth flow.  

For instance, consider an OAuth implementation where the state parameter is either **missing** or **predictable** (e.g., a static value like "state" or a simple sequential number). An attacker can initiate an OAuth flow and provide their malicious redirect URI. After the user authenticates and authorizes the application, the authorization server redirects the authorization code to the attacker's controlled URI, as specified by the weak or absent state parameter.
# Exploiting OAuth - Implicit Grant Flow
In the implicit grant flow, tokens are directly returned to the client via the browser without requiring an intermediary authorization code. This flow is primarily used by single-page applications and is designed for public clients who cannot securely store client secrets. However, this flow has inherent vulnerabilities:
## Weaknesses
- **Exposing Access Token in URL**: The application redirects the user to the OAuth authorization endpoint, which returns the access token in the URL fragment. Any script running on the page can easily access this fragment.
- **Inadequate Validation of Redirect URIs**: The OAuth server does not adequately validate the redirect URIs, allowing potential attackers to manipulate the redirection endpoint.
- **No HTTPS Implementation**: The application does not enforce HTTPS, which can lead to token interception through man-in-the-middle attacks.
- **Improper Handling of Access Tokens**: The application stores the access token insecurely, possibly in `localStorage` or `sessionStorage`, making it vulnerable to XSS attacks.
## Deprecation of Implicit Grant Flow
Due to these vulnerabilities, the [OAuth 2.0 Security Best Current Practice](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-security-topics) recommends deprecating the implicit grant flow in favour of the authorization code flow with [Proof Key for Code Exchange](https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow-with-pkce) (PKCE). This updated flow provides enhanced security by mitigating the risks of token exposure and lack of client authentication.
# Other Vulnerabilities and Evolution of OAuth 2.1

﻿Apart from the vulnerabilities discussed earlier, attackers can exploit several other critical weaknesses in OAuth 2.0 implementations. The following are some additional vulnerabilities that pentesters should be aware of while pentesting an application.

Insufficient Token Expiry

Access tokens with long or infinite lifetimes pose a significant security risk. If an attacker obtains such a token, they can access protected resources indefinitely. Implementing short-lived access and refresh tokens helps mitigate this risk by limiting the window of opportunity for attackers.

Replay Attacks  

Replay attacks involve capturing valid tokens and reusing them to gain unauthorized access. Attackers can exploit tokens multiple times without mechanisms to detect and prevent token reuse. Implementing `nonce` values and `timestamp` checks can help mitigate replay attacks by ensuring each token is used only once.

Insecure Storage of Tokens

Storing access tokens and refresh tokens insecurely (e.g., in local storage or unencrypted files) can lead to token theft and unauthorized access. Using secure storage mechanisms, such as secure cookies or encrypted databases, can protect tokens from being accessed by malicious actors.

Evolution of OAuth 2.1

OAuth 2.1 represents the latest iteration in the evolution of the OAuth standard, building on the foundation of OAuth 2.0 to address its shortcomings and enhance security. The journey from OAuth 2.0 to OAuth 2.1 has been driven by the need to mitigate known vulnerabilities and incorporate best practices that have emerged since the original specification was published. OAuth 2.0, while widely adopted, had several areas that required improvement, particularly in terms of security and interoperability. ![a rocket with Oauth 2.1 showing evolution of OAuth framework](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1724169664413.png)

**Major Changes**

OAuth 2.1 introduces several key changes aimed at strengthening the protocol.

- One of the most significant updates is the deprecation of the `implicit grant type`, which was identified as a major security risk due to token exposure in URL fragments. Instead, OAuth 2.1 recommends the authorization code flow with PKCE for public clients.
- Additionally, OAuth 2.1 mandates using the `state` parameter to protect against CSRF attacks. 
- OAuth 2.1 also emphasizes the importance of `secure handling and storage of tokens`. It advises against storing tokens in browser local storage due to the risk of XSS attacks and recommends using secure cookies instead.
- Moreover, OAuth 2.1 enhances interoperability by providing clearer guidelines for `redirect URI validation`, client authentication, and scope validation. 

In summary, OAuth 2.1 builds on OAuth 2.0 by addressing its security gaps and incorporating best practices to offer a more secure and protected authorization framework. For more detailed information on OAuth 2.1, you can refer to the official specification [here(opens in new tab)](https://oauth.net/2.1/).