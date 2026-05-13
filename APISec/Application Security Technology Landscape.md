
Application security includes a wide range of technologies designed to protect software systems, such as:

- Static code analyzers  
- Dynamic testing tools  
- Software composition analysis (SCA)  
- Container security solutions  
- Web Application Firewalls (WAFs)  
- Web vulnerability scanners  

These tools are widely adopted and effective for traditional application risks. However, modern API-driven architectures introduce a **new class of threats** that these tools do not fully address.
# The API Security Gap

Despite mature AppSec tooling, API breaches continue to rise. This exposes a critical issue:

> Traditional security tools are not designed to detect most API-specific vulnerabilities.

## Why Traditional Tools Fall Short

Tools like:

- SAST (Static Application Security Testing)  
- DAST (Dynamic Application Security Testing)  

focus primarily on identifying **common, well-known vulnerabilities**, such as:

- SQL Injection  
- Cross-Site Scripting (XSS)  
- Known CVEs (Common Vulnerabilities and Exposures)  

However, API attacks rarely rely on these.

## Nature of API Vulnerabilities

API vulnerabilities are typically:

- **Logic-based** (business logic flaws)  
- **Authorization-related** (broken access control)  
- **Context-specific** (unique to the application’s design)  

These are:
- Harder to detect automatically  
- Often invisible to generic scanners  
- Highly dependent on how the API is implemented  

As a result, **standard security testing often misses critical API flaws**.

# The API Security Lifecycle

To effectively secure APIs, security must be integrated across the **entire application lifecycle**.

> The earlier security is introduced, the more effective and cost-efficient it becomes.

This is often referred to as **“shifting security left.”**
## 1. API Design Phase

This is the earliest and most critical stage.

At this stage, teams define:
- API structure  
- Endpoints  
- Data flows  
- Business logic  
### Key Security Considerations

- What data will the API expose?  
- Who should have access to it?  
- What are the potential abuse scenarios?  
- What controls are required?  

Security should be part of **design discussions**, not an afterthought.
## 2. Development Phase

During implementation, developers translate designs into code.
### Security Activities

- Code reviews  
- Static analysis (SAST)  
- Dependency analysis (SCA)  
### Most Effective Technique

**Manual code reviews** are especially valuable for API security because they can uncover:

- Logic flaws  
- Authorization gaps  
- Misuse of business rules  

Automated tools alone are insufficient at this stage.
## 3. Testing Phase

This is the final checkpoint before deployment.
### Testing Approaches

- Legacy DAST tools  
- Manual testing  
- External penetration testing  
- Automated API-specific security testing  
### Critical Objective

Identify and fix vulnerabilities **before production exposure**.

API-specific testing should simulate:
- Unauthorized access attempts  
- Abuse of business logic  
- Data extraction scenarios  
## 4. Runtime (Production) Phase

Once deployed, APIs must be actively monitored and protected.
### Runtime Controls

- Web Application Firewalls (WAFs)  
- API gateways  
- SIEM systems (Security Information and Event Management)  
### Role of Runtime Security

- Detect suspicious behavior  
- Block active attacks  
- Provide visibility into API usage  

However, runtime defenses are **reactive**, not preventive.
## 5. Decommissioning Phase

APIs that are no longer needed must be removed.
### Risks of Not Decommissioning

- Creation of **shadow or zombie APIs**  
- Exposure of outdated or vulnerable endpoints  
- Increased attack surface  

Proper lifecycle management ensures that obsolete APIs do not become hidden vulnerabilities.
# Mapping Risks to the Lifecycle

Effective API security involves aligning **identified risks** with **appropriate mitigation stages**.
### Example 1: Unknown (Shadow) APIs

**Mitigation Options:**
- Design phase:
  - Enforce API inventory policies  
  - Maintain centralized API catalogs  

- Runtime phase:
  - Use monitoring tools to discover undocumented APIs  
### Example 2: Unauthorized Access

**Mitigation Options:**
- Development phase:
  - Implement strict authorization checks  

- Testing phase:
  - Simulate cross-user access attempts  
  - Validate access control logic  
### Example 3: Data Harvesting

**Mitigation Options:**
- Design phase:
  - Limit exposed data fields  

- Testing phase:
  - Simulate bulk data extraction scenarios  

- Runtime phase:
  - Apply rate limiting and anomaly detection  
# Building a Security Strategy

After identifying risks through threat modelling, the next step is to:

1. **Prioritise risks** based on severity  
2. **Map each risk to lifecycle stages**  
3. **Assign mitigation strategies accordingly**  

> Address security issues as early as possible in the lifecycle.

Early-stage fixes:
- Reduce cost  
- Prevent downstream vulnerabilities  
- Improve overall system resilience  