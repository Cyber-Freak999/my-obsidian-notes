---
tags:
  - crypto
  - concept
link: https://tryhackme.com/room/hashingbasics
prerequisites:
  - "[[Cryptography Basics]]"
  - "[[Public Key Cryptography Basics]]"
---
You can confirm the integrity of a file via hashes. A **hash value** is a fixed-size string or characters that is computed by a hash function. A **hash function** takes an input of an arbitrary size and returns an output of fixed length, i.e., a hash value.

# Hash Function

> [!NOTE] 
> Hash functions are different from encryption. There is no key, and it’s meant to be impossible (or computationally impractical) to go from the output back to the input.

A hash function takes some input data of any size and creates a summary or **digest** of that data. The output has a fixed size. It’s hard to predict the output for any input and vice versa.

The output of a hash function is typically raw bytes, which are then encoded. Common encodings are base64 or hexadecimal. `md5sum`, `sha1sum`, `sha256sum`, and `sha512sum` produce their outputs in hexadecimal format. 
> [!Important]
> Remember that hexadecimal format prints each raw byte as two hexadecimal digits.
## Why Hashing is important
Hashing helps protect data’s integrity and ensure password confidentiality. During login session, hashing is used to verify the password. This is because the server don't record the password as good security practice; it records the hash value of the password. So the hash value of the submitted password and the recorded hash value are compared.
## Hash Collision
A hash collision is when two different inputs give the same output. Hash functions are designed to avoid collisions as best as possible. Furthermore, hash functions are designed to prevent an attacker from being able to create, i.e., engineer, a collision intentionally. However, because the number of inputs is practically unlimited and the number of possible outputs is limited, this leads to a pigeonhole effect.

> [!NOTE] Calculating number of hash values from bit size
> Total number of possible hash values = $2^n$ (n = number of bit)

