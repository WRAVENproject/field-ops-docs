# CTF Crypto Cheat Sheet (WRAVEN Edition)

**Last updated: July 26, 2025**
**Maintained by: WRAVEN Threat Research Team**

> Crypto challenges turn encryption, encoding, and hashing into puzzles. This sheet focuses on practical attacks, tools, and quick references—no deep proofs, just the moves you need in a CTF or practice lab.

---

## 🛠 What Are Crypto Challenges?

Crypto challenges test your ability to transform or break data:

* **Decryption puzzles:** Given ciphertext and algorithm hints, recover plaintext.
* **Encoding layers:** Multiple encodings stacked (`base64`→`hex`→`rot13`).
* **Hash reversing:** Find inputs matching a given hash via brute force or lookup.
* **Algorithm flaws:** Exploit small keys, reused parameters, or weak implementations.

> 🎯 **Tip:** Always identify if the challenge is encoding, hashing, or encryption first. That narrows the tools you need.

---

## 📖 Crypto Basics

| Term              | Meaning                                                                         |
| ----------------- | ------------------------------------------------------------------------------- |
| Symmetric Crypto  | Same key used to encrypt and decrypt (e.g., AES, DES)                           |
| Asymmetric Crypto | Public/private key pairs for encryption and digital signatures (e.g., RSA, ECC) |
| Hashing           | One-way function producing fixed-size output (e.g., SHA-256)                    |
| Ciphertext        | Encrypted data                                                                  |
| Plaintext         | Original readable data                                                          |
| IV (Nonce)        | Initialization Vector or random number for block/stream ciphers                 |

> 📒 **Reminder:** Encryption ≠ hashing. Encryption is reversible (with key); hashing isn't.

---

## 🔐 RSA Overview

RSA is the most common asymmetric algorithm in CTFs.

| Variable  | Meaning                       |
| --------- | ----------------------------- |
| `p`, `q`  | Two large primes              |
| `n = p*q` | RSA modulus                   |
| `e`       | Public exponent (often 65537) |
| `d`       | Private exponent (secret)     |
| `c`       | Ciphertext                    |
| `m`       | Plaintext (message)           |

> 🔍 **Advice:** If you see `n`, `e`, `c`, start by checking small `e` attacks or feeding to `RsaCtfTool`.

---

## 🔐 Common Ciphers & Scripts

### Caesar / Shift Cipher

```bash
# ROT13 example
echo "uryyb" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

### Vigenère Cipher

```bash
# Use hashlib and frequency analysis or dcode.fr online tool
decode_vigenere ciphertext key_length
```

### XOR Cipher (Single-byte)

```python
ct = bytes.fromhex("3a0c070e")
for key in range(256): print(bytes([b^key for b in ct]))
```

> 🛠 **Tool:** CyberChef for quick XOR, Caesar, and Vigenère operations.

---

## ✍️ Encodings & Transforms

| Encoding   | Decode Command / Tool                                                   |             |
| ---------- | ----------------------------------------------------------------------- | ----------- |
| Base64     | \`echo \$enc                                                            | base64 -d\` |
| Hex        | \`echo \$hex                                                            | xxd -r -p\` |
| URL Encode | `python3 -c "import urllib.parse; print(urllib.parse.unquote('$enc'))"` |             |
| ROT13      | `tr 'A-Za-z' 'N-ZA-Mn-za-m'`                                            |             |
| ASCII85    | CyberChef or `openssl base64 -d -a -A`                                  |             |

> 🔧 **Shortcut:** Drop text into CyberChef’s “Magic” and let it guess layers.

---

## 🗝️ Hash Identification & Cracking

| Hash Type | Length   | Tool / Tip                  |
| --------- | -------- | --------------------------- |
| MD5       | 32 hex   | `hashid`, `hashcat -m 0`    |
| SHA-1     | 40 hex   | `hashid`, `hashcat -m 100`  |
| SHA-256   | 64 hex   | `hashid`, `hashcat -m 1400` |
| bcrypt    | 60 chars | `john --format=bcrypt`      |

> ⚡ **Tip:** Use `hashid` or CyberChef to identify hash type before cracking.

---

## 🔎 RSA Attacks & Tools

| Attack         | When It Works                                 | Tool / Script                  |
| -------------- | --------------------------------------------- | ------------------------------ |
| Wiener's       | Small `d`                                     | `rsatool`, `wiener.py`         |
| Common Modulus | Same `n`, different `e`                       | `common_modulus.py`            |
| Broadcast      | Same message encrypted to multiple recipients | `CryptoSocket` techniques      |
| Factoring      | Small or weak primes                          | `yafu`, `msieve`, `RsaCtfTool` |

> 🔍 **Workflow:** Feed `(n,e,c)` to `RsaCtfTool` before manual scripting.

---

## 🧠 Recommended Tools

| Tool            | Description                                |
| --------------- | ------------------------------------------ |
| CyberChef       | Encodings, XOR, hash ID, and more in a GUI |
| RsaCtfTool      | Automated RSA attacks and analysis         |
| Hashcat         | GPU-accelerated hash cracking              |
| John the Ripper | Wordlist and brute-force cracking          |
| dcode.fr        | Browser-based cipher solvers               |
| Python & Sage   | Custom scripts and math libraries          |

> 🛠 **Setup:** Install `pip install rsa ctftools hashcat john` or use your distro’s packages.

---

## 🧪 Quick Tips & Strategy

* Check for **multiple layers**: encoding → hashing → encryption.
* Look at length and charset: hex? base64? random bytes?
* Always Google challenge name + `writeup` when stuck.
* Keep small scripts handy: Caesar, XOR, Vigenère, RSA.
* Automate repeats: build a tiny toolkit of common functions.

---

**WRAVEN Reminder:** Crypto is puzzle-solving. Understanding the structure beats brute forcing every time.

**Repo:** [github.com/WRAVENproject/field-ops-docs](https://github.com/WRAVENproject/field-ops-docs)

---

**Made for the field. Built by WRAVEN.**
