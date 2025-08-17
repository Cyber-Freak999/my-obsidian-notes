# **What Is a Compartment in OCI?**

A **compartment** in Oracle Cloud Infrastructure (OCI) is a **logical container** used to organize and isolate cloud resources. It plays a crucial role in managing access, organizing resources, and tracking usage.
When you open an OCI account, you get a **tenancy**, which is essentially your cloud account.  
Within this tenancy, OCI creates a default container called the **Root Compartment**. This compartment can hold all your resources, but it's **best practice not to use it as a catch-all**.
Instead, you should create your own **dedicated compartments** to keep your resources organized and access-controlled.

---

# **Why Use Compartments?**

- **Isolation of resources**  
    Helps in separating different environments (like dev, test, prod) or departments. 
- **Access control**  
    You can apply IAM policies to restrict which users or groups can access which compartments.
- **Cleaner organization**  
    Keeps your resources grouped logically, improving manageability and clarity.

---

# **Resource Assignment to Compartments**

- Every OCI resource (like a VM, VCN, or bucket) **must belong to exactly one compartment**.
- Resources **cannot belong to multiple compartments** at the same time.
- If needed, you can **move a supported resource** from one compartment to another.

---

# **Cross-Compartment Resource Interaction**

Resources in different compartments **can still interact** with each other.  
For example, a **compute instance in one compartment** can use a **VCN in another compartment**. This enables flexible and scalable architectures while keeping resources logically separated.

---

# **Global Scope of Compartments**

- Compartments are **global constructs**.
- Once created, a compartment is available in **all OCI regions** you have access to.
- You can still **restrict access to specific regions** using policies, even though the compartments themselves are visible globally.

---

# **Nested Compartments**

OCI supports up to **six levels of nested compartments**.  
This allows you to structure compartments in a way that mimics your organization or team hierarchy. For example:

```
Root
 └── Finance
      ├── Billing
      ├── Compliance
      └── Analytics
```

---

### **Quotas and Budgets on Compartments**

- You can set **quotas** to limit resource types or usage within a compartment  
    (e.g., prevent bare metal machines in a dev environment).
- You can set **budgets** on compartments to track and control costs.  
    Alerts can be triggered if spending exceeds a defined threshold.

---

# **Best Practices**

- **Avoid using the Root Compartment** for all resources.    
- Create **logical, dedicated compartments** for teams, projects, or resource types.
- Use **IAM policies** to manage access at the compartment level.
- Take advantage of **nested compartments** for clearer organizational mapping.
- Monitor usage and spending through **quotas and budgets**.

![[Pasted image 20250723125224.png]]