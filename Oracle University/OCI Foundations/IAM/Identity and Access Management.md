# **What is IAM in OCI?**

OCI Identity and Access Management (IAM) is a security service that:

- **Identifies users ([[[[AuthN and AuthZ|AuthN]])**: Username/password, security settings.
- **Controls access ([[AuthN and AuthZ|AuthZ]])**: Determines what resources they can use.

IAM is **role-based** and **fine-grained**, meaning:

- Users are grouped.
- Groups are assigned **roles**.
- **Policies** define **what actions** roles can perform on **which resources**.

# **Key Concepts in OCI IAM**

| Concept                    | Description                                                                      |
| -------------------------- | -------------------------------------------------------------------------------- |
| **Authentication (AuthN)** | Verifying the identity (e.g., via password, API keys)                            |
| **Authorization (AuthZ)**  | Determining what actions a user is permitted to perform                          |
| **Identity Domain**        | Logical boundary for managing users, groups, and auth settings                   |
| **User**                   | A person or application identity                                                 |
| **Group**                  | Collection of users to assign access uniformly                                   |
| **Policy**                 | Rules granting permissions to groups within a scope (tenancy, compartment)       |
| **[[Compartments]]**       | Logical container for OCI resources                                              |
| **Dynamic Group**          | A group based on instance metadata (for assigning policies to compute instances) |

# **Identity Domains in Practice**

- An **Identity Domain** is created first.
- Users and groups are added to it.
- Policies reference groups and define what actions they can take.
- The policies apply across **tenancy** or **compartments**.

![[Pasted image 20250723085708.png]]

# **OCID (Oracle Cloud Identifier)**

- Every resource in OCI (user, block volume, instance, etc.) gets a unique ID.
- Format:  `ocid1.<resource-type>.<realm>.<region>.<future_use>.<unique_ID>`
		

| Element         | Description                                     |
| --------------- | ----------------------------------------------- |
| `ocid1`         | OCID version identifier                         |
| `resource-type` | e.g., instance, volume                          |
| `realm`         | Group of regions (e.g., commercial, government) |
| `region`        | Geographic location                             |
| `unique_ID`     | System-generated string                         |
   
- **Examples**:
    - `ocid1.tenancy.oc1..aaaa...` – for tenancy (no region)
    - `ocid1.volume.oc1.eu-franfurt-1.aaaa...` – for a block volume in region `eu-franfurt` 
- You **see OCIDs** when using:
    - **OCI CL**        
    - **Terraform or SDK**
    - **Advanced API automation**

# **Real-World Use**

- **Console Users**: Rarely interact with OCIDs directly.
- **Developers/DevOps (CLI/SDK)**: Must know and use OCIDs regularly.
- **Security Admins**: Write IAM policies using group names, compartments, and actions.
