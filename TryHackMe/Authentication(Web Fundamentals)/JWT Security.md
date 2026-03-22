---
tags:
  - concept
  - web-app
  - auth
  - crypto
link: https://tryhackme.com/room/jwtsecurity
---
# Token-Based Authentication
## The Rise of APIs
Application Programming Interfaces, or APIs for short, have become incredibly popular today. One of the key reasons for this boom is the ability to create a single API that can then serve several different interfaces, such as a web application and mobile application, at the same time. This allows the same server-side logic to be centralised and reused for all interfaces. From a security perspective, this is also usually beneficial as it means we can implement the server-side security in a single API that would then protect our server regardless of the interface that is being used.

However, new session management methods were also created with the rise of APIs. As cookies are usually associated with web applications used through a browser, cookie-based authentication for APIs usually doesn't work as well since the solution is then not agnostic for other interfaces. This is where token-based session management comes in to save the day.  
## Token-Based Session Management
Token-based session management is a relatively new concept. Instead of using the browser's automatic cookie management features, it relies on client-side code for the process. After authentication, the web application provides a token within the request body. Using client-side JavaScript code, this token is then stored in the browser's LocalStorage.

When a new request is made, JavaScript code must load the token from storage and attach it as a header. One of the most common types of tokens is JSON Web Tokens (JWT), which are passed through the `Authorization: Bearer` header. However, as we are not using the browser's built-in cookie management features, it is a bit of the wild west where anything goes. Although there are standards, nothing is forcing anything from sticking to these standards. Tokens like JWTs are a way to standardise token-based session management.
# JSON Web Tokens
JWTs are self-contained tokens that can be used to securely transmit session information. It is an [open standard](https://tools.ietf.org/html/rfc7519), providing information for any developer or library creator who wants to use JWTs.
## JWT Structure
A JWT consists of three components, each Base64Url encoded and separated by dots:
- **Header** - The header usually indicates the type of token, which is JWT, as well as the signing algorithm that is used.
- **Payload** - The payload is the body of the token, which contain the claims. A claim is a piece of information provided for a specific entity. In JWTs, there are registered claims, which are claims predefined by the JWT standard and public or private claims. The public and private claims are those which are defined by the developer. It is worth knowing the difference between public and private claims, but not for security purposes, hence this will not be our focus in this room.
- **Signature** - The signature is the part of the token that provides a method for verifying the token's authenticity. The signature is created by using the algorithm specified in the header of the JWT. Let's dive a bit into the main signing algorithms.
## Signing Algorithms
Although there are several different algorithms defined in the JWT standard, we only really care about three main ones:
- **None** - The None algorithm means no algorithm is used for the signature. Effectively, this is a JWT without a signature, meaning that the verification of the claims provided in the JWT cannot be verified through the signature.
- **Symmetric Signing** - A symmetric signing algorithm, such as HS256, creates the signature by appending a secret value to the header and body of the JWT before generating a hash value. Verification of the signature can be performed by any system that has knowledge of the secret key.
- **Asymmetric Signing** - An asymmetric signing algorithm, such as RS256, creates the signature by using a private key to sign the header and body of the JWT. This is created by generating the hash and then encrypting the hash using the private key. Verification of the signature can be performed by any system that has knowledge of the public key associated with the private key that was used to create the signature.
## Security in the Signature
JWTs can be encrypted (called JWEs), but the key power of JWTs comes from the signature. Once a JWT is signed, it can be sent to the client, who can use this JWT wherever needed. We can have a centralised authentication server that creates the JWTs used on several applications. Each application can then verify the signature of the JWT; if verified, the claims provided within the JWT can be trusted and acted upon.
# Sensitive Information Disclosure
The first common issue we will dive into is the exposure of sensitive information within the JWT.

A common cookie-based session management approach is using the server-side session to store several parameters. In PHP, for example, you can use `$SESSION['var']=data` to store a value associated with the user's session. These values are not exposed client-side and can therefore only be recovered server-side. However, with tokens, the claims are exposed as the entire JWT is sent client-side. If the same development practice is followed, sensitive information can be disclosed. Some examples are seen on real applications:

- Credential disclosure with the password hash, or even worse, the clear-text password being sent as a claim.
- Exposure of internal network information such as the private IP or hostname of the authentication server.
# Signature Validation Mistake
The second common mistake with JWTs is not correctly verifying the signature. If the signature isn't correctly verified, a threat actor may be able to forge a valid JWT token to gain access to another user's account. Let's examine the common signature verification issues.
## Not Verifying the Signature
The first issue with signature validation is when there is no signature validation. If the server does not verify the signature of the JWT, then it is possible to modify the claims in the JWT to whatever you prefer them to be. While it is uncommon to find APIs where no signature validation is performed, signature validation may have been omitted from a single endpoint within the API. Depending on the sensitivity of the endpoint, this can have a significant business impact.