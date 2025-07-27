# Burp Suite Cheat Sheet (WRAVEN Edition)

**Last updated: July 26, 2025**
**Maintained by: WRAVEN Threat Research Team**

> Burp Suite is the Swiss Army knife for web hacking. This sheet covers proxies, scanners, intruders, repeaters, extensions, workflows, hotkeys, and tips to own web targets in CTFs or pentests.

---

## 🎛️ Setup & Config

1. **Proxy Settings**

   * Browser → Proxy to `127.0.0.1:8080`
   * Trust Burp CA: export from Proxy → Options → CA → install in browser

2. **Project vs Temporary**

   * Temporary: Quick start, no save
   * Project: Save configs, history, scope settings

3. **Scope Configuration**

   * Target → Scope → Include → add domains or CIDR
   * Exclude staging/dev & out-of-scope hosts
   * **Tip:** Enable "Scope only" in Scanner and Intruder to avoid noise.

---

## 🔍 Core Tools & Tabs

| Tool         | Purpose                               | Hotkey |
| ------------ | ------------------------------------- | ------ |
| Proxy        | Intercept, forward, modify HTTP(S)    | Ctrl+P |
| HTTP History | Review all proxied requests/responses |        |
| Repeater     | Craft & resend requests manually      | Ctrl+R |
| Intruder     | Automated payload fuzzing/bruteforce  | Ctrl+I |
| Scanner      | Active vulnerability scanning (Pro)   |        |
| Sequencer    | Analyze token/session randomness      |        |
| Comparer     | Diff two responses or requests        | Ctrl+E |
| Decoder      | Transform encodings, hashes, base64   | Ctrl+D |
| Extender     | Add extensions (BApp store & JARs)    |        |
| Collaborator | Out-of-band interactions & callbacks  |        |

> ⚙️ **Advice:** Start every engagement by capturing a full crawl via Proxy → HTTP history.

---

## 🚦 Intercept & Modify

* **Intercept On/Off:** Proxy → Intercept tab → toggle or Ctrl+I
* **Match & Replace:** Proxy → Options → Match and Replace → automate header or cookie tweaks
* **Intercept Filters:** Focus on methods/status codes (e.g., only intercept POSTs)
* **Break on Response Codes:** Proxy → Options → Intercept Client/Server responses for 500 / 302 etc.

> 🛑 **Tip:** Use "Intercept → Response interception" to catch redirects and embed custom logic.

---

## 🔄 Repeater Tricks

| Action               | Description                                     |
| -------------------- | ----------------------------------------------- |
| Send to Repeater     | Right-click request → Send to Repeater          |
| Auto-scroll Response | Options → Enable auto-scroll for streaming data |
| Show comments        | Annotate requests/responses                     |
| History navigation   | Up/Down arrows to cycle through recent requests |

> 🔁 **Advice:** Label key requests (login, search, upload) with colors and tags for quick access.

---

## ⚙️ Intruder Modes & Options

| Mode          | Use Case                                    |
| ------------- | ------------------------------------------- |
| Sniper        | Single payload position; pinpoint injection |
| Battering Ram | Same payload across all positions           |
| Pitchfork     | Parallel payload sets across positions      |
| Cluster Bomb  | All combinations of payload sets            |

### Payload Types

* **Simple list**: common words/passwords
* **Runtime file**: load large lists without memory bloat
* **Grep match**: filter good/bad responses by string or status

> 🚀 **Tip:** Use Intruder → Options → Throttle and Threads to avoid WAF blocks.

---

## 🔎 Scanner Highlights (Pro)

* **Active vs Passive**: Passive finds low-hanging info, Active validates issues
* **Scan in Scope Only**: minimize noise
* **Scan configurations**: Attack strength (Normal, Aggressive, Turbo)
* **Issue definitions**: tune alert thresholds
* **Scan Dashboard**: prioritize fix based on severity

> 🔍 **Advice:** Run passive scan during recon; schedule active scan during off-peak to avoid locking out.

---

## 🧩 Session Handling & Auth

* **Session Rules**: Extender → Auth → Session Handling Rules
* **Login sequence**: record login in Repeater → define rule to detect logged-in state
* **Token refresh**: handle JWT or OAuth tokens automatically via Macros
* **Macros**: Recorder to run prior requests before main attack

> 🔑 **Tip:** Use "Run a macro before request" in Intruder and Scanner for authenticated tests.

---

## 🛠 Extender & BApps

| Extension                | Use Case                     |
| ------------------------ | ---------------------------- |
| Autorize                 | WebSockets auth helper       |
| JSON Beautifier          | Pretty-print JSON responses  |
| J2EEScan                 | Find Java/J2EE vulns         |
| SQLiPy                   | Enhanced SQLi testing        |
| SAML Raider              | SAML analysis & exploitation |
| Burp Collaborator Client | Manage OAST interactions     |

> 🔌 **Tip:** Explore BApp store; enable only extensions you need to reduce memory.

---

## 🔧 Useful Features & Hotkeys

| Feature                 | Location / Hotkey                            |
| ----------------------- | -------------------------------------------- |
| Comparer                | Right-click → Compare (Ctrl+E)               |
| Decoder                 | Tools → Decoder (Ctrl+D)                     |
| Search in Request/Resp. | Ctrl+F                                       |
| Request Marking         | Right-click → Add comment or highlight color |
| Save state              | Project options → Save Project               |

> ⚡ **Pro Tip:** Use keyboard shortcuts for
> **intercept toggle**, **send to** actions, and **next request** to speed up workflows.

---

## 📜 Common Workflows

1. **Discovery:** Proxy → crawl with spider → save URLs
2. **Mapping:** use Repeater/Comparator to identify hidden params
3. **Exploitation:** Intruder + custom payloads → brute-forcing
4. **Validation:** Scanner (Pro) → verify XSS, SQLi, SSTI, etc.
5. **Reporting:** Export issues → include request/response samples

> 🏃‍♂️ **Workflow Tip:** Chain "Send to Intruder" → "Send to Scanner" for rapid attack loops.

---

## 💡 Pro Tips & Tricks

* **Match & Replace:** automatically remove anti-bot headers or tokens
* **Custom Payload Processing:** use grep, replace filters for dynamic fuzzing
* **Extender Scripting:** write Java or Python (via Jython) extensions for bespoke automation
* **Collaborator:** spin your own collaborator server for OAST instead of Burp's
* **Headless mode:** integrate via CLI for CI-based scans

> 🎯 **Note:** Burp can be memory-hungry; allocate 4–8GB in `burp.config`.

---

**WRAVEN Reminder:** Burp Suite is more than a proxy, it’s an integrated platform. Master proxies, scanners, and extensions for maximum impact.

**Repo:** [github.com/WRAVENproject/field-ops-docs](https://github.com/WRAVENproject/field-ops-docs)

---

**Made for the field. Built by WRAVEN.**
