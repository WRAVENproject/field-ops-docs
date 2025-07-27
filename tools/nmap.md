# Nmap Cheat Sheet 2025 (WRAVEN Edition)

**Last updated: July 17, 2025**
**Maintained by: WRAVEN Threat Research Team**

> **Purpose:** This cheat sheet is a quick-reference guide for security researchers, students, and red teamers working with Nmap. Built by WRAVEN to reduce lookup time.

---

## 🛠️ Nmap Basics

**What is Nmap?**
Nmap (Network Mapper) is a free and open-source tool used for network discovery, port scanning, OS detection, and service enumeration.

**Common Use Cases:**

* Discovering open ports
* Detecting live hosts
* Identifying services and versions
* OS fingerprinting
* Automating recon

---

## 🎯 Target Specification

| Command                        | Description           |
| ------------------------------ | --------------------- |
| `nmap 192.168.1.1`             | Scan a single IP      |
| `nmap 192.168.1.1 192.168.2.1` | Scan specific IPs     |
| `nmap 192.168.1.1-254`         | Scan a range          |
| `nmap 192.168.1.0/24`          | CIDR notation         |
| `nmap scanme.nmap.org`         | Scan a domain         |
| `-iL targets.txt`              | Scan from a file      |
| `-iR 100`                      | Scan 100 random hosts |
| `--exclude 192.168.1.1`        | Skip specific IPs     |

---

## 🔍 Scan Techniques

| Command | Description                         |
| ------- | ----------------------------------- |
| `-sS`   | TCP SYN scan (default if root)      |
| `-sT`   | TCP connect scan (default w/o root) |
| `-sU`   | UDP scan                            |
| `-sA`   | TCP ACK scan                        |
| `-sW`   | TCP Window scan                     |
| `-sM`   | TCP Maimon scan                     |

---

## 🖥️ Host Discovery

| Command | Description                    |
| ------- | ------------------------------ |
| `-sL`   | List targets only, no scan     |
| `-sn`   | Ping scan only, no port scan   |
| `-Pn`   | Skip host discovery, assume up |
| `-PS`   | TCP SYN ping                   |
| `-PA`   | TCP ACK ping                   |
| `-PU`   | UDP ping                       |
| `-PR`   | ARP discovery (local net)      |
| `-n`    | Skip DNS resolution            |

---

## 🔢 Port Scanning

| Command            | Description               |
| ------------------ | ------------------------- |
| `-p 80`            | Scan a specific port      |
| `-p 20-100`        | Scan a range              |
| `-p U:53,T:21-25`  | Mixed TCP/UDP scan        |
| `-p-`              | Scan all 65535 ports      |
| `-F`               | Fast scan (top 100 ports) |
| `--top-ports 2000` | Scan top 2000 ports       |

---

## 🔍 Service & Version Detection

| Command                   | Description                                       |
| ------------------------- | ------------------------------------------------- |
| `-sV`                     | Detect service versions                           |
| `-A`                      | Aggressive scan: version, OS, scripts, traceroute |
| `--version-intensity 0-9` | Set detection intensity                           |
| `--version-light`         | Quicker, less accurate                            |
| `--version-all`           | Max intensity                                     |

---

## 🧠 OS Detection

| Command            | Description             |
| ------------------ | ----------------------- |
| `-O`               | Enable OS detection     |
| `--osscan-guess`   | Be more aggressive      |
| `--osscan-limit`   | Skip if too little info |
| `--max-os-tries 1` | Limit attempts          |

---

## 🧪 NSE Scripts (Nmap Scripting Engine)

| Command                             | Description         |
| ----------------------------------- | ------------------- |
| `-sC`                               | Default scripts     |
| `--script=banner`                   | Run a single script |
| `--script=http*`                    | Wildcard match      |
| `--script-args snmpcommunity=admin` | Script arguments    |

### ⚡ Useful NSE Examples

```bash
nmap -Pn --script=http-sitemap-generator scanme.nmap.org
nmap -Pn --script=dns-brute domain.com
nmap -p80 --script=http-sql-injection scanme.nmap.org
```

---

## 🐢 Timing & Stealth

| Command | Description               |
| ------- | ------------------------- |
| `-T0`   | Paranoid (very slow)      |
| `-T3`   | Default timing            |
| `-T4`   | Aggressive (CTF-friendly) |
| `-T5`   | Insane (use with care)    |

## 📦 Output Options

| Command          | Description                     |
| ---------------- | ------------------------------- |
| `-oN normal.txt` | Normal text output              |
| `-oX xml.xml`    | XML format                      |
| `-oG grep.txt`   | Greppable format                |
| `-oA out`        | All formats with basename "out" |

---

## 🧱 IDS Evasion Tricks

| Command               | Description                  |
| --------------------- | ---------------------------- |
| `-f`                  | Fragment packets             |
| `--data-length 200`   | Add random padding           |
| `-D decoy1,decoy2,me` | Use decoys                   |
| `-S spoofed.ip.addr`  | Spoof source IP (needs root) |

---

## 🧪 Example Recon Command

```bash
nmap -sS -Pn -T4 -A -p- -oA fullscan 192.168.1.0/24
```

---

**WRAVEN Reminder:** Tools don’t hack, humans do. Nmap is your recon scalpel—learn where to cut, not just how.

**Repo:** [github.com/WRAVENproject/field-ops-docs](https://github.com/WRAVENproject/field-ops-docs)

**Made for the field. Built by WRAVEN.**
