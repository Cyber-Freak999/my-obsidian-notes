## ❗ What Is Error Disclosure?

- When APIs return **too much internal information** (stack traces, framework names, DB errors, etc.) to the user.    
- Helps attackers **enumerate users**, identify your **tech stack**, or map **attack surfaces**.
- Commonly seen in:
    - API responses
    - Console logs
    - Browser dev tools
    - Unhandled exceptions

## 🧠 Why It's Dangerous

- Exposing info like `"Spring Framework Error"` lets attackers search for related CVEs.    
![[Pasted image 20250629221459.png]]
- Reveals:
    - **Programming language**
    - **Database type**
    - **Framework versions**
    - **Stack traces / internal structure**

## ✅ Best Practices
[Error Handling Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/Error_Handling_Cheat_Sheet.html)

| DO ✅                                                            | DON'T ❌                                     |
| --------------------------------------------------------------- | ------------------------------------------- |
| Return **generic error messages** like `"Something went wrong"` | Return stack traces or error dumps to users |
| **Log** detailed errors server-side for dev/debug               | Expose sensitive debug output publicly      |
| Use error codes or IDs for internal mapping                     | Say if a user/email/resource exists         |
| **Fail fast** and early on bad input                            | Let deep layers process malicious input     |
| Catch and handle exceptions properly                            | Leave unhandled errors that bubble up       |


## 🛠️ Examples

### ❌ Bad (Discloses stack & tech info):

```json
{
  "error": "SQLSyntaxErrorException: syntax error at or near 'SELECT' in Spring JDBC"
}
```

#### ✅ Good (Generic, safe):

```json
{
  "error": "An unexpected error occurred. Please contact support."
}
```

### 🕵️ Real-World Tip

- **GitHub returns 404 for both non-existent and unauthorized pages.**  
    → Prevents resource enumeration (you can’t tell if a repo exists unless you're allowed to access it).
![[Pasted image 20250629054230.png]]   

## 🚫 Common Pitfalls

- Logging errors in the **response** instead of **server logs**.    
- Using `try/catch` to return `err.toString()` or `res.send(err)`. 
- Overly detailed form validation errors revealing valid/invalid users.

## 🔒 Security Mindset

> Always assume your error messages will be **read by attackers**, not just users.

Make your errors:
- **Helpful to devs (internally)**
- **Useless to attackers (externally)**

---
## Q/A
### **Q1: What strategies can help link internal error logs to external generic messages for debugging?**

To ensure developers can debug without exposing sensitive error data to users, you can **tie external generic errors to internal logs** using traceable identifiers.

#### ✅ Recommended Strategies:

- **Use Correlation IDs or Error IDs**
    - Generate a unique ID for every request (e.g., UUID).
    - Include this ID in both the internal log and the user-facing error response:
    ```json
    {
          "error": "An unexpected error occurred.",
          "error_id": "a6f3-223b"
    }
	```
- **Centralized Logging**
    - Log full error context (stack trace, request metadata) server-side.        
    - Tools: ELK stack, Datadog, Sentry, Logstash, etc.
- **Context-Aware Logging Middleware**
    - Automatically capture context like user ID, endpoint, request body, and error cause.
- **Map Custom Error Codes**
    - Define a catalog of error codes (e.g., `E101: Auth failed`, `E203: DB timeout`) and map those to log entries and user responses.        

### **Q2: How can API gateways or WAFs be configured to sanitize unhandled exceptions automatically?**

API gateways and Web Application Firewalls (WAFs) can **intercept and normalize** responses that would otherwise disclose sensitive info.

#### ✅ Controls to Apply:

- **Custom Error Handling Middleware**
    - Gateways like Kong, Tyk, or Express Gateways can strip or rewrite error responses.
- **Set Safe Default Response Templates**
    - Configure gateway to respond with this for 500 or unclassified errors.:
```json
{
"error": "Service temporarily unavailable"
}
```         
- **Pattern-Based Sanitization**
    - Detect sensitive keywords in responses (`Spring`, `SQL`, `Exception`, etc.) and replace with generic messages.

- **Use WAF Rule Sets**    
    - Configure ModSecurity or AWS WAF rules to:
        - Block stack traces
        - Detect and filter common tech signatures
- **Force HTTP Status Code Overwrites**
    - Rewrite certain error codes to safer equivalents (e.g., 404 instead of 403/401).

### **Q3: In what ways can error messages be abused for user enumeration in login or forgot-password flows?**

Attackers can exploit **differentiated error messages** to determine if a user exists or not, which helps build **username/email lists** for further attacks.

 🛑 Vulnerable Patterns:
- Login:
    - `"User does not exist"` → tells attacker the username is invalid.
    - `"Incorrect password"` → confirms user **does exist**.
- Password Reset:
    - `"A reset link was sent to your email"` vs `"Email not found"` → same issue.

 ✅ Safe Alternatives:
- Always return **generic messages**, e.g.:
    - `"If your account exists, a reset link has been sent."`
    - `"Login failed. Please check your credentials."`
- Rate limit and monitor repeated login/forgot-password attempts from same IP/device.
- Log failed attempts for behavioral analytics or alerting.
