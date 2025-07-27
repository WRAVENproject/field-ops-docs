# OSINT Cheat Sheet (WRAVEN Edition)

**Last updated: July 26, 2025**
**Maintained by: WRAVEN Threat Research Team**

> Open-Source Intelligence (OSINT) is gathering info from public sources. This sheet covers methods, tools, tips, and workflows to make you an OSINT ninja—great for CTFs, investigations, and recon.

---

## 🔎 OSINT Basics

| Term         | Meaning                                                  |
| ------------ | -------------------------------------------------------- |
| OSINT        | Info collection from public sources (web, social, leaks) |
| HUMINT       | Human intelligence—talking to people                     |
| Footprinting | Mapping out digital footprint & surface data             |
| Doxxing      | Aggregating personal info (be ethical!)                  |
| Metadata     | Hidden file/data attributes (dates, GPS, software)       |
| Geolocation  | Pinpointing physical location from data                  |

> 🗒️ **Tip:** Always note your source and timestamp—public data changes.

---

## 🌐 Web Recon Techniques

1. **Search Engines:** Advanced operators

   * `site:example.com filetype:pdf password`
   * `intitle:"index of" "backup.sql"`
2. **Social Media:** Username / photo cross-checks

   * `"username" site:twitter.com`
   * Reverse-image search (Google, TinEye)
3. **Archive & History:**

   * Wayback Machine: check `web.archive.org`
   * Cached pages: `cache:example.com`
4. **Breach Data:**

   * `haveibeenpwned.com`
   * `dehashed.com`, `intelx.io`

> 🔍 **Advice:** Construct a query matrix: combine names, domains, filetypes, dates.

---

## 🔧 OSINT Tools & Platforms

| Tool / Site                   | Purpose                                 |
| ----------------------------- | --------------------------------------- |
| Google Dorks                  | Advanced search operators               |
| Maltego                       | Graph-based relationship mapping        |
| SpiderFoot                    | Automated data gathering                |
| Shodan                        | Internet-connected device search        |
| Censys                        | IPv4/SSL certificate enumeration        |
| theHarvester                  | Email, subdomain, IP harvesting         |
| Recon-ng                      | Framework for web recon modules         |
| Metasploit modules            | `auxiliary/gather/osint` scripts        |
| FOCA                          | File metadata and server fingerprinting |
| Social-Engineer Toolkit (SET) | Phishing and social recon               |

> 🔧 **Setup:** Use a dedicated VM or container. Isolate your recon tools from daily work.

---

## 🧭 People & Profile Discovery

| Technique       | Tool / Command                     |
| --------------- | ---------------------------------- |
| Username search | `usersearch.org`, BrandYourself    |
| Email patterns  | `hunter.io`, `email-format.com`    |
| Social profiles | `site:linkedin.com "First Last"`   |
| Photo match     | Google/TinEye reverse image search |

> 🧑‍💻 **Pro Tip:** Create a matrix of possible email formats: `first.last@domain`, `f.last@domain`, etc.

---

## 🌍 Geolocation & Mapping

| Task              | Tool / Method                   |
| ----------------- | ------------------------------- |
| IP to location    | `ipinfo.io/1.2.3.4`, `whois`    |
| Photo metadata    | `exiftool image.jpg`            |
| Map overlays      | Google Earth, QGIS              |
| Street view recon | `maps.google.com` → Street View |

> 🌐 **Advice:** Combine metadata with visual clues (landmarks, signs) to confirm.

---

## 🔗 Link & Network Analysis

1. **Domain/IP lookup:** `whois`, `dig`, `nslookup`
2. **SSL/TLS certs:** `crt.sh` → view certificate transparency log
3. **ASN & BGP:** `bgp.he.net` → track network ownership
4. **Reverse DNS:** `dig -x 1.2.3.4` → find hostnames

> 🕸️ **Insight:** Correlate domains by certs or WHOIS contacts to uncover clusters.

---

## 🔍 Document & Metadata Analysis

| File Type     | Tool / Command                  |
| ------------- | ------------------------------- |
| PDFs/DOCs     | `exiftool file.pdf`             |
| Images (JPEG) | `exiftool image.jpg`, `strings` |
| Office files  | `oletools`, `oleid`             |
| Presentations | `strings`, `zip -l file.pptx`   |

> 📑 **Checklist:** Always run metadata tools *before* opening files to avoid sandbox escapes.

---

## 💡 OSINT Workflow & Ethics

1. Define scope and objectives
2. Passive recon (no direct interaction)
3. Active recon (scanning, APIs)
4. Analyze and cross-verify findings
5. Document sources and methodology
6. Respect privacy and legal boundaries

> ⚖️ **Ethics Reminder:** Only gather public info. Don’t hack or phish—stick to open sources.

---

## 🔄 Continuous Monitoring

| Method              | Tool / Service                     |
| ------------------- | ---------------------------------- |
| Domain expiry       | `dnstwist`, `registrar APIs`       |
| Brand mentions      | Google Alerts, Talkwalker Alerts   |
| Certificate changes | `crt.sh` notifications             |
| Leak monitoring     | `Have I Been Pwned` API, LeakWatch |

> 🔔 **Tip:** Automate alerts to catch new intel without manual checks.

---

**WRAVEN Reminder:** OSINT is detective work—methodical, patient, and ethical. Record everything.

**Repo:** [github.com/WRAVENproject/field-ops-docs](https://github.com/WRAVENproject/field-ops-docs)

---

**Made for the field. Built by WRAVEN.**
