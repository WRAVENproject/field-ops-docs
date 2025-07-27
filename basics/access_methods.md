# Standard Access Methods (WRAVEN Edition)
**Last updated: July 26, 2025**  
**Maintained by: WRAVEN Threat Research Team**

> Overview of common ways into systems. Useful for CTFs, real-world testing, and spotting where attackers might sneak in.

---

## 💻 Remote Shells & Admin Access

### 🔹 SSH (Secure Shell)
| Command | Description |
|---------|-------------|
| `ssh user@host` | Standard login |
| `ssh -i id_rsa user@host` | Login with private key |
| `ssh -p 2222 user@host` | Specify port |

**Ports:** TCP 22  
**Bonus:** Try default creds, check for weak keys, look for reused credentials.

---

### 🔹 Telnet
| Command | Description |
|---------|-------------|
| `telnet host 23` | Connect to default Telnet port |

**Ports:** TCP 23  
**Notes:** Plaintext auth. If it’s open, it’s already a red flag.

---

## 🖨️ Print Services

### 🔹 IPP (Internet Printing Protocol)
| Command | Description |
|---------|-------------|
| `lpstat -h ipp://target -p` | List printers |
| `lpadmin -p printer -E -v ipp://target/printer` | Add printer connection |

**Ports:** TCP 631  
**Notes:** Often overlooked. Can be used for info leaks or command injection via PostScript.

---

## 📁 File Sharing Protocols

### 🔹 SMB / CIFS
| Command | Description |
|---------|-------------|
| `smbclient -L //target/ -U guest` | List shares |
| `smbclient //target/share -U user` | Connect to a share |
| `enum4linux target` | Basic enumeration |

**Ports:** TCP 445, 139  
**Bonus:** Look for null sessions, guest access, or weak creds.

---

### 🔹 FTP (File Transfer Protocol)
| Command | Description |
|---------|-------------|
| `ftp target` | Connect via interactive shell |
| `ftp anonymous@target` | Try anonymous login |

**Ports:** TCP 21  
**Notes:** Try brute-forcing, and check for file upload permissions.

---

## 🧪 Web-Based Entry Points

### 🔹 HTTP Auth / Admin Panels
- Check for `/admin`, `/login`, `/phpmyadmin`, etc.
- Use `hydra`, `ffuf`, or manual login attempts
- Watch for weak or default creds: `admin:admin`, `root:toor`

**Ports:** TCP 80 (HTTP), 443 (HTTPS)

---

## 🖥️ RDP (Remote Desktop Protocol)
| Command | Description |
|---------|-------------|
| `xfreerdp /u:user /p:pass /v:target` | Linux RDP login |
| `rdesktop target` | Legacy client |

**Ports:** TCP 3389  
**Notes:** Loud on network. Great target for weak creds or ticket abuse (Kerberos).

---

## 🔑 Other Services to Probe
| Service | Port | Tool / Notes |
|---------|------|--------------|
| VNC | 5900 | Use `vncviewer`, check for no auth |
| SNMP | 161 | Use `snmpwalk -v1 -c public target` |
| NFS | 2049 | Use `showmount -e target`, `mount` shares |
| LDAP | 389 | Use `ldapsearch`, enum users |
| Kerberos | 88 | Use `GetNPUsers.py` from Impacket |

---

## 🔎 Tools for Brute-Forcing & Login Attacks
| Tool | Use |
|------|-----|
| `hydra` | Fast login bruteforcer |
| `medusa` | Login bruteforce, parallelized |
| `ncrack` | Like hydra, but cleaner output |
| `crackmapexec` | Great for SMB/Win networks |

---

**WRAVEN Tip:** If it accepts logins, it’s a target. Don’t skip over old or weird protocols—those are often the ones attackers abuse.

**Repo:** [github.com/WRAVENproject/field-ops-docs](https://github.com/WRAVENproject/field-ops-docs)

---

Made for the field. Built by WRAVEN.
