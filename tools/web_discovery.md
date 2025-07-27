# Gobuster, FFUF, & Web Discovery (WRAVEN Edition)
**Last updated: July 26, 2025**  
**Maintained by: WRAVEN Threat Research Team**

> This cheat sheet covers tools for brute-force web discovery—finding hidden directories, subdomains, virtual hosts, and weird endpoints. Designed for CTFs, pentests, and real recon work.

---

## 🧰 What These Tools Do

These tools are used to find things the site owner didn’t mean to leave exposed. Think:
- Admin panels
- Old backups
- Hidden APIs
- Staging servers
- Subdomains from devs who forgot to lock stuff down

You give the tool a wordlist, and it checks each word as a URL, folder, or subdomain. It’s like guessing all the keys to a door until one turns.

---

## 🚪 Gobuster

**Gobuster** is a CLI tool written in Go. It brute-forces:
- Directories (`dir`)
- DNS subdomains (`dns`)
- VHosts (`vhost`)
- S3 buckets (`s3`)

### 🔹 Directory Bruteforce (dir mode)

```bash
gobuster dir -u http://target -w wordlist.txt -x php,txt -t 50
```
Flag	Meaning
-u	Target URL
-w	Wordlist
-x	Extensions to try (e.g., .php, .txt)
-t	Threads (higher = faster, noisier)

Example: Find hidden files or admin panels like /admin.php, /backup.zip, /hidden/

---

### 🔹 DNS Subdomain Bruteforce
```
gobuster dns -d target.com -w subdomains.txt
```
Flag	Meaning
-d	Domain name to attack
-w	Wordlist of possible subdomains

Example: Discover dev.target.com, api.target.com, etc.

---

### 🔹 VHost Discovery (virtual hosts)
```
gobuster vhost -u http://target -w vhosts.txt -t 50
```
Use when the IP points to multiple sites via host headers (common in shared hosting). Works best with an IP or wildcard DNS.

---

### 🔹 Output Tip
```
gobuster ... -o results.txt
```
Saves your scan output. Combine with grep, cut, or just eyeball it later.

---

### FFUF (Fuzz Faster U Fool)

FFUF is a flexible, blazing fast web fuzzer written in Go. It supports:
	•	URL fuzzing
	•	Parameter fuzzing
	•	Header fuzzing
	•	Subdomain fuzzing (with a helper tool)

### 🔹 Basic Directory Fuzz
```
ffuf -u http://target/FUZZ -w wordlist.txt -e .php,.bak -t 50
```
Flag	Meaning
-u	URL, replace FUZZ with injection point
-w	Wordlist
-e	Extensions to try
-t	Threads


---

### 🔹 Filter Output
```
ffuf -fc 404      # Hide 404s
ffuf -fs 1234     # Filter by response size
ffuf -fw 256      # Filter by word count
```

---

### 🔹 Parameter Fuzzing
```
ffuf -u http://target/page.php?FUZZ=value -w params.txt
```
Find hidden GET parameters like debug=1, test=true, etc.

---

### 🔹 POST Fuzzing
```
ffuf -X POST -d "username=admin&password=FUZZ" -u http://target/login.php -w rockyou.txt
```
Good for login brute-force testing. Make sure you’re allowed to do this.

---

### 🔹 Header Fuzzing
```
ffuf -u http://target -w headers.txt -H "X-FUZZ: test"
```
Fuzz HTTP headers like X-Forwarded-For, X-Original-URL, etc.

---

### 🧾 Wordlists to Use

Tool	Location
Common lists	/usr/share/wordlists/
SecLists	https://github.com/danielmiessler/SecLists
Quickstart	dirbuster/directory-list-2.3-small.txt

Always check what the target responds with by default, so you can exclude false positives.

---

### 🧪 Tips & Tricks
	•	Use -x or -e to catch .php, .bak, .old, .zip, etc.
	•	Always check response size and status code.
	•	Test with and without trailing slashes.
	•	Use Burp to confirm what FFUF or Gobuster finds.
	•	Use DNS tools (dig, amass, dnsenum) alongside Gobuster DNS mode.

---

### 🧠 When to Use What

Goal	Use
Find hidden folders	gobuster dir / ffuf -u http://site/FUZZ
Find subdomains	gobuster dns + amass
Brute-force login	ffuf with POST data
Fuzz API params	ffuf with FUZZ in param
Test virtual hosts	gobuster vhost


---

WRAVEN Reminder: These tools are loud. Don’t just blast them at a production box. Understand the context, and always get permission.

Repo: github.com/WRAVENproject/field-ops-docs

---

Made for the field. Built by WRAVEN.