The **[pigeonhole effect](https://en.wikipedia.org/wiki/Pigeonhole_principle)** states that the number of items (_pigeons_) is more than the number of containers (_pigeonholes_); some containers must hold more than one item. In other words, in this context, there are a fixed number of different output values for the hash function, but you can give it any size input. As there are more inputs than outputs, some inputs must inevitably give the same output.
Related: [MD5 Collision Demo](https://www.mscs.dal.ca/~selinger/md5collision/) ,[SHA1 colliion attack](https://shattered.io/)
# Insecure Password Storage for Authentication
- Storing passwords in plaintext
- Storing passwords using a deprecated encryption
- Storing passwords using an insecure hashing algorithm
# Using Hashing for Secure Password Storage
This is where hashing comes in. What if, instead of storing the password, you just stored its hash value using a secure hashing function? This process means you never have to store the user’s password, and if your database is leaked, an attacker will have to crack each password to find out what the password was.
There’s just one problem with this. What if two users have the same password? As a hash function will always turn the same input into the same output, you will store the same password hash for each user.
That means if someone cracks that hash, they gain access to more than one account. It also means someone can create a Rainbow Table to break the hashes.
A **Rainbow Table** is a lookup table of hashes to plaintexts, so you can quickly find out what password a user had just from the hash. A rainbow table trades the time to crack a hash for hard disk space, but it takes time to create.

Websites like [CrackStation](https://crackstation.net/) and [Hashes.com](https://hashes.com/en/decrypt/hash) internally use massive rainbow tables to provide fast password cracking for **hashes without salts**. Doing a lookup in a sorted list of hashes is quicker than trying to crack the hash.

To protect against rainbow tables, we add a salt to the passwords. The salt is a randomly generated value stored in the database and should be unique to each user. In theory, you could use the same salt for all users, but duplicate passwords would still have the same hash and a rainbow table could still be created for passwords with that salt. Hash functions like Bcrypt and Scrypt handle this automatically. Salts don’t need to be kept private.

# Recognizing Password Hashes
Automated hash recognition tools such as [hashID](https://pypi.org/project/hashID/) exist but are unreliable for many formats. For hashes that have a prefix, the tools are reliable. Use a healthy combination of context and tools.  If you find the hash in a web application database, it’s more likely to be MD5 than NTLM (NT LAN Manager). Automated hash recognition tools often get these hash types mixed up, highlighting the importance of learning yourself.
## Linux Passwords
On Linux, password hashes are stored in `/etc/shadow`, which is normally only readable by root. They used to be stored in `/etc/passwd`, which was readable by everyone.
The `shadow` file contains the password information. Each line contains nine fields, separated by colons (`:`). The first two fields are the login name and the encrypted password.
The encrypted password field contains the hashed passphrase, saved in the format `$prefix$options$salt$hash`

| Unix-style Prefix              | Algorithm                                                                                                                                                                                        |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `$y$`                          | yescrypt is a scalable hashing scheme and is the default and recommended choice in new systems                                                                                                   |
| `$gy$`                         | gost-yescrypt uses the GOST R 34.11-2012 hash function and the yescrypt hashing method                                                                                                           |
| `$7$`                          | scrypt is a password-based key derivation function                                                                                                                                               |
| `$2b$`, `$2y$`, `$2a$`, `$2x$` | bcrypt is a hash based on the Blowfish block cipher originally developed for OpenBSD but supported on a recent version of FreeBSD, NetBSD, Solaris 10 and newer, and several Linux distributions |
| `$6$`                          | sha512crypt is a hash based on SHA-2 with 512-bit output originally developed for GNU libc and commonly used on (older) Linux systems                                                            |
| `$md5`                         | SunMD5 is a hash based on the MD5 algorithm originally developed for Solaris                                                                                                                     |
| `$1$`                          | md5crypt is a hash based on the MD5 algorithm originally developed for FreeBSD                                                                                                                   |
The prefix makes it easy to recognise Unix and Linux-style passwords; it specifies the hashing algorithm used to generate the hash.
## MS Windows Passwords
MS Windows passwords are hashed using NTLM, a variant of MD4. They’re visually identical to MD4 and MD5 hashes, so it’s very important to use context to determine the hash type.

On MS Windows, password hashes are stored in the SAM (Security Accounts Manager). MS Windows tries to prevent normal users from dumping them, but tools like mimikatz exist to circumvent MS Windows security. Notably, the hashes found there are split into NT hashes and LM hashes.

> [!tip]
> A great place to find more hash formats and password prefixes is the [Hashcat Example Hashes](https://hashcat.net/wiki/doku.php?id=example_hashes) page.

# Password Cracking

> [!NOTE] You can’t “decrypt” password hashes.
> They’re not encrypted. You have to crack the hashes by hashing many different inputs (such as `rockyou.txt` as it covers many possible passwords), potentially adding the salt if there is one and comparing it to the target hash. Once it matches, you know what the password was.

Tools: [Hashcat](https://hashcat.net/hashcat/), [John the Ripper](https://www.openwall.com/john/),[Ophcrack](https://ophcrack.sourceforge.io/)

You can use a graphics card to crack many hash types quickly. Some hashing algorithms, such as Bcrypt, are designed so that hashing on a GPU does not provide any speed improvement over using a CPU; this helps them resist cracking.
# Hashing for Integrity Checking
Hashing can be used to check that files haven’t been changed. If you put the same data in, you always get the same data out. Even if a single bit changes, the hash will change significantly. This means you can use it to check that files haven’t been modified or to ensure that the file you downloaded is identical to the file on the web server. Very common with when downloading ISO files from some major websites. They would always give a sha256sum hash and tell you to compare it to that of the file you downloaded.
## HMACs
**HMAC (Keyed-Hash Message Authentication Code)** is a type of [message authentication code](https://en.wikipedia.org/wiki/Message_authentication_code) (MAC) that uses a cryptographic hash function in combination with a secret key to verify the authenticity and integrity of data.
An HMAC can be used to ensure that the person who created the HMAC is who they say they are, i.e., authenticity is confirmed; moreover, it proves that the message hasn’t been modified or corrupted, i.e., integrity is maintained. This is achieved through the use of a secret key to prove authenticity and a hashing algorithm to produce a hash and prove integrity.
The following steps gives a fair idea of how HMAC works.
1. The secret key is padded to the block size of the hash function.
2. The padded key is XORed with a constant (usually a block of zeros or ones).
3. The message is hashed using the hash function with the XORed key.
4. The result from Step 3 is then hashed again with the same hash function but using the padded key XORed with another constant.
5. The final output is the HMAC value, typically a fixed-size string.

> [!NOTE] HMAC Formula
> $$HMAC(K,M) = H((K⊕opad||H((K⊕ipad)||M))\;
> where\; M = Message, K = Key$$


Related: [John the Ripper](John%20the%20Ripper%20-%20The%20Basics.md)