# Stego & Forensics Cheat Sheet (WRAVEN Edition)

**Last updated: July 26, 2025**
**Maintained by: WRAVEN Threat Research Team**

> Stego and forensics challenges teach you to uncover hidden data and analyze artifacts. This sheet covers common techniques, tools, and quick-start commands for both steganography puzzles and basic digital forensics.

---

## 🕵️‍♂️ What Are Stego Challenges?

Stego (steganography) hides data within other files. In CTFs you might see:

* Images with hidden messages in pixels
* Audio files with embedded data in samples or metadata
* PDFs or documents with concealed content

> 💡 **Tip:** Always check file metadata and view files in a hex editor before assuming it’s only pixel-level stego.

---

## 🎨 Common Steganography Techniques

| Technique       | Description                                    | Detection / Tool               |
| --------------- | ---------------------------------------------- | ------------------------------ |
| LSB (Images)    | Hides data in least significant bits of pixels | `steghide`, `zsteg`, `binwalk` |
| Metadata        | Adds data to EXIF tags or document properties  | `exiftool`, `exiv2`            |
| Echo Hiding     | Embeds data in audio echo patterns             | `audacity`, `steghide`         |
| Null Bytes      | Inserts hidden data appended after EOF marker  | `xxd`, `hd`, manual slicing    |
| Spread Spectrum | Disperses data across audio frequencies        | Specialized scripts            |

> 🔎 **Advice:** Run `exiftool file` and `binwalk file` first—often the stego payload is obvious.

---

## 🛠 Stego Tools & Commands

| Tool       | Usage Example                                 |                |
| ---------- | --------------------------------------------- | -------------- |
| `exiftool` | `exiftool image.jpg`                          |                |
| `binwalk`  | `binwalk -e image.png`                        |                |
| `steghide` | `steghide extract -sf image.jpg -p password`  |                |
| `zsteg`    | `zsteg -a image.png`                          |                |
| `outguess` | `outguess -k pass -r input.png -t secret.txt` |                |
| `strings`  | \`strings file.pdf                            | grep -i flag\` |

> 🛠 **Setup:** Install via your package manager (`apt install steghide binwalk exiftool`).

---

## 🔍 Forensics Basics

Digital forensics covers analyzing data remnants:

* File carving: Recover deleted files from images
* Metadata analysis: Timestamps, users, file origins
* Process/memory: Inspect running state or dumps
* Network: Analyze packet captures for clues

> 🔍 **Reminder:** Duplicate images before you work. Always preserve originals.

---

## 🗂 File System Forensics

| Task                | Command / Tool                                 |
| ------------------- | ---------------------------------------------- |
| File type detection | `file suspicious.bin`                          |
| Strings extraction  | `strings -n 6 suspicious.bin`                  |
| File carving        | `foremost -i disk.img -o output_dir`           |
| Data recovery       | `photorec /d output_dir /cmd disk.img options` |
| Hex inspection      | `hexedit file.bin` or `xxd -g 1 file.bin`      |

> 🗂 **Advice:** Look for odd file headers or JPEG markers in non-image files.

---

## 🧠 Memory & Process Analysis

| Task           | Tool / Command                             |
| -------------- | ------------------------------------------ |
| Memory dump    | `volatility -f mem.dmp imageinfo`          |
| Process list   | `volatility pslist`                        |
| Network creds  | `volatility dumpfiles -Q PID --name *.txt` |
| Kernel modules | `volatility modules`                       |

> 🧐 **Tip:** Identify profile (`imageinfo`) before running other Volatility commands.

---

## 🌐 Network Forensics (PCAP)

| Task              | Command / Tool                                                   |
| ----------------- | ---------------------------------------------------------------- |
| Open pcap         | `wireshark file.pcap` or `tshark -r file.pcap`                   |
| HTTP strings      | `tshark -r file.pcap -Y http -T fields -e http.request.full_uri` |
| Extract files     | `tshark -r file.pcap --export-objects http,./http_objects`       |
| Follow TCP stream | In Wireshark: right-click → Follow → TCP Stream                  |

> 🌐 **Advice:** Filter early: use display filters (`host x.x.x.x`) to reduce noise.

---

## 🔧 Combined Quick Workflow

1. **Identify file type:** `file target`
2. **Check metadata:** `exiftool`, `strings`
3. **Run automated scans:** `binwalk -e`, `volatility imageinfo`
4. **Manual inspection:** Hex editor, image viewers, audio player
5. **Carve and recover:** `foremost`, `photorec`
6. **Analyze output:** Search for `flag`, keywords, patterns

> 🚀 **Workflow Tip:** Automate step 3 with a shell script to save time on every challenge.

---

**WRAVEN Reminder:** Forensics is detective work. Patience and methodical steps win over wild guessing.

**Repo:** [github.com/WRAVENproject/field-ops-docs](https://github.com/WRAVENproject/field-ops-docs)

---

**Made for the field. Built by WRAVEN.**
