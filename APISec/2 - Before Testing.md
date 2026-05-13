# Pre-API Pentest Checklist Summary

## Client Discovery Questions (Before Testing Starts)

1. **What’s the API architecture?**  
    REST is most common, but it might be SOAP, GraphQL, RPC, or use Webhooks — this impacts how tests are structured.
2. **What type of test are we doing?**
    - **Whitebox**: Full access (source code, configs).
    - **Blackbox**: External testing with no internal knowledge.
    - **Greybox**: Limited internal context (e.g., user credentials).
3. **Which environment will be tested?**
    - **Production**: Real users, higher risk.
    - **Pre-production / QA**: Safer for active testing.
4. **How is authentication handled?**
    This defines how to test login flows or bypasses. e.g. Basic Auth, OAuth 2.0, API keys, or none. 
5. **What roles exist?**  
    Admins, regular users, guests — you’ll want to test access controls across these roles.
6. **Is there documentation?**  
    OpenAPI/Swagger, Postman collections, or internal docs can save huge amounts of time and help test for OWASP’s **Improper Inventory Management**.

## Initial Preparation Tasks(Must Do)

1. **Interact with the API normally**  
    Use the API as an intended user would — understand endpoints, expected inputs/outputs, workflows.
    
2. **Document use cases**  
    Define scenarios like user signup, role changes, or payment flows. Build your pentesting checklist around these.
    
3. **Adopt a testing methodology**  
    Use frameworks like:
    - **OWASP API Security Top 10**
    - **OWASP ASVS**
    - Or define a custom process tailored to your team and risk profile.

# Tools Setup

## Note-taking
- Use **CherryTree**, **Obsidian**, or other offline tools to keep findings secure and organized.
- Avoid cloud apps (e.g., Notion) for sensitive pentest data.

## API Hacking Tools
- **Burp Suite**: For proxying, intercepting, fuzzing, DAST, and automation.
- **Postman**: Manual testing and scripting test scenarios with collection runners.
- **APIsec Scan**: Great for automated testing using an OpenAPI spec or other inputs.
## Using APIsec Scan (Recommended by APISec)

1. **Import API** using OpenAPI spec, Postman collection, GraphQL, AWS, etc.
2. **Analyze endpoints**: Grouped by authentication needs, sensitivity, parameters.
3. **Run an unauthenticated scan** to establish a baseline and detect public issues.
4. **Configure authentication** to test role-based access controls and mass assignment issues.
5. **Review results**:
    - Vulnerabilities grouped by [[OWASP Top 10 Vulnerabilities]] category.
    - Each finding has method, endpoint, severity, CVSS score, and remediation guidance.
6. **Export reports** with detailed recommendations for dev and security teams.

# API Discovery – Finding Hidden or Undocumented Endpoints

## Manual API Discovery:

- Tools: **Wireshark**, source code reviews, analyzing bytecode, reading internal docs.    
- Good for complex or undocumented APIs but time-intensive.

## Automated API Discovery:

- Tools: **Burp**, **Amass**, **KiteRunner**, **OWASP ZAP**, **WFuzz**.    
- Great for speed and breadth but may miss logic-specific flaws.

**Best practice:** Combine both approaches — manual for depth, automated for scale.
