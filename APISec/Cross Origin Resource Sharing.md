# 🔍 **What is CORS?**

- **CORS is a browser-enforced security policy**, not a server-side defense.    
- It controls **which origins (domains)** can interact with your APIs via browser-based requests. 
- It **does not stop direct attacks** (e.g., via curl, Postman, backend scripts).    

---

## 🚨 **Why It Matters**

- Prevents **malicious sites** from interacting with your APIs using a logged-in user's browser.  
- Helps prevent **data theft, UI impersonation**, and **unauthorized API use**.

---

## ⚠️ **Common CORS Pitfalls**

- **Wildcard `*` in `Access-Control-Allow-Origin`** → Allows _anyone_ to use your API   
- **Copy-pasting from Stack Overflow** → Often sets unsafe defaults like open CORS for development.
- APIs go to **production with insecure CORS configs** due to dev shortcuts.

---

## 🔧 **Safe CORS Solution (Using Helmet in Express.js)**

Instead of the `cors` package that often defaults to permissive settings:

- Use [`helmet`](https://helmetjs.github.io/), which:   
    - Sets **secure HTTP headers**
    - Controls **allowed origins**, **methods**, and **resource access**
    - Includes broader protections beyond CORS (e.g., `Content-Security-Policy`, `X-Frame-Options`)

![[Pasted image 20250629053244.png]]

```js
import express from "express";
import helmet from "helmet";

const app = express();
app.use(helmet());

app.get("/", (req, res) => {
  res.send("Hello world!");
});

app.listen(8000);
```

---

## 🧱 **CORS vs Direct Attacks**

- **CORS only protects browser-based access.**    
- **Attackers sending direct requests** to your API **bypass CORS** completely.
- CORS protects **users**, not **your backend** — use **authentication & authorization** for real security.
