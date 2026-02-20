---
tags:
  - tool
  - crypto
  - cli
link: https://tryhackme.com/room/johntheripperbasics
prerequisites:
  - "[[Cryptography Basics]]"
  - "[[Public Key Cryptography Basics]]"
  - "[[Hashing Basics]]"
---
[Openwall Wiki](https://www.openwall.com/john/)

`john [options] [file path]`

- `john`: Invokes the John the Ripper program
- `[options]`: Specifies the options you want to use
- `[file path]`: The file containing the hash you’re trying to crack; if it’s in the same directory, you won’t need to name a path, just the file.

## Automatic Cracking
`john --wordlist=[path to wordlist] [path to file]`

- `--wordlist=`: Specifies using wordlist mode, reading from the file that you supply in the provided path
- `[path to wordlist]`: The path to the wordlist you’re using, as described in the previous task

**Example Usage:**

`john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt`

## Format-Specific Cracking
`john --format=[format] --wordlist=[path to wordlist] [path to file]`

- `--format=`: This is the flag to tell John that you’re giving it a hash of a specific format and to use the following format to crack it
- `[format]`: The format that the hash is in

**Example Usage:**

`john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt`

## Identifying Hashes
[Hashes.com](https://hashes.com/en/tools/hash_identifier), [hash-identifier](https://gitlab.com/kalilinux/packages/hash-identifier/-/tree/kali/master)


> [!Important] When you tell John to use formats, if you’re dealing with a standard hash type, e.g. md5 as in the example above, you have to prefix it with `raw-` to tell John you’re just dealing with a standard hash type, though this doesn’t always apply.

To check if you need to add the prefix or not, you can list all of John’s formats using `john --list=formats` and either check manually or grep for your hash type using something like `john --list=formats | grep -iF "md5"`.

# Cracking Windows Auth Hashes
Authentication hashes are the hashed versions of passwords stored by operating systems; it is sometimes possible to crack them using our brute-force methods. To get your hands on these hashes, you must often already be a privileged user, so we will explain some of the hashes we plan on cracking as we attempt them.

NThash is the hash format modern Windows operating system machines use to store user and service passwords. It’s also commonly referred to as NTLM, which references the previous version of Windows format for hashing passwords known as LM, thus NT/LM.

In Windows, SAM (Security Account Manager) is used to store user account information, including usernames and hashed passwords. You can acquire NTHash/NTLM hashes by dumping the SAM database on a Windows machine, using a tool like Mimikatz, or using the Active Directory database: `NTDS.dit`. You may not have to crack the hash to continue privilege escalation, as you can often conduct a “pass the hash” attack instead, but sometimes, hash cracking is a viable option if there is a weak password policy.
# Cracking Hashes from /etc/shadow
The `/etc/shadow` file is the file on Linux machines where password hashes are stored. It also stores other information, such as the date of last password change and password expiration information. It contains one entry per line for each user or user account of the system. This file is usually only accessible by the root user, so you must have sufficient privileges to access the hashes. However, if you do, there is a chance that you will be able to crack some of the hashes.

`unshadow [path to passwd] [path to shadow]`

- `unshadow`: Invokes the unshadow tool
- `[path to passwd]`: The file that contains the copy of the `/etc/passwd` file you’ve taken from the target machine
- `[path to shadow]`: The file that contains the copy of the `/etc/shadow` file you’ve taken from the target machine

**Example Usage:**
`unshadow local_passwd local_shadow > unshadowed.txt`


> [!NOTE] When using `unshadow`, you can either use the entire `/etc/passwd` and `/etc/shadow` files, assuming you have them available, or you can use the relevant line from each

We can then feed the output from `unshadow`, in our example use case called `unshadowed.txt`, directly into John. We should not need to specify a mode here as we have made the input specifically for John.

`john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt`

# Single Crack Mode
`john --single --format=[format] [path to file]`

- `--single`: This flag lets John know you want to use the single hash-cracking mode
- `--format=[format]`: As always, it is vital to identify the proper format.

**Example Usage:**

`john --single --format=raw-sha256 hashes.txt`

In this mode, John uses only the information provided in the username to try and work out possible passwords heuristically by slightly changing the letters and numbers contained within the username.

Consider the username “Markus”. Some possible passwords could be:
- Markus1, Markus2, Markus3 (etc.)
- MArkus, MARkus, MARKus (etc.)
- Markus!, Markus$, Markus* (etc.)
This technique is called **word mangling**.
John is building its dictionary based on the information it has been fed and uses a set of rules called “mangling rules,” which define how it can mutate the word it started with to generate a wordlist based on relevant factors for the target you’re trying to crack. This exploits how poor passwords can be based on information about the username or the service they’re logging into.

> [!NOTE] File Formats in Single Crack Mode
> If you’re cracking hashes in single crack mode, you need to change the file format that you’re feeding John for it to understand what data to create a wordlist from. You do this by prepending the hash with the username that the hash belongs to, so according to the above example, we would change the file `hashes.txt`
> From `1efee03cdcb96d90ad48ccc7b8666033`
> To `mike:1efee03cdcb96d90ad48ccc7b8666033`

# [John Custom Rules](https://www.openwall.com/john/doc/RULES.shtml)
Custom rules allow attackers to exploit the fact that we know the likely position of added elements to create dynamic passwords  that meet the **password complexity requirements** from our wordlists for cracking the hash.
Many organisations will require a certain level of password complexity to try and combat dictionary attacks. In other words, when creating a new account or changing your password, if you attempt a password like `polopassword`, it will most likely not work. Most time you'll see prompts for password complexity. However, we can exploit the fact that most users will be predictable in the location of these symbols.
Custom rules are defined in the `john.conf` file. It is usually located in `/etc/john/john.conf`

Example
```
[List.Rules:PoloPassword]
cAz"[0-9] [!£$%@]"
```
The first line `[List.Rules:<Rule-Name>]` is used to define the name of your rule; this is what you will use to call your custom rule a John argument.
We then use a regex style pattern match to define where the word will be modified

**Usage**
`john --wordlist=[path to wordlist] --rule=PoloPassword [path to file]`
# Cracking Password Protected Zip Files
`zip2john [options] [zip file] > [output file]`

- `[options]`: Allows you to pass specific checksum options to `zip2john`; this shouldn’t often be necessary
- `[zip file]`: The path to the Zip file you wish to get the hash of
- `>`: This redirects the output from this command to another file
- `[output file]`: This is the file that will store the output

**Example Usage**

`zip2john zipfile.zip > zip_hash.txt`

`john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt`

# Cracking Password Protected RAR Files
`rar2john [rar file] > [output file]`

- `rar2john`: Invokes the `rar2john` tool
- `[rar file]`: The path to the RAR file you wish to get the hash of
- `>`: This redirects the output of this command to another file
- `[output file]`: This is the file that will store the output from the command  

**Example Usage**

`/opt/john/rar2john rarfile.rar > rar_hash.txt`

`john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt`

# Cracking SSH Keys
`ssh2john` converts the `id_rsa` private key, which is used to log in to the SSH session, into a hash format that John can work with

`ssh2john [id_rsa private key file] > [output file]`

- `ssh2john`: Invokes the `ssh2john` tool
- `[id_rsa private key file]`: The path to the id_rsa file you wish to get the hash of
- `>`: This is the output director. We’re using it to redirect the output from this command to another file.
- `[output file]`: This is the file that will store the output from

**Example Usage**
`/opt/john/ssh2john.py id_rsa > id_rsa_hash.txt`

`john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt`