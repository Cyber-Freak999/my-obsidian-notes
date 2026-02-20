---
tags:
  - concept
  - crypto
prerequisites:
  - "[[Cryptography Basics]]"
link: https://tryhackme.com/room/publickeycrypto
---
# Common use of Asymmetric Encryption
## The Core Problem (Why This Is Needed)

You and your friend want to communicate using a **shared secret code** (fast and efficient).  
But there’s a catch:

> **How do you safely send the secret code itself over an insecure channel?**

If you send it openly, anyone listening can steal it — and the whole system collapses.

This is known as the **key distribution problem**.
## A Clearer Metaphor
### Step 1: Your Friend Prepares a Lock

Your friend creates a **special lock** and keeps the **only key** to it.
- They give **copies of the lock** to everyone.
- They **never share the key**.
Important detail:

> Anyone can _lock_ the box, but **only your friend can unlock it**.
### Step 2: You Send the Secret Safely

You:
1. Put the **secret code instructions** (the symmetric key) into a box. 
2. Lock the box using **your friend’s lock**.
3. Send the locked box over the open world.
Even if someone intercepts it:
- They can’t open the box 
- They don’t have the key
### Step 3: Secure Communication Begins

Your friend:
1. Uses their **private key** to open the box
2. Reads the secret code instructions

Now both of you share the same secret and can communicate securely using the **faster secret code**, without needing locks anymore.
# RSA
RSA is a public-key encryption algorithm that enables secure data transmission over insecure channels. It is based on the mathematically difficult problem of factoring a large number

1. Bob chooses two prime numbers: _p_ = 157 and _q_ = 199. He calculates _n_ = _p_ × _q_ = 31243.
2. With _ϕ_(_n_) = _n_ − _p_ − _q_ + 1 = 31243 − 157 − 199 + 1 = 30888, Bob selects _e_ = 163 such that _e_ is relatively prime to _ϕ_(_n_); moreover, he selects _d_ = 379, where _e_ × _d_ = 1 mod _ϕ_(_n_), i.e., _e_ × _d_ = 163 × 379 = 61777 and 61777 mod 30888 = 1. The public key is (_n_,_e_), i.e., (31243,163) and the private key is $(n,d), i.e., (31243,379).
3. Let’s say that the value they want to encrypt is _x_ = 13, then Alice would calculate and send _y_ = _x__e_ mod _n_ = 13163 mod 31243 = 16341.
4. Bob will decrypt the received value by calculating _x_ = _y__d_ mod _n_ = 16341379 mod 31243 = 13. This way, Bob recovers the value that Alice sent.

_p_ and _q_ would be at least a 300-digit prime number each in real world application.

For dealing with RSA in ctfs, you need to know the main variables: p, q, m, n, e, d, and c. As per our numerical example:

- p and q are large prime numbers
- n is the product of p and q
- The public key is n and e
- The private key is n and d
- m is used to represent the original message, i.e., plaintext
- c represents the encrypted text, i.e., ciphertext

