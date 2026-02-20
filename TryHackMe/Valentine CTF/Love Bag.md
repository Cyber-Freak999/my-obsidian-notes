# Objective

Uncover what’s hidden inside Cupid’s Vault web application.

```
My Dearest Hacker,

Cupid's Vault was designed to protect secrets meant to stay hidden forever. Unfortunately, Cupid underestimated how determined attackers can be. Intelligence indicates that Cupid may have unintentionally left vulnerabilities in the system. With the holiday deadline approaching, you've been tasked with uncovering what's hidden inside the vault before it's too late.

You can find the web application here: http://MACHINE-IP:5000
```

Target:

```
http://10.65.174.143:5000
```

---

#  Phase 1 – Reconnaissance

##  Service Fingerprinting

```bash
nikto -url http://10.65.174.143:5000
```

**Findings:**

- Server: `Werkzeug/3.1.5 Python/3.10.12`
- Methods allowed: `GET, HEAD, OPTIONS`
- `robots.txt` present
- Missing security headers

Port `5000` + Werkzeug strongly indicates a Flask application.

---

#  Phase 2 – robots.txt Enumeration

```bash
curl http://10.65.174.143:5000/robots.txt
```

Output:

```
User-agent: *
Disallow: /cupids_secret_vault/*

# cupid_arrow_2026!!!
```

### 🚨 Observations

- Hidden route: `/cupids_secret_vault/*`
- Comment contains suspicious string: `cupid_arrow_2026!!!`
    Likely a password

---

# Phase 3 – Vault Discovery

Accessing:

```
/cupids_secret_vault/
```

Page response:

> "You've found the secret vault, but there's more to discover..."

This implies:
- Further subroutes exist
- The vault is not the final destination

robots.txt wildcard confirmed subpaths are likely present.

---

# Phase 4 – Administrator Panel Discovery

Enumerating sub-domain:
```bash
ffuf -u http://10.65.174.143:5000/cupids_secret_vault/FUZZ -w /usr/share/wordlists/dirb/common.txt -mc 200,301,302,403
```

Discovered subroute:

```
/cupids_secret_vault/administrator
```

This is nested under the vault directory. This gave us a login page.

---

## 🔓 Phase 5 – Credential Reuse

Used credentials:

```
Username: admin
Password: cupid_arrow_2026!!!
```

Successful login → Flag retrieved.

---

# 🧠 Vulnerabilities Identified

## 1️⃣ Information Disclosure

Sensitive route and credential leaked in `robots.txt`.

## 2️⃣ Security Through Obscurity

Admin panel hidden but not protected properly.

## 3️⃣ Hardcoded Credentials

Static password exposed in application comment.

## 4️⃣ Weak Access Control

No:
- Rate limiting
- Lockout mechanism
- Additional authentication factors
