# What roles exist in OCI Identity Domains?

Oracle Cloud Identity Domains support **predefined roles** that help manage different areas of access and responsibility. These roles are used to assign **delegated administration** and access to apps, users, and configurations **within a domain**.
Common OCI Identity Domain Roles:

|**Role**|**Purpose / Permissions**|
|---|---|
|**Domain Administrator**|Full admin over the identity domain: manage users, groups, settings, apps, policies.|
|**Security Administrator**|Can manage security settings like password policies, MFA, risk-based policies.|
|**Application Administrator**|Manage app integrations, SSO, SCIM provisioning, OAuth/SAML settings.|
|**Group Administrator**|Can manage group membership and group-based role assignments.|
|**User Administrator**|Can create, modify, and delete users, assign roles, and reset passwords.|
|**Audit Administrator**|Can view logs and audit reports but can’t make changes.|
|**Help Desk Administrator**|Reset MFA, unlock accounts — limited support tasks.|

> These roles are **assignable to users** within a specific identity domain (not tenancy-wide unless scoped that way).

---

# What is Delegated Administration, and How Do You Assign It?

## **What Is Delegated Administration?**

Delegated administration in OCI means assigning **specific administrative responsibilities** to other users **without giving them full tenancy or root-level access**.

This helps enforce **principle of least privilege** while distributing management tasks across teams (e.g., giving HR team user admin rights, dev team app admin rights).

## **How to Assign Delegated Admin:**

1. **Go to Identity & Security → Domains**
    
2. Select your **Identity Domain**.
    
3. Go to **Users**, select a user.
    
4. Under the **Roles tab**, click **Assign Role**.
    
5. Choose a **role** (like “User Administrator”) and **scope** (Domain-wide or application-specific).
    
6. Save.
## Example:

- A user in HR is assigned **User Administrator** role → Can manage user accounts, reset passwords, assign groups.
    
- A DevOps lead is assigned **Application Administrator** role → Can manage SSO settings for GitHub or Jira integrations.
    

>  This helps break away from “everyone is admin” model — better control, auditing, and security.

---

# What’s the Difference Between Default Domain Policies and Compartment-Level IAM Policies?

These are **two separate layers of access control** in OCI:

| **Aspect**        | **Identity Domain Policies**                                          | **IAM Policies (Tenancy/Compartment)**                                           |
| ----------------- | --------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| **Scope**         | Control what users can do **inside the domain** (users, apps, roles). | Control access to **OCI resources** (compute, storage, DB, etc.) across tenancy. |
| **Used For**      | Managing identity configurations, domain roles, app access.           | Granting permissions like `allow group X to manage compute in compartment Y`.    |
| **Where Defined** | Inside the **identity domain** (via roles and domain config).         | In **IAM service** under Identity → Policies.                                    |
**Examples**
- Who can create new users                 
- Who can manage MFA settings
- Who can edit SSO apps
- Who can launch VMs
- Who can access Object Storage
- Who can view budgets     

> 💡 **Important:** Adding a user to a group in the **domain** gives them domain-level roles.  
> But to access **cloud resources**, you must write **IAM policies** (in root/compartment scope) that reference those groups.

---
# How does replication of identity domains work in OCI?

**By default**, only the **default identity domain** is automatically **replicated** across all regions you have subscribed to in your tenancy.

For **additional (custom) identity domains**:

- They are **region-specific** by default.
    
- You **must manually enable replication** if users in that domain need access to OCI resources in other subscribed regions.
    

**How to enable replication:**

1. Go to the **Identity Domains** section in the OCI Console.
    
2. Select the domain you want to replicate.
    
3. Choose **Replication Settings**.
    
4. Select the additional regions where you want this domain to be replicated.
    
5. Confirm and apply the changes.
    

**Note:** Replication is useful for:

- High availability across regions.
    
- Allowing users to authenticate and access resources in other regions without latency or failure.
    

---
# Can domains be renamed or deleted after creation?

#### **Renaming:**

- **Not allowed.** Once an identity domain is created, its **name (OCID and display name)** is **permanent** and cannot be changed.
    
- If you need a domain with a different name, you'd need to **create a new one** and migrate users or resources.
    

#### **Deletion:**

