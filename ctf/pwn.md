# Pwning & Binary Exploitation Cheat Sheet (WRAVEN Edition)

**Last updated: July 26, 2025**
**Maintained by: WRAVEN Threat Research Team**

> Pwn challenges test your ability to corrupt memory and hijack control flow. This sheet covers key concepts, protections, tools, and workflows for CTF-level binary exploitation.

---

## 🧠 What Is Pwn?

Binary exploitation (pwn) is about finding and using memory bugs to run code or leak data:

* Overwriting return addresses
* Hijacking function pointers
* Manipulating heap metadata

> 🔍 **Tip:** Always start by understanding how the program reads, writes, and executes memory.

---

## 🗄 Memory Corruption Basics

| Concept        | Description                                         |
| -------------- | --------------------------------------------------- |
| Stack Overflow | Overflow a buffer to overwrite saved RIP, saved RBP |
| Heap Overflow  | Corrupt heap chunks to control malloc/free          |
| Off-by-One     | Single-byte overflow can still break boundaries     |
| Endianness     | Little vs big endian—how bytes are ordered          |

> 🧩 **Advice:** Sketch out the stack layout (return address, saved registers, local variables) before building your payload.

---

## 🔒 Common Protections

| Protection   | Mitigation                               |
| ------------ | ---------------------------------------- |
| NX / DEP     | No execute on writable pages             |
| ASLR         | Randomize addresses of libs, stack, heap |
| Stack Canary | Detect stack buffer overflows            |
| PIE          | Position Independent Executable          |
| RELRO        | Read-Only relocations (partial/full)     |

> 🔐 **Bypass Tip:** Leak a libc or stack address to defeat ASLR; brute canaries one byte at a time; use ret2libc or ROP for NX.

---

## 🔨 Exploitation Techniques

| Technique                         | Description                                        |
| --------------------------------- | -------------------------------------------------- |
| ret2libc                          | Redirect execution to libc functions               |
| ROP (Return Oriented Programming) | Chain small instruction gadgets to build logic     |
| Format String                     | Exploit `%n` specifiers to write arbitrary data    |
| Heap Exploits                     | Tcache poisoning, house of spirit, fastbin dup     |
| GOT Overwrite                     | Overwrite Global Offset Table entry for code reuse |

> 🕹 **Strategy:** Combine primitives—leak → calculate offsets → pivot stack → execute system('/bin/sh').

---

## 🛠 Tools & Commands

| Tool              | Usage Example                             |
| ----------------- | ----------------------------------------- |
| `checksec.sh`     | `checksec --file=binary`                  |
| `readelf`         | `readelf -a binary`                       |
| `objdump`         | `objdump -d binary`                       |
| GDB + pwndbg      | `gdb binary`                              |
| ROPgadget         | `ROPgadget --binary binary`               |
| Ropper            | `ropper --file binary --search 'pop rdi'` |
| Pwntools (Python) | `from pwn import *`                       |
| `strace`/`ltrace` | Trace syscalls or library calls           |

> ⚙️ **Setup Tip:** Write a Python exploit template with pwntools, load context.arch and context.binary for quick launches.

---

## 📝 Pwn Workflow

1. **Recon:** `file`, `checksec`, `strings`, `objdump -d`
2. **Map Functions:** Identify `main`, `vuln`, `printf`, `system`
3. **Leak Info:** Find format string or overflow to leak addresses
4. **Bypass Protections:** brute-canary, leak ASLR, disable NX via ROP
5. **Craft Payload:** Build ROP chain or ret2libc call
6. **Test & Iterate:** Send payload, debug in GDB, adjust offsets
7. **Polish:** Automate with script, handle edge cases, clean output

> 🚀 **Advice:** Automate “leak then exploit” loops. Save time on repetitive debugging.

---

## 📚 Practice & Resources

| Resource       | Link                                                                       |
| -------------- | -------------------------------------------------------------------------- |
| ROP Emporium   | [https://ropemporium.com](https://ropemporium.com)                         |
| Protostar      | [https://exploit.education/protostar](https://exploit.education/protostar) |
| pwnable.kr     | [http://pwnable.kr/](http://pwnable.kr/)                                   |
| pwnable.tw     | [https://pwnable.tw/](https://pwnable.tw/)                                 |
| pwntools docs  | [https://docs.pwntools.com/](https://docs.pwntools.com/)                   |

> 💡 **Pro Tip:** Solve one challenge per resource weekly to build muscle memory.

---

**WRAVEN Reminder:** Pwning is puzzle-solving with low-level hacks. Patience and incremental steps win.

**Repo:** [github.com/WRAVENproject/field-ops-docs](https://github.com/WRAVENproject/field-ops-docs)

---

**Made for the field. Built by WRAVEN.**