Some tools include [RsaCTFtool](https://github.com/Ganapati/RsaCtfTool) and [rsatool](https://github.com/ius/rsatool).
# Diffie-Hellman Key Exchange
**Key exchange** aims to establish a shared secret between two parties. It is a method that allows two parties to establish a shared secret over an insecure communication channel without requiring a pre-existing shared secret and without an observer being able to get this key. Consequently, this shared key can be used for symmetric encryption in subsequent communications.
Diffie-Hellman Key Exchange comes in where there is a need to establish a shared key for symmetric cryptography but no use asymmetric cryptography for the key exchange.
1. Alice and Bob agree on the **public variables**: a large prime number _p_ and a generator _g_, where 0 < _g_ < _p_. These values will be disclosed publicly over the communication channel. Although insecurely small, we will choose _p_ = 29 and _g_ = 3 to simplify our calculations.
2. Each party chooses a private integer. As a numerical example, Alice chooses _a_ = 13, and Bob chooses _b_ = 15. Each of these values represents a **private key** and must not be disclosed.
3. It is time for each party to calculate their **public key** using their private key from step 2 and the agreed-upon public variables from step 1. Alice calculates _A_ = $g^a\bmod{p}$ = 313 mod 29 = 19 and Bob calculates _B_ = $g^b \bmod{p}$ = 315 mod 29 = 26. These are the public keys.
4. Alice and Bob send the keys to each other. Bob receives _A_ = $g^a \bmod{p}$ = 19, i.e., Alice’s public key. And Alice receives _B_ = $g^b\bmod{p}$ = 26, i.e., Bob’s public key. This step is called the **key exchange**.
5. Alice and Bob can finally calculate the **shared secret** using the received public key and their own private key. Alice calculates $B^a\bmod{p}$ = 2613 mod 29 = 10 and Bob calculates $A^b \bmod{p}$ = 1915 mod 29 = 10. Both calculations yield the same result, $g^ab \bmod{p}$ = 10, the shared secret key.
# SSH
SSH authentication uses public and private keys to prove the client is a valid and authorised user on the server(key authentication). By default, SSH keys are RSA keys. You can choose which algorithm to generate and add a passphrase to encrypt the SSH key. `ssh-keygen` is the program usually used to generate key pairs. It would require a passphrase when generating it.
Types of algorithm for the keys:
- **DSA (Digital Signature Algorithm)** is a public-key cryptography algorithm specifically designed for digital signatures.
- **ECDSA (Elliptic Curve Digital Signature Algorithm)** is a variant of DSA that uses elliptic curve cryptography to provide smaller key sizes for equivalent security.
- **ECDSA-SK (ECDSA with Security Key)** is an extension of ECDSA. It incorporates hardware-based security keys for enhanced private key protection.
- **Ed25519** is a public-key signature system using EdDSA (Edwards-curve Digital Signature Algorithm) with Curve25519.
- **Ed25519-SK (Ed25519 with Security Key)** is a variant of Ed25519. Similar to ECDSA-SK, it uses a hardware-based security key for improved private key protection.

Using tools like John the Ripper, you can attack an encrypted SSH key to attempt to find the passphrase, highlighting the importance of using a complex passphrase and keeping your private key private.

When generating an SSH key to log in to a remote machine, you should generate the keys on your machine and then copy the public key over, as this means the private key never exists on the target machine using `ssh-copy-id`. The permissions must be set up correctly to use a private SSH key; otherwise, your SSH client will ignore the file with a warning. Only the owner should be able to read or write to the private key (`600` or stricter). `ssh -i privateKeyFileName user@host` is how you specify a key for the standard Linux OpenSSH client.

The `~/.ssh` folder is the default place to store these keys for OpenSSH. The `authorized_keys` (note the US English spelling) file in this directory holds public keys that are allowed access to the server if key authentication is enabled. By default on many Linux distributions, key authentication is enabled as it is more secure than using a password to authenticate. Only key authentication should be accepted if you want to allow SSH access for the root user.
# Digital Signatures and Certificates
Digital signatures provide a way to verify the authenticity and integrity of a digital message or document. Using asymmetric cryptography, you produce a signature with your private key, which can be verified using your public key. Only you should have access to your private key, which proves you signed the file. In many modern countries, digital and physical signatures have the same legal value.

The simplest form of digital signature is encrypting the document with your private key. If someone wants to verify this signature, they would decrypt it with your public key and check if the files match.

Certificates are an essential application of public key cryptography, and they are also linked to digital signatures. A common place where they’re used is for HTTPS.

These certificates have a chain of trust, starting with a root CA (Certificate Authority). This CA are, by default, acknowledged and trusted by your device, operating system, and web browser. Certificates are trusted only when the Root CAs say they trust the organisation that signed them.

Let’s say you have a website and want to use HTTPS. This step requires having a TLS certificate. You can get one from the various certificate authorities for an annual fee. Furthermore, you can get your own TLS certificates for domains you own using [Let's Encrypt](https://letsencrypt.org/) for free. If you run a website, it’s worth setting up and switching to HTTPS, as any modern website would do.
# PGP and GPG
**PGP** stands for Pretty Good Privacy. It’s software that implements encryption for encrypting files, performing digital signing, and more. [GnuPG or GPG](https://gnupg.org/) is an open-source implementation of the OpenPGP standard.

GPG is commonly used in email to protect the confidentiality of the email messages. Furthermore, it can be used to sign an email message and confirm its integrity.

You may need to use GPG to decrypt files in CTFs. With PGP/GPG, private keys can be protected with passphrases in a similar way that we protect SSH private keys. If the key is passphrase protected, you can attempt to crack it using John the Ripper and `gpg2john`