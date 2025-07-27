# Basics: Common Terms, Slang, & Stuff You Should Know (WRAVEN Edition)

**Last updated: July 26, 2025**
**Maintained by: WRAVEN Threat Research Team**

> New to cybersecurity? Start here. This isn't just a glossary—it's a quick intro to how people talk, think, and learn in this field. Whether you're here for CTFs, career prep, or just hacking for fun, these are the words, ideas, and mental models that help everything click.

---

## 🧠 General Terms

| Term    | Meaning                                                                                             |
| ------- | --------------------------------------------------------------------------------------------------- |
| CTF     | Capture The Flag – a hacking competition with challenges like web, crypto, reversing, and forensics |
| Shell   | Command-line access to a system (bash, sh, cmd, etc.)                                               |
| TTY     | Terminal session – makes your shell behave more like a real local one                               |
| RE      | Reverse Engineering – figuring out how code/binaries work by pulling them apart                     |
| Payload | The code you run after exploiting a vuln (e.g., reverse shell, add-user script)                     |
| POC     | Proof of Concept – a minimal example showing that a technique works                                 |
| Pivot   | Using one compromised machine to reach others                                                       |
| OPSEC   | Operational Security – not getting caught, burning tools, or leaking info                           |

> ✏️ **Tip:** You don’t need to memorize all this. Skim it, use it, and revisit it when it shows up in a writeup or tool output.

---

## 🔗 Network & Protocol Basics

| Term | Meaning                                                         |
| ---- | --------------------------------------------------------------- |
| IP   | Internet address of a system (IPv4: `192.168.0.1`)              |
| Port | Virtual channel for services (e.g., 22 = SSH, 80 = HTTP)        |
| DNS  | Turns names (`example.com`) into IPs                            |
| TCP  | Reliable, ordered network connection (handshake + stream)       |
| UDP  | Fast but unreliable network traffic (no handshake)              |
| ICMP | Protocol used by `ping` and `traceroute`                        |
| HTTP | Protocol used to load websites                                  |
| FTP  | File Transfer Protocol – often misconfigured, check for uploads |
| SMB  | Windows file sharing – can leak creds or allow access to shares |

> 🔍 **Advice:** When in doubt, draw a packet flow diagram. Even a doodle helps connect the dots.

---

## 🔍 Recon & Exploitation Concepts

| Term        | Meaning                                                                  |
| ----------- | ------------------------------------------------------------------------ |
| Enumeration | Actively discovering info on a target (users, services, files)           |
| Brute Force | Trying lots of inputs (passwords, URLs) to find valid ones               |
| LFI / RFI   | Local/Remote File Inclusion – tricking a web app to load files           |
| SQLi        | SQL Injection – injecting database commands into a query                 |
| XSS         | Cross-Site Scripting – injecting JS that runs in someone else's browser  |
| SSRF        | Server-Side Request Forgery – making the server request internal systems |
| Privesc     | Privilege Escalation – going from user → admin/root                      |
| CVE         | Common Vulnerabilities and Exposures – public catalog of bugs            |
| Zero-Day    | A vuln that hasn't been patched or publicly disclosed yet                |

> 🧪 **Try This:** Pick `SQLi` or `XSS`, find a simple lab online, and break it. Hands-on cements theory.

---

## 🧃 Slang & Hacker Lingo

| Term          | Meaning                                                      |
| ------------- | ------------------------------------------------------------ |
| Pwned         | Fully compromised (you got access)                           |
| Drop a shell  | Gained remote access on a box                                |
| Script kiddie | Uses tools without understanding them (not a compliment)     |
| Box           | A target machine, usually in a CTF or network                |
| Juice         | Sensitive items like creds, tokens, or secrets               |
| Burned        | A technique/tool that’s no longer stealthy or useful         |
| Foothold      | The initial access you get before escalating privileges      |
| Loot          | Any data you grab – creds, files, hashes, flags              |
| Box is cooked | It’s done; someone already pwned it                          |
| C2            | Command and Control – how attackers talk to infected systems |

> 🧃 **Pro Tip:** You don’t need to use slang to be effective. Clarity > coolness.

---

## 💬 Friendly Advice for New Folks

* Ask questions—people like helping if you show you care.
* Don’t memorize tools—learn what problems they solve.
* If it’s confusing, step away and revisit later—breakthroughs happen on second look.
* Break stuff in VM labs, not in production networks.
* Read writeups, then try similar challenges without peeking.
* Not knowing something doesn’t make you bad at this. Quitting does.

> 🧠 **Reminder:** Learning isn’t linear. Expect loops, pauses, and sudden insights.

---

## 🔐 Important Mindsets

* **Curiosity beats credentials.** Everyone starts somewhere.
* **Learn the layers.** IP → services → files → users → apps → code.
* **Noise ≠ signal.** Tools spit output; you filter what matters.
* **Don’t copy/paste blindly.** Pause and ask “what does this do?”
* **Think like an attacker.** How could you break or bypass this?

> 🧷 **Last Note:** Celebrate small wins. Document them in a journal or repo.

---

## 🛠 Tools & Setup

| Tool       | Purpose                                           |
| ---------- | ------------------------------------------------- |
| Terminal   | Your command center—aliases and scripts save time |
| Nmap       | Port scanning, host discovery                     |
| Wireshark  | Packet capture and analysis                       |
| Burp Suite | Web proxy, repeater, intruder for web tests       |
| Gobuster   | Directory/host brute-forcing                      |
| FFUF       | Flexible web fuzzing                              |
| Ghidra/IDA | Reverse engineering binaries                      |
| Metasploit | Exploit framework                                 |
| VSCode/IDE | Note-taking, script editing                       |
| VirtualBox | Safe VM environment for testing                   |

> 🛠️ **Setup Tip:** Create aliases for your most-used commands. It saves minutes every day.

---

## 📚 Learning Resources

| Resource        | URL                                                                              |
| --------------- | -------------------------------------------------------------------------------- |
| TryHackMe       | [https://tryhackme.com](https://tryhackme.com)                                   |
| Hack The Box    | [https://hackthebox.com](https://hackthebox.com)                                 |
| OverTheWire     | [https://overthewire.org](https://overthewire.org)                               |
| VulnHub         | [https://vulnhub.com](https://vulnhub.com)                                       |
| OWASP Top 10    | [https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/) |
| CTFTime         | [https://ctftime.org](https://ctftime.org)                                       |
| Pentest Academy | [https://pentesteracademy.com](https://pentesteracademy.com)                     |

> 📖 **Advice:** Pick one site and solve one challenge a week—consistency beats intensity.

---

## 🎯 CTF Categories

| Category     | What It Teaches                           |
| ------------ | ----------------------------------------- |
| Web          | HTTP, inputs, auth, directories           |
| Pwn (Binary) | Memory, stack, heap, exploits             |
| Crypto       | Encryption, hashes, math                  |
| Forensics    | Logs, memory dumps, disk images           |
| OSINT        | Public data gathering, social engineering |
| Misc         | Steganography, hardware, trivia           |

> 🎯 **Challenge:** Try one challenge from each category over the next month.

---

## 🔄 Responsible Practice

* Always get permission before scanning or testing.
* Use lab environments like VMs or containers.
* Respect scope and local laws—unauthorized access is illegal.
* Share findings responsibly via disclosure channels.

> ⚖️ **Ethics Reminder:** The same skills that secure can also destroy. Choose wisely.

---

## 🌱 Next Steps & Growth

* Join Discord/Slack communities (LIKE OURS!) and ask questions.
* Write your own CTF writeups or blog posts.
* Contribute to open-source security tools.
* Pair-program or study with peers.
* Keep a learning journal—patterns emerge over time.

> 🚀 **Growth Hack:** Schedule 15 minutes daily to learn a new concept or tool.

---

**WRAVEN Reminder:** Everyone starts somewhere. If you're reading this, you’re already ahead of the people who never tried. Keep asking, breaking, and sharing.

**Repo:** [github.com/WRAVENproject/field-ops-docs](https://github.com/WRAVENproject/field-ops-docs)

---

**Made for the field. Built by WRAVEN.**