- **Yes**, but with restrictions:
    
    - You must first **delete all users**, groups, apps, and configurations inside the domain.
        
    - You also need to **remove any active sessions or federation links**.
        
    - Only then can you delete the domain via the console or API.
        

**Caution:** Deleting an identity domain is **irreversible** and may result in **loss of data**, including all identity objects within that domain.

---

# How does billing or cost management differ with multiple identity domains?

- OCI **does not charge separately** for creating multiple identity domains — the **cost is typically bundled** within your tenancy subscription.
    
- However, **indirect costs** may apply:
    
    - **Increased usage of IAM resources** (e.g., more MFA configurations, app integrations).
        
    - **Custom features** like Identity Governance, SCIM provisioning, or external identity federation **may incur charges** if activated per domain.
        
    - **Resource replication across regions** (e.g., for identity domains or other linked services) can increase costs.
        

**Tip:** Use **OCI Cost Analysis** to monitor usage and filter by identity domain-related services if needed.

---

# What are limitations of having too many identity domains in one tenancy?

While OCI supports multiple identity domains, keep in mind the following limitations:

|Limitation|Details|
|---|---|
|**Management Overhead**|More domains mean more complexity in managing users, roles, and policies. You’ll need to define and maintain configurations per domain.|
|**Policy Fragmentation**|IAM policies and security rules become scattered, making it harder to audit and maintain a consistent security posture.|
|**Cross-domain Sharing**|Domains are **logically isolated**. Sharing users or apps between them is not supported directly. You’d need to duplicate configurations or federate externally.|
|**Service Limits**|OCI imposes **soft limits** (which can be increased via request) on the number of identity domains per tenancy. The default is often **up to 5 or 10 domains**, depending on the region or contract.|
|**Lack of Unified Identity View**|No built-in way to view all users across domains in one interface. You'll need to check each domain separately.|
|**Replication Management**|Each domain’s replication has to be managed **individually**, increasing the operational effort in multi-region deployments.|

---
# Can groups be nested (i.e., groups within groups) in OCI IAM?

### ❌ **Short Answer: No, OCI IAM does not support nested groups.**

## Explanation:

- OCI IAM follows a **flat group structure**.    
- **Users can belong to multiple groups**, but **groups cannot contain other groups**.
- This design avoids ambiguity in permission resolution and simplifies policy evaluation.
##  Workaround:

While you can't nest groups, you can simulate similar functionality:

- **Assign the same user to multiple groups**.
- Use **group-based naming conventions** to reflect hierarchy, e.g.:
    - `AppTeam`
    - `AppTeam_ReadOnly`
    - `AppTeam_Admin`

Then write policies accordingly:

```plaintext
Allow group AppTeam_ReadOnly to read all-resources in compartment MyApp
Allow group AppTeam_Admin to manage all-resources in compartment MyApp
```

This gives you **fine-grained control** without nesting.

---

# How does group assignment affect application access and SSO integrations?

### ✅ **Group assignment is central to controlling app access and SSO behavior in OCI.**

## Here's how it works:

### **A. Application Access:**

- When integrating an app (like Oracle Fusion, Salesforce, custom apps), you can **assign it to specific groups**.
    
- Only **users in the assigned group(s)** will be able to **see and launch the app** from their OCI dashboard or via SSO.
    

> Example: Assign the `HR_Team` group to an HR application → only HR team members can access it.

### **B. SSO (Single Sign-On):**

- Group membership defines which users are **provisioned to external identity providers or SaaS apps**.
    
- OCI supports SCIM provisioning for many apps (e.g., Microsoft 365, ServiceNow), and groups are used to determine **who gets synced**.
    
- **Federation rules and access policies** can also be built around groups for **granular control**.
    

### **C. "All Domain Users" Group Impact:**

- This group includes **every user** in the domain by default.
    
- If you assign an app to "All Domain Users," **everyone** will get access — which can be risky if not intended.
    

## 🛡️ Best Practices for Application Access & SSO:

1. **Use dedicated groups for each application** (e.g., `SalesforceUsers`, `DevToolsAccess`).
    
2. **Avoid assigning sensitive apps to “All Domain Users.”**
    
3. **Use attribute-based rules** where supported (e.g., job title, department) to automate group membership.
    
4. **Audit group memberships regularly** to ensure proper access control.
    
5. For SCIM or SAML-based apps, map group claims carefully to avoid overprovisioning.
