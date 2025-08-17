# 🔐 What is the **Shared Security Model**?

- In **on-premises**, _you own everything_, so _you're responsible for everything_.
    
- In **OCI (Oracle Cloud Infrastructure)**:    
    - **Oracle** is responsible for **security _of_ the cloud** (infrastructure, hardware, physical facilities, virtualization).
    - **You (the customer)** are responsible for **security _in_ the cloud** (data, access control, patching, endpoint security).


# 🛡️ **Defense in Depth**

Oracle uses a **"defense-in-depth"** strategy: security is built into **multiple layers** of the cloud stack.

Each layer addresses a different **use case** with specific OCI security services.
## 🔸 1. **Infrastructure Protection**

| 🔧 Use Case                         | 🛡️ Services                                                            |
| ----------------------------------- | ----------------------------------------------------------------------- |
| Protect apps from malicious traffic | **Web Application Firewall (WAF)** – filters L7 traffic, mitigates DDoS |
| Network-based threat prevention     | **Network Firewall** – intrusion detection/prevention                   |

## 🔸 2. **Identity and Access Management (IAM)**

| 🔧 Use Case                        | 🛡️ Services                                                             |
| ---------------------------------- | ------------------------------------------------------------------------ |
| Manage **who** can access **what** | **OCI IAM** – users, groups, dynamic groups, policies                    |
| Enforce secure login               | **Multifactor Authentication (MFA)** – requires 2+ forms of verification |
| Federated access                   | Identity Federation with external providers (e.g., Microsoft AD, SAML)   |

## 🔸 3. **Operating System and Workload Protection**

|🔧 Use Case|🛡️ Services|
|---|---|
|Secure boot and tamper protection|**Shielded Instances** – prevent unauthorized kernel/OS changes|
|Dedicated hardware for VM isolation|**Dedicated VM Host** – single-tenant bare metal servers|
|Patch/update large OS fleets|**OS Management** – manage OS-level updates and compliance at scale|

## 🔸 4. **Data Protection**

|🔧 Use Case|🛡️ Services|
|---|---|
|Encrypt and manage secrets|**Vault** – stores encryption keys and credentials (passwords, tokens)|
|Certificate management|**Certificates** – create/manage certificate authorities (CAs) and SSL certs|

- **Data at rest** encryption: default and cannot be turned off.
- **Bring Your Own Keys (BYOK)** support for stricter controls.

## 🔸 5. **Detection and Remediation** _(Cloud Security Posture Management)_

| 🔧 Use Case                                                   | 🛡️ Services                                                                                     |
| ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| Monitor, detect, and respond to misconfigurations and threats | **Cloud Guard** – auto-detects threats, config drift, user behavior                              |
| Enforce secure configurations                                 | **Security Zones** – define secure compartments that enforce Oracle best practices automatically |

![[Pasted image 20250801105321.png]]
# 🧠 Key Takeaways

- **Security is shared**: Oracle secures the infrastructure, you secure everything you put in it.
- **Multiple layers of protection**:
    - Network & app layer (firewalls)
    - Identity & access (IAM, MFA)        
    - OS & workloads (patching, shielded instances)
    - Data (encryption, key/cert management)
    - Governance (Cloud Guard, Security Zones)
- **Security is not a product**, it’s a **framework and ecosystem** embedded throughout OCI.
In a typical OCI environment:
- Your **compute**, **storage**, and **networks** are protected by: **Firewalls**, **IAM**, **Vault**, **Cloud Guard**, **auditing**, **Bastion**, **vulnerability scanning**, etc.
- You get both **manual** and **automated** options to _monitor, respond, and remediate_.

![[Pasted image 20250801105412.png]]