![[Pasted image 20250725141301.png]]

# ✅ **Key Best Practices**

1. **Don’t use the Tenancy Administrator for daily operations.**
    - Create a separate admin group (e.g., `OCI-Admins`) for managing day-to-day tasks.
2. **Use compartments to isolate resources.**
    - Create separate compartments for environments like **dev**, **prod**, **sandbox**, or **region-based** segmentation (e.g., NA, EU).
    - **Avoid putting everything in the root compartment.**
3. **Enforce Multi-Factor Authentication (MFA).**
    - Require at least **two factors** (e.g., password + mobile device).
    - Strongly recommended for all users, especially administrators.

---

# 🔧 **Setting Up the Tenancy Admin Delegation**

## 👤 **Tenancy Administrator**
- Has full access across the tenancy.
- Should **not** be used for day-to-day operations.

## 👥 **OCI Admin Group**
- Group of users who manage the tenancy on behalf of the tenancy admin.    
- Use **IAM policies** to grant them necessary permissions.

### 🛂 **Policies for OCI Admins**

Here are the **core policies** to define for the `OCI-Admins` group.

#### ✅ **1. Manage All Resources**

> Give them tenancy-wide or compartment-scoped access to manage all cloud services.

```plaintext
Allow group OCI-Admins to manage all-resources in tenancy
```

OR

```plaintext
Allow group OCI-Admins to manage all-resources in compartment <compartment-name>
```

#### ✅ **2. Manage Identity Resources (No Aggregated Resource Type!)**

Since IAM doesn’t have a single resource type for all Identity resources, you must **list each one explicitly**:

```plaintext
Allow group OCI-Admins to manage users in tenancy
Allow group OCI-Admins to manage groups in tenancy
Allow group OCI-Admins to manage dynamic-groups in tenancy
Allow group OCI-Admins to manage policies in tenancy
Allow group OCI-Admins to manage compartments in tenancy
Allow group OCI-Admins to manage domains in tenancy
Allow group OCI-Admins to manage identity-providers in tenancy
Allow group OCI-Admins to manage network-sources in tenancy
Allow group OCI-Admins to manage tag-namespaces in tenancy
Allow group OCI-Admins to manage tag-defaults in tenancy
```

You can also **scope these to a compartment** if needed.

