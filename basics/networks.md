# Basic Networking & Protocols (WRAVEN Edition)

**Last updated: July 26, 2025**
**Maintained by: WRAVEN Threat Research Team**

> For when you're in the field and need to remember how the internet actually works. Covers the essentials: IPs, ports, protocols, and how stuff connects.

---

## 🧠 IP, DNS, and Subnets

### 🔹 IP Address Basics

| Term           | Example                                         | Description                       |
| -------------- | ----------------------------------------------- | --------------------------------- |
| IPv4           | `192.168.1.10`                                  | 32-bit address (4 octets)         |
| IPv6           | `2001:0db8:85a3::8a2e:0370:7334`                | 128-bit address                   |
| Private ranges | `192.168.0.0/16`, `10.0.0.0/8`, `172.16.0.0/12` | Used in LANs, not routable online |

### 🔹 CIDR / Subnet Mask

| CIDR  | Netmask           | Hosts         |
| ----- | ----------------- | ------------- |
| `/24` | `255.255.255.0`   | 254 usable    |
| `/16` | `255.255.0.0`     | 65,534 usable |
| `/32` | `255.255.255.255` | Single host   |

### 🔹 DNS Terms

| Record | Purpose                  | Example                        |
| ------ | ------------------------ | ------------------------------ |
| A      | Maps name to IPv4        | `example.com -> 93.184.216.34` |
| AAAA   | Maps name to IPv6        | `example.com -> ::1`           |
| CNAME  | Alias to another name    | `www -> example.com`           |
| MX     | Mail server              | `mail.example.com`             |
| NS     | Authoritative nameserver | `ns1.example.com`              |

### 🔹 Handy DNS Tools

```bash
dig A example.com
nslookup example.com
dnsrecon -d example.com
gobuster dns -d example.com -w subdomains.txt
```

---

## 🌐 TCP, UDP, and ICMP

### 🔸 TCP (Transmission Control Protocol)

* Reliable, connection-based
* 3-way handshake: SYN → SYN/ACK → ACK
* Example services: HTTP, HTTPS, SSH, FTP

### 🔸 UDP (User Datagram Protocol)

* Unreliable, no handshake
* Faster but no guarantees
* Example services: DNS, SNMP, TFTP

### 🔸 ICMP (Internet Control Message Protocol)

* Used for ping, traceroute, etc.
* Doesn't use ports

### 🔹 Common Ports

| Port | Protocol | Service  |
| ---- | -------- | -------- |
| 22   | TCP      | SSH      |
| 53   | UDP/TCP  | DNS      |
| 80   | TCP      | HTTP     |
| 443  | TCP      | HTTPS    |
| 139  | TCP      | NetBIOS  |
| 445  | TCP      | SMB      |
| 3389 | TCP      | RDP      |
| 3306 | TCP      | MySQL    |
| 8080 | TCP      | Alt HTTP |

---

## 📡 HTTP Request Anatomy

```http
GET /index.html HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Accept: */*
```

### 🔹 Curl Reference

```bash
curl http://example.com
curl -X POST -d "user=admin" http://example.com/login
curl -I http://example.com  # HEAD request
```

---

## 🔍 Wireshark Filters (Quick Hits)

| Filter                          | Purpose                |
| ------------------------------- | ---------------------- |
| `ip.addr == 192.168.1.5`        | Match IP               |
| `tcp.port == 80`                | Match port             |
| `http.request`                  | Show HTTP requests     |
| `dns.qry.name == "example.com"` | Match DNS query        |
| `icmp`                          | Show ping/ICMP traffic |

---

## ⚙️ Useful Tools

| Tool             | Use                        |
| ---------------- | -------------------------- |
| `ping`           | Check host is up           |
| `traceroute`     | Show path to host          |
| `netstat -tulnp` | Show listening services    |
| `ss -antp`       | Faster netstat replacement |
| `tcpdump`        | Capture packets from CLI   |
| `wireshark`      | GUI packet analyzer        |

---

**WRAVEN Note:** Know your packets. Understanding how data moves is more useful than memorizing tools. This sheet gives you the fundamentals.

**Repo:** [github.com/WRAVENproject/field-ops-docs](https://github.com/WRAVENproject/field-ops-docs)

---

Made for the field. Built by WRAVEN.
