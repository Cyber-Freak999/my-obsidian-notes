 # The Problem
![[Pasted image 20241118201010.png]]
# OAuth Actors
- Resource Owner
- Client
- Resource Server
- Authorization Server

RO makes content in RS, wants to use  3rd party app to access content. Client needs to be delegated access to RS on RO behalf. AS is the one that delegates access to client.

# Authorization vs Delegation
OAuth  is not an open authorization protocol but rather a delegation protocol.

---

This distinction often causes confusion since OAuth grants limited access to third-party applications on behalf of a user, which resembles authorization but with important nuances. Let’s break down why OAuth is about delegation:

1. **Delegation of Access Rights**: OAuth allows users to grant third-party applications limited access to their resources without sharing passwords or giving full control. It delegates specific permissions (such as reading or writing data) rather than giving the app comprehensive access. This avoids giving the application direct "authorization" to act as the user in all capacities; instead, it can only perform specific actions designated by the user.
    
2. **Resource Ownership vs. Access Control**: In OAuth, the _resource owner_ (typically the user) delegates access to a _client application_ by interacting with the _authorization server_, which issues access tokens with defined scopes and limitations. This approach means that OAuth is less about confirming whether the application _has authority_ and more about whether the user permits it to access certain resources.
    
3. **Bounded Control**: By delegating through OAuth, users set explicit limits on what an application can do, often restricted by time and scope (like only allowing access to read emails, without permissions to send them). These boundaries reinforce that OAuth is a system of delegation where the application acts on behalf of the user within controlled limits.
    

In essence, OAuth is not about granting unrestricted access or authorization in the traditional sense. Instead, it’s a structured method of _delegating_ specific rights, maintaining a clear boundary between the user’s authority and the permissions given to the application.

