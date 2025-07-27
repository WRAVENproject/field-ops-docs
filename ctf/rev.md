# Reverse Engineering Cheat Sheet (WRAVEN Edition)

**Last updated: July 26, 2025**
**Maintained by: WRAVEN Threat Research Team**

> Reverse engineering (RE) is peeling back compiled code to understand logic, find vulnerabilities, or extract hidden data. This sheet covers static & dynamic techniques, tools, and workflows for CTFs and real-world binaries.

---

## 🔍 What Is Reverse Engineering?

* **Static Analysis:** Inspect code without running it (disassembly, decompilation).
* **Dynamic Analysis:** Run the program under observation (debugging, tracing).
* **Goal:** Understand program behavior, patch, or extract secrets.

> 📝 **Tip:** Always start with static analysis to get the lay of the land before firing up a debugger.

---

## 📁 Common File Formats

| Format    | Extension      | Notes                                        |
| --------- | -------------- | -------------------------------------------- |
| ELF       | `.elf`, no ext | Linux binaries                               |
| PE        | `.exe`, `.dll` | Windows binaries                             |
| Mach-O    | no ext         | macOS / iOS binaries                         |
| Shellcode | no ext         | Raw bytes in `.bin` or extracted from memory |

> 📂 **Advice:** Identify format with `file binary`, then choose appropriate loader in your RE tool.

---

## 🛠 Static Analysis Tools

| Tool     | Use Case                                 |
| -------- | ---------------------------------------- |
| Ghidra   | Free decompiler & disassembler           |
| IDA Free | Interactive disassembler                 |
| radare2  | CLI-based reverse framework              |
| objdump  | Quick disassembly (`objdump -d binary`)  |
| strings  | Find ASCII/Unicode strings in binary     |
| readelf  | Inspect ELF headers (`readelf -h -S -s`) |
| hexdump  | View raw bytes (`hexdump -C binary`)     |
| binwalk  | Extract embedded files or firmware       |

> ⚙️ **Setup:** Load symbols if available (`-s`), and import into Ghidra/IDA for navigation.

---

## ⚙️ Dynamic Analysis Tools

| Tool            | Use Case                            |
| --------------- | ----------------------------------- |
| GDB / PEDA      | Linux debugger with extensions      |
| WinDbg          | Windows debugger                    |
| ltrace / strace | Trace library or system calls       |
| Frida           | Dynamic instrumentation for scripts |
| pwndbg          | GDB plugin for exploits             |
| QEMU / Unicorn  | Emulate CPU for scripting           |
| PIN / DynamoRIO | Binary instrumentation frameworks   |

> 🐞 **Tip:** Use `break main` then step through functions. Inspect registers and memory with `x/20x $rsp`.

---

## 🧩 Key Static Analysis Steps

1. **Strings & symbols:** `strings binary | less`
2. **Imports & exports:** `ldd binary`, `objdump -R binary`
3. **Disassemble:** Ghidra/IDA loader or `objdump -d`
4. **Identify functions:** Look for `main`, `auth`, `check_flag`
5. **Set breakpoints:** Note interesting offsets for dynamic analysis

> 🔎 **Strategy:** Map out code flow: startup, input handling, validation, flag check.

---

## 🕵️‍♀️ Key Dynamic Analysis Steps

1. **Run under debugger:** `gdb -q binary`
2. **Attach to process:** `attach <pid>`
3. **Step instruction:** `stepi` or `si`
4. **Dump memory region:** `dump memory mem.bin addr addr+size`
5. **Trace syscalls:** `strace -f -e open,read,write ./binary`

> 🕵️ **Advice:** Use conditional breakpoints: `break *0x401000 if rax==0xdeadbeef`.

---

## 🔓 Common Patterns & Techniques

| Technique         | Description                                   |
| ----------------- | --------------------------------------------- |
| XOR decoding      | Byte-wise XOR loops; search constants in code |
| Base64 in code    | `AES`, `import base64` patterns               |
| Key/IV hardcoded  | Look for `0x` hex arrays or ASCII keys        |
| Anti-debug tricks | Check for `ptrace`, timing loops              |
| Function hooking  | Intercept calls with Frida for live patching  |

> 🔧 **Pro Tip:** Grep for `xor`, `base64`, `malloc`, `strcmp` to find crypto or checks.

---

## 📦 Automating with Scripts

* **r2pipe / python:** Control radare2 from scripts to batch analyze binaries.
* **angr:** Symbolic execution for path exploration.
* **Capstone / Keystone:** Disassembly and assembly libraries.

> 🖥️ **Workflow:** Automate repetitive tasks (string extraction, function listing) so you can focus on logic.

---

## 🧠 RE Workflow Summary

1. Identify format & gather metadata
2. Extract strings & basic analysis
3. Load into decompiler & explore functions
4. Mark critical code paths & annotate
5. Debug key functions dynamically
6. Extract or patch logic for flags/secrets
7. Clean up notes & write a brief report

> 🗒️ **Reminder:** Document your steps with screenshots or scripts—it helps when challenges get complex.

---

## 🔧 Recommended Practice

* Start with small binaries (< 100 KB) before tackling large CTF pwns.
* Practice reversing obfuscated code (e.g., packers, UPX).
* Participate in RE-focused CTFs and real malware bookmarks.

> 🚀 **Challenge:** Pick an open-source binary, compile with symbols stripped, and try to recover function names.

---

**WRAVEN Reminder:** Reverse engineering is detective work. Patience, note-taking, and tool mastery pay off.

**Repo:** [github.com/WRAVENproject/field-ops-docs](https://github.com/WRAVENproject/field-ops-docs)

---

**Made for the field. Built by WRAVEN.**
