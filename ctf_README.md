# 🏁 CTF Platforms & Practice Resources

> A practical guide to where you can practice Capture The Flag challenges, what you will encounter in different categories, and which tools are commonly used.

---

## 📁 Table of Contents

* [Beginner-Friendly Platforms](#-beginner-friendly-platforms)
* [Intermediate / Advanced Platforms](#-intermediate--advanced-platforms)
* [Live Competitive CTFs](#-live-competitive-ctfs)
* [CTF Categories & Toolkits](#-ctf-categories--toolkits)
* [Essential CTF Toolbox](#-essential-ctf-toolbox)
* [Writeup Resources](#-writeup-resources)
* [General CTF Strategy](#-general-ctf-strategy)

---

## 🟢 Beginner-Friendly Platforms

If you are new to Capture The Flag competitions, it is better to start with platforms that provide guided challenges and gradually introduce cybersecurity concepts. **TryHackMe** is a good starting point because its rooms provide structured, hands-on learning. **picoCTF**, developed for students, combines learning with practical CTF-style challenges. For Linux fundamentals, **OverTheWire Bandit** is useful because its challenges are completed through the command line and introduce basic Linux concepts. **Hack The Box Starting Point** provides guided introductory machines before moving into the wider HTB environment. If you are particularly interested in cryptography, **CryptoHack** provides gamified challenges that help build cryptography fundamentals. **PWNABLE.kr** can be explored when you are ready to start learning about binary exploitation and low-level security.

| Platform                          | Focus                                                     | Link              |
| --------------------------------- | --------------------------------------------------------- | ----------------- |
| **TryHackMe**                     | Guided rooms and beginner-friendly cybersecurity learning | `tryhackme.com`   |
| **picoCTF**                       | Student-focused CTF challenges                            | `picoctf.org`     |
| **OverTheWire — Bandit**          | Linux command-line fundamentals through SSH               | `overthewire.org` |
| **Hack The Box — Starting Point** | Guided introductory machines                              | `hackthebox.com`  |
| **CryptoHack**                    | Cryptography fundamentals                                 | `cryptohack.org`  |
| **PWNABLE.kr**                    | Binary exploitation fundamentals                          | `pwnable.kr`      |

A simple progression for beginners is to first become comfortable with **Linux and networking**, then move into **web security and basic CTF challenges**. After that, you can explore areas such as cryptography, forensics, reverse engineering, and binary exploitation.

---

## 🟡 Intermediate / Advanced Platforms

Once you are comfortable with the fundamentals, you can move to platforms that provide more realistic or technically challenging environments. **Hack The Box** provides virtual machines and penetration-testing labs, while **VulnHub** allows you to download vulnerable virtual machines and practice locally. For web security, the **PortSwigger Web Security Academy** provides dedicated web application vulnerability labs. **PentesterLab** focuses on structured web and infrastructure security exercises, while **Root-Me** offers challenges across a wide range of cybersecurity categories.

For more structured learning, **Hack The Box Academy** provides learning paths and cybersecurity training. **CTFtime.org** is useful for finding CTF competitions and events taking place around the world. If you want to develop deeper knowledge of binary exploitation and systems security, **pwn.college** provides dedicated learning material and challenges.

| Platform                             | Focus                                            | Link                           |
| ------------------------------------ | ------------------------------------------------ | ------------------------------ |
| **Hack The Box (HTB)**               | VM-based penetration-testing labs and machines   | `hackthebox.com`               |
| **VulnHub**                          | Downloadable vulnerable VMs for offline practice | `vulnhub.com`                  |
| **PortSwigger Web Security Academy** | Web application security labs                    | `portswigger.net/web-security` |
| **PentesterLab**                     | Structured web and infrastructure exercises      | `pentesterlab.com`             |
| **Root-Me**                          | Challenges across multiple security categories   | `root-me.org`                  |
| **Hack The Box Academy**             | Structured learning paths and training           | `academy.hackthebox.com`       |
| **CTFtime.org**                      | CTF competition calendar and events              | `ctftime.org`                  |
| **pwn.college**                      | Binary exploitation and systems security         | `pwn.college`                  |

---

## 🏆 Live Competitive CTFs

CTFs are not limited to practice platforms. There are also live competitions where individuals or teams solve challenges within a specific time period. **CTFtime.org** can be used to track upcoming competitions and find events based on category, difficulty, and date.

Some well-known competitions include **DEF CON CTF, Google CTF, Hack The Box University and Business CTFs, picoCTF, CSAW CTF, and ångstromCTF**.

There are several common competition formats. In a **Jeopardy-style CTF**, participants solve independent challenges and receive points for each successful solution. In an **Attack-Defense CTF**, teams operate and defend their own services while attempting to attack services belonging to other teams. Team-based competitions also allow participants to divide challenges according to their individual areas of expertise.

---

# 🧩 CTF Categories & Toolkits

CTF challenges are divided into different categories. Each category focuses on a particular area of cybersecurity, so the tools and techniques you use will depend on the type of challenge you are solving.

---

## 🌐 Web Exploitation

Web exploitation challenges involve websites and web applications. The goal is usually to understand how the application works and identify a weakness that can lead to the flag.

Common topics include **SQL Injection, Cross-Site Scripting (XSS), Server-Side Template Injection (SSTI), IDOR, JWT manipulation, deserialization, and authentication bypass**.

Common tools include **Burp Suite, ffuf, Gobuster, SQLmap, and browser Developer Tools**. When beginning a web challenge, it is useful to first inspect the application's pages, source code, cookies, HTTP requests, and parameters. Simple locations such as `/robots.txt` and page source can sometimes provide useful clues.

> **Beginner tip:** Understand the application's behavior first. Do not immediately start trying random payloads.

---

## 🔐 Cryptography

Cryptography challenges involve encrypted, encoded, or mathematically transformed information. The challenge may provide a message or value and require you to determine how it was created and recover the original information.

Common topics include **Caesar and Vigenère ciphers, RSA, XOR analysis, and hash length extension**. Some challenges may also involve RSA techniques such as small-`e`, common-modulus, or Wiener's attacks.

Useful tools include **CyberChef, RsaCtfTool, Hashcat, PyCryptodome, and SageMath**.

A good first step is to identify the structure of the data before trying to solve it. CyberChef's **Magic** function can be useful for quickly identifying common encodings and transformations.

> **Beginner tip:** First determine whether the data is encoded, encrypted, hashed, or simply transformed. These are different concepts.

---

## 💣 Binary Exploitation — Pwn

Binary exploitation, often called **Pwn**, focuses on understanding compiled programs and how they handle memory and input. These challenges generally require a stronger understanding of programming, operating systems, memory, and sometimes assembly.

Common topics include **buffer overflows, ROP chains, format-string vulnerabilities, heap exploitation, and shellcoding**.

Tools commonly used in this category include **GDB with pwndbg or GEF, pwntools, Ghidra, and checksec**.

Before analyzing a binary in depth, `checksec` can help identify protections such as **NX, PIE, canaries, and RELRO**. Understanding these protections helps you understand the security configuration of the program.

> **Beginner tip:** Learn basic C, memory concepts, and GDB before attempting advanced Pwn challenges.

---

## 🔬 Reverse Engineering

Reverse engineering involves analyzing a program to understand how it works without relying on its original source code. A CTF challenge may provide an executable and ask you to determine what it does, identify a particular input, or locate the flag.

Common tools include **Ghidra, IDA Free, Binary Ninja, radare2, Cutter, and dnSpy for .NET programs**.

Important concepts include **disassembly, control-flow analysis, anti-debugging, and unpacking**.

A useful starting point is to examine the file using `file` and `strings` before moving into detailed disassembly. This can give you an initial understanding of the program and may reveal useful strings or information.

> **Beginner tip:** You do not need to understand every assembly instruction. Start by identifying the functions and program behavior that matter to the challenge.

---

## 🕵️ Forensics

Forensics challenges involve examining digital evidence to discover useful information. The evidence might be a PCAP file, memory dump, image, document, archive, or another type of digital artifact.

Common tools include **Wireshark, Volatility, Autopsy, binwalk, exiftool, steghide, and zsteg**.

Typical tasks include **PCAP analysis, memory-dump analysis, file carving, steganography, and metadata extraction**.

For example, when given an image, you might first examine its metadata and file structure before checking for strings, embedded content, or unusual data. `binwalk` can also be used in appropriate CTF challenges to identify embedded files.

> **Beginner tip:** Treat the challenge file as evidence. Examine it systematically instead of immediately modifying it.

---

## 🌐 OSINT

**OSINT stands for Open-Source Intelligence.** In CTFs, OSINT challenges require you to find and connect information that is publicly available.

Common techniques include search-engine operators, Shodan, `exiftool`, reverse-image searching, and the Wayback Machine.

Challenges may involve **geolocating photographs, examining metadata, finding information connected to usernames, or connecting information from different public sources**.

The important part of OSINT is not simply finding information. It is determining whether different pieces of information are connected and relevant to the challenge.

> **Beginner tip:** Start with the information provided by the challenge and work outward from there. Keep track of where each piece of information came from.

---

## 🔑 Steganography

Steganography involves hiding information inside another file or medium. In CTFs, you may receive an image, audio file, or other media that appears normal but contains hidden information.

Common tools include **steghide, zsteg, stegsolve, binwalk, and Sonic Visualiser** for audio analysis.

Common techniques include **LSB extraction, hidden-file detection, image analysis, and audio spectrogram analysis**.

When examining a suspicious image, consider its metadata, pixel data, appended content, embedded files, and possible hidden messages.

---

# 🧰 Essential CTF Toolbox

You do not need every security tool available when you begin. It is more useful to understand a small number of tools properly and gradually expand your toolkit.

Kali Linux and Parrot OS provide many tools commonly used for security testing and CTF practice.

```bash
# Web
burpsuite
ffuf
gobuster
sqlmap
nikto
wpscan

# Crypto
CyberChef
RsaCtfTool
openssl
hashcat
john

# Pwn
gdb
pwndbg/gef/peda
pwntools
ropper
one_gadget
checksec

# Reverse Engineering
ghidra
radare2
objdump
strings
ltrace
strace

# Forensics
wireshark
volatility3
binwalk
foremost
exiftool
steghide

# General
python3
nc
curl
jq
CyberChef
```

### Handy CyberChef Techniques

Some common CyberChef operations worth recognizing are **From Base64, From Hex, Magic, and XOR Brute Force**. These are particularly useful when a challenge provides encoded or transformed data.

### Pwntools Quick Template

For authorized CTF challenges, pwntools can be used to automate interaction with a challenge binary.

```python
from pwn import *

context.binary = elf = ELF('./chal')

p = process('./chal')
# or remote('host', port)

p.sendline(b'A' * 72 + p64(0xdeadbeef))

p.interactive()
```

The example demonstrates the basic idea of loading a binary, starting or connecting to it, sending input, and interacting with the process.

> ⚠️ **Use these tools only against CTF targets, intentionally vulnerable systems, or systems where you have explicit authorization.**

---

# 📖 Writeup Resources

CTF writeups are useful when you are unable to solve a challenge or want to understand a technique in more detail. **CTFtime.org** provides information about CTF events and writeups, while communities such as **r/securityCTF** can provide discussions and learning material.

You can also find useful educational content from **LiveOverflow, John Hammond, and IppSec**, particularly for CTF and Hack The Box challenges. GitHub's `ctf-writeups` topic contains community-created solutions, and **CTF Wiki** provides a broader collection of CTF techniques and references.

The best way to use a writeup is to understand the reasoning behind the solution rather than simply copying the commands or final answer.

---

# 🎯 General CTF Strategy

Start by reading the challenge description carefully. Important information such as the flag format, hints, filenames, usernames, versions, and error messages may already be provided.

Before attempting exploitation, **enumerate the challenge** and understand what you have been given. Determine whether you are working with a website, executable, image, PCAP, encrypted text, memory dump, or another type of file.

If you become stuck, avoid repeatedly trying random techniques. Search exact error messages or version strings when research is permitted, and use documentation to understand unfamiliar technologies or tools.

Keep notes for every challenge. Tools such as **Obsidian or CherryTree** can be useful for recording findings, commands, approaches that failed, and the final solution. Over time, these notes become a personal reference for techniques you have already learned.

Try to automate repetitive tasks with small Python scripts when appropriate. CTFs are a good environment for learning how to turn repetitive manual work into simple automation.

For team competitions, divide challenges according to each person's strengths. One person may focus on web challenges while another works on forensics, cryptography, reverse engineering, or Pwn. Sharing findings and failed approaches can save the team considerable time.

Finally, practice consistently. Working through a few challenges every week is generally more useful for learning than trying to complete a large number of challenges immediately before a competition.

---

# 🧠 A Simple CTF Learning Approach

For beginners, a practical progression is:

```text
Linux & Command Line
        ↓
Networking Fundamentals
        ↓
Python Basics
        ↓
Easy CTF Challenges
        ↓
Web / Crypto / Forensics
        ↓
Reverse Engineering
        ↓
Binary Exploitation
        ↓
Live CTF Competitions
```

You do not have to follow this path perfectly. CTFs are meant to be exploratory, and it is completely normal to discover a category that interests you and spend more time on it.

The most important skill is learning how to approach an unfamiliar problem: **read it carefully, gather information, form a reasonable hypothesis, test it, document what you learn, and try again when necessary.**

---

⬅️ **[Back to Main README](../README.md)**
