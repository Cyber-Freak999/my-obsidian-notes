# ✅ **TL;DR – Encryption Basics in OCI**

- **Encryption** transforms **plain text** into **cipher text** (unreadable).
- **Decryption** turns **cipher text** back into **plain text**, using a **key**.
- Two main encryption types:
    - **Symmetric**: same key used to encrypt and decrypt.
    - **Asymmetric**: uses a **key pair** (public + private).
- **Encryption at rest**: protects stored data.
- **Encryption in transit**: protects data moving between systems (e.g., HTTPS).
- **Common algorithms**: AES (symmetric), RSA (asymmetric), ECDSA (digital signing).
- **Hardware Security Module (HSM)**: a physical, tamper-resistant device that securely stores and manages encryption keys. Used behind OCI Vault.

---

# 🔐 **Encryption & Decryption Basics**

## **Encryption**

- Converts **plain text** (readable) ➡️ **cipher text** (unreadable).
- Prevents unauthorised access.
- **Cipher text** looks like random strings of letters/numbers.
## **Decryption**

- Reverse of encryption: transforms cipher text ➡️ plain text.
## **Encryption Key**

- A string of characters used during encryption/decryption.
- Without the correct key, the data remains unreadable.
# 📦 **Encryption at Rest vs. In Transit**

|Type|Description|
|---|---|
|**Encryption at Rest**|Protects data stored on disk (e.g., block storage, databases).|
|**Encryption in Transit**|Protects data while it's moving (e.g., over networks or the internet via HTTPS).|

- At rest: prevents someone from reading stored data without the key.
- In transit: prevents eavesdropping or tampering during data movement.
# 🔁 **Symmetric vs. Asymmetric Encryption**

## **Symmetric Encryption**

- **One key** is used for both encryption and decryption.
- Example:
    - John encrypts a message with a **secret key**.
    - Mike uses **the same secret key** to decrypt it.
- **Fast and efficient**, but the key must be securely shared between parties.
- Example algorithm: **AES**
## 🔹 **Asymmetric Encryption**

- **Two keys**: a public key and a private key.    
- Example:
    - Mike has a **key pair**.
    - John uses Mike’s **public key** to encrypt a message.
    - Only Mike can decrypt it using his **private key**.
- Public key = shared openly
- Private key = kept secret
- **More secure for communication** (no need to share private keys).
- Example algorithm: **RSA**

# 🧮 **Encryption Algorithms**

| Algorithm | Type                 | Use Case                                | Notes                                                                |
| --------- | -------------------- | --------------------------------------- | -------------------------------------------------------------------- |
| **AES**   | Symmetric            | Fast encryption/decryption              | Uses 128-, 192-, or 256-bit keys. Widely used in cloud and hardware. |
| **RSA**   | Asymmetric           | Secure key exchange, digital signatures | Uses key pairs. Slower than AES but great for security.              |
| **ECDSA** | Asymmetric (Signing) | Digital signatures only                 | Elliptic curve cryptography. Not used for encrypting data.           |
Use **RSA** for secure sharing, **AES** for speed.
# 🧱 **Hardware Security Module (HSM)**

- A **physical device** used to **store and protect encryption keys**.    
- Performs cryptographic operations securely (e.g., encryption, digital signing).    
- **Tamper-resistant**: If someone tampers with it, the key can self-destruct.
- In OCI:
    - Used **behind the scenes in Oracle Vault** service.
    - Complies with **[FIPS 140-2](https://en.wikipedia.org/wiki/FIPS_140-2) Level 3**, a strong security certification.
