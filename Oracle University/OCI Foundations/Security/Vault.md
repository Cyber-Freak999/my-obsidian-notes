# 🧾 **TL;DR: OCI Vault Service**

- **OCI Vault** is a **centralized, managed service** to securely store and manage:
    - **Encryption keys** (used for encrypting/decrypting data)
    - **Secrets** (passwords, SSH keys, API tokens, certificates, etc.)
- Keys can be stored in **software** or in **HSMs** (Hardware Security Modules).
    - HSMs offer **stronger security**, meet **FIPS 140-2 Level 3** compliance.
- Vault supports **AES**, **RSA**, and **ECDSA** algorithms.
- Uses **envelope encryption**:
    - A **Data Encryption Key (DEK)** encrypts the actual data.
    - A **Master Encryption Key (MEK)** encrypts the DEK.
- Integration with OCI services like Object Storage is **default** and seamless.
- You can **rotate keys** without re-encrypting all the data.
- Deleting a Vault **permanently destroys** all protected data, but deletion is **delayed (7–30 days)** to prevent accidental loss.

---

# 🔐 What Does OCI Vault Do?

- Eliminates the need to store sensitive data (keys/secrets) in code/config files.
- Provides a secure **centralized location** for:
    - **Keys**: Encrypt and decrypt data.
    - **Secrets**: Store and manage credentials securely.

# Key Protection Modes

| Mode         | Description                                                                                                                             |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| **Software** | Keys are stored on servers. Can be exported. Less secure.                                                                               |
| **HSM**      | Keys stored in tamper-proof hardware. Cannot be exported. Strong security (FIPS 140-2 Level 3). All operations are done inside the HSM. |
Key Algorithms Supported: AES, RSA and ECDSA
# 🧬 Envelope Encryption (How Vault Actually Works)

OCI Vault uses **2 levels of encryption**:

1. **Data Encryption Key (DEK):**
    - Used to **encrypt/decrypt actual customer data**.
    - Short-lived; discarded after use.
2. **Master Encryption Key (MEK):**
    - Stored in Vault (in software or HSM).
    - Used to **encrypt the DEK**.

> This two-layer structure is called **envelope encryption**.

## 🔒 Integration with OCI Services (e.g., Object Storage)

### 🔄 When Uploading (Encryption Flow):

1. Object Storage calls Vault to **generate a DEK**.    
2. Vault returns:
    - Plaintext DEK
    - **DEK encrypted** with the Master Key (MEK)
3. Object Storage:
    - Uses the DEK to encrypt the file
    - **Stores the encrypted file** + **encrypted DEK**
    - **Discards the plaintext DEK**

### 🔓 When Downloading (Decryption Flow):

1. Object Storage sends the **encrypted DEK** to Vault.    
2. Vault decrypts the DEK using the MEK.    
3. Object Storage uses the plaintext DEK to decrypt and serve the data.    

## 📌 Key Rotation & Deletion

- **Key Rotation**: Only the **MEK is rotated**, not the DEK or data. No re-encryption needed.
- **Key Deletion**:
    - Soft-deletion with **7–30 day delay**.
    - Once deleted, **data encrypted with those keys is unrecoverable**.
    - Vault deletion deletes all keys within it.
# ✅ Security Features

- **IAM policies**: Control who can use/manage keys.    
- **Audit logs**: Track all key access/usage.
- **Regional service**: Has a **public API endpoint**.
- Designed to prevent accidental key or Vault deletion.
