# Web Exploitation Cheat Sheet (WRAVEN Edition)

**Last updated: July 26, 2025**
**Maintained by: WRAVEN Threat Research Team**

> Web challenges test your skills on HTTP, inputs, auth, and server logic. This sheet covers common vulnerabilities, strategic approaches, tools, and tips to level up your web hacking game.

---

## 🧠 Web Recon & Enumeration

1. **Map the Application Surface**

   * Crawl all endpoints: use Burp Spider, `ffuf`, `gobuster`, and `wget --mirror`.
   * Bookmark interesting paths: `/admin`, `/api`, `/upload`, `/debug`.

2. **Gather Metadata & Comments**

   * View page source for hidden fields, comments, or credentials.
   * Check HTTP headers: `curl -I https://target` or Burp → Proxy → HTTP history.
   * Inspect JavaScript and JSON for API routes or secrets.

3. **Parameter Bruteforcing**

   * Use `ffuf` for URL params: `ffuf -u http://target/?FUZZ=1 -w params.txt`.
   * Fuzz JSON keys: `ffuf -X POST -H "Content-Type: application/json" -d '{"FUZZ":"test"}' -w params.txt`.

> 🔎 **Tip:** Keep a running list of endpoints and parameters in a note—helps track where to test.

---

## 🔓 Common Vulnerabilities & Exploits

| Category                              | Description                          | Tests / Tools                             |
| ------------------------------------- | ------------------------------------ | ----------------------------------------- |
| SQL Injection (SQLi)                  | Inject DB commands via inputs        | Burp Intruder, `sqlmap`, `sqlilabs`       |
| Blind SQLi                            | No direct output; infer via delays   | Boolean/time-based tests                  |
| Cross-Site Scripting                  | Inject JS for cookie theft           | `<script>alert(1)</script>`, Burp REQ     |
| Server-Side Template Injection (SSTI) | Execute code in templates            | `{{7*7}}` for Jinja, `#{7*7}` for ERB     |
| Local/Remote File Inclusion (LFI/RFI) | Load files via path traversal        | `../../etc/passwd`, `php://filter`        |
| Command Injection                     | Execute OS commands via unsafe input | `;id`, `&&ls`, Burp REQ                   |
| Server-Side Request Forgery (SSRF)    | Force server to make HTTP requests   | `http://localhost:8000`, Burp REQ         |
| Authentication Bypass                 | Skip login via logic flaws           | `admin'--`, `or 1=1`, `curl -u user:pass` |
| File Upload                           | Upload webshell via multipart form   | `php-reverse-shell.php`, Burp REQ         |
| Cross-Site Request Forgery (CSRF)     | Trick user into action               | Capture and replay tokens                 |
| Insecure Deserialization              | Deserialize data to run code         | `ObjectInputStream`, `ysoserial`          |
| JWT / Token Flaws                     | Tamper with tokens to escalate       | `jwt.io`, `jwt_tool`                      |

> 🛠 **Advice:** Test each input with `'</script>` or `';id` to quickly spot XSS or command injection.

---

## 🔧 Web Hacking Tools

| Tool                 | Purpose                            |
| -------------------- | ---------------------------------- |
| Burp Suite           | Proxy, scanner, intruder, repeater |
| OWASP ZAP            | Free web scanner and proxy         |
| FFUF / Gobuster      | Directory/param brute-forcing      |
| sqlmap               | Automated SQLi                     |
| wfuzz                | Flexible web fuzzer                |
| dalfox               | XSS scanning and exploitation      |
| nmap                 | Service discovery, scripts         |
| Nikto                | Web server scanner                 |
| dirb                 | Directory brute-forcing            |
| amass                | Subdomain enumeration              |
| whatweb / wappalyzer | Fingerprint tech stacks            |
| CyberChef            | Data transforms and encoding       |

> ⚙️ **Setup:** Use a hardened Kali VM or Docker container with all tools installed.

---

## 🛡 Effective Strategies

1. **Follow the Data Flow**

   * Identify entry points → backend processing → storage.
   * Test inputs at each stage: client side, server side, DB.

2. **Chain Vulnerabilities**

   * Combine LFI → log poisoning → RCE.
   * SSRF → metadata URL → cloud token leak.

3. **Automate Common Checks**

   * Write small scripts for `sqli`, `xss`, `ssti` patterns.
   * Use Burp macros for repeated form submissions.

4. **Bypass WAFs & Filters**

   * Try encodings: `URL`, `Unicode`, Base64.
   * Use comment injection: `/admin/*/password`.

> 🚀 **Pro Tip:** Build a cheatsheet of bypass payloads for each vuln type.

---

## 🎯 Testing Quick Wins

| Test             | Payload Example                           |
| ---------------- | ----------------------------------------- |
| SQLi – boolean   | `' OR '1'='1`                             |
| XSS – reflected  | `<script>alert(document.domain)</script>` |
| LFI – path trav. | `../../../../etc/passwd`                  |
| SSTI – Jinja     | `{{7*'7'}}`                               |
| Command Inj.     | `;whoami`                                 |
| SSRF             | `http://127.0.0.1:22`                     |
| CSRF             | Capture token, use `curl -X POST`         |

---

## 🔐 Defense & Detection

* Inspect logs for abnormal parameters.
* Monitor for multiple failed SQL or file load attempts.
* Enable Content Security Policy (CSP) against XSS.
* Use parameterized queries for DB.
* Validate and sanitize all user inputs.

> 🔒 **Note:** Knowing defenses helps you understand bypass techniques.

---

**WRAVEN Reminder:** Web hacking is about puzzles and logic—not memorizing every payload. Understand how data flows through the app.

**Repo:** [github.com/WRAVENproject/field-ops-docs](https://github.com/WRAVENproject/field-ops-docs)

---

**Made for the field. Built by WRAVEN.**

