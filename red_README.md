# 🔴 Red Teaming — Offensive Security Playbook

> **Methodology, tooling, and technique reference mapped loosely to common red-team and MITRE ATT&CK concepts. Intended only for authorized penetration tests, red-team engagements, CTFs, and controlled lab environments.**

---

## ⚠️ Scope & Ethics

Red teaming involves simulating realistic attacks to understand how well an organization can prevent, detect, and respond to threats. Every activity in this guide should be performed only against systems you own or systems for which you have explicit authorization. A properly defined scope and **Rules of Engagement (RoE)** should clearly identify the permitted targets, techniques, testing windows, and limitations. Unauthorized access, credential attacks, persistence, or exploitation can be illegal and can cause real-world damage.

---

## 📁 Table of Contents

* [Methodology Overview](#-methodology-overview)
* [Reconnaissance (OSINT)](#-reconnaissance-osint)
* [Scanning & Enumeration](#-scanning--enumeration)
* [Web Application Attacks](#-web-application-attacks)
* [Exploitation Frameworks](#-exploitation-frameworks)
* [Initial Access Techniques](#-initial-access-techniques)
* [Privilege Escalation](#-privilege-escalation)
* [Lateral Movement](#-lateral-movement)
* [Persistence](#-persistence)
* [Command & Control (C2)](#-command--control-c2)
* [Active Directory Attacks](#-active-directory-attacks)
* [Password Attacks](#-password-attacks)
* [Wireless Attacks](#-wireless-attacks)
* [Social Engineering](#-social-engineering)
* [Reporting](#-reporting)

---

## 🧭 Methodology Overview

A red-team engagement normally follows a structured process rather than immediately attempting exploitation. The tester begins with reconnaissance to understand the target environment, followed by scanning and enumeration to identify accessible services and potential weaknesses. If an authorized path to initial access is identified, the engagement may proceed toward privilege escalation and controlled lateral movement. Persistence and command-and-control concepts can then be evaluated where explicitly permitted. Finally, the activity is documented and reported so the organization can improve its defenses.

```text
1. Reconnaissance        → Passive / active information gathering
2. Scanning              → Port, service, and vulnerability discovery
3. Gaining Access        → Exploitation and initial foothold
4. Maintaining Access    → Persistence and controlled access
5. Privilege Escalation  → Local admin/root or domain-level access
6. Lateral Movement      → Controlled movement across the network
7. Covering Tracks       → Log and artifact considerations
8. Reporting             → Findings, risk, evidence, remediation
```

Common frameworks and references include **PTES**, **OSSTMM**, **MITRE ATT&CK**, and the **Cyber Kill Chain**. These provide different ways of organizing and describing offensive-security activity.

---

## 🔍 Reconnaissance (OSINT)

Reconnaissance is the information-gathering stage. The objective is to understand the target's publicly exposed presence before moving into more active testing. OSINT can reveal domains, subdomains, employee information, technologies, historical URLs, certificates, and other information that may help define the attack surface.

| Tool / Technique                  | Purpose                                                  |
| --------------------------------- | -------------------------------------------------------- |
| `theHarvester`                    | Collect publicly available emails, hosts, and subdomains |
| **Shodan / Censys**               | Search publicly exposed devices and services             |
| `whois`                           | Obtain domain registration information                   |
| **Maltego**                       | Visualize relationships between OSINT entities           |
| **Recon-ng**                      | Modular reconnaissance framework                         |
| **SpiderFoot**                    | Automated OSINT aggregation                              |
| **Sublist3r / Amass**             | Subdomain enumeration                                    |
| **crt.sh**                        | Search certificate-transparency records                  |
| **Google Dorking**                | Search for publicly indexed information                  |
| **LinkedIn / Hunter.io**          | Research public employee and email information           |
| **Wayback Machine / waybackurls** | Examine historical URLs and web content                  |

A simple example of reconnaissance is identifying certificate records for a domain and comparing them with publicly known subdomains. This can help build an initial understanding of the organization's external attack surface without directly exploiting anything.

---

## 📡 Scanning & Enumeration

Once the scope is understood, scanning and enumeration help identify accessible services and technologies. Tools such as **Nmap**, **Gobuster**, **ffuf**, **WhatWeb**, **Nikto**, **WPScan**, **enum4linux**, and **smbclient** can be used in authorized environments to understand exposed services.

```bash
# Nmap full sweep
nmap -sC -sV -O -p- -T4 target -oA fullscan

# Service-specific enumeration
enum4linux -a target
smbclient -L //target -N
showmount -e target
snmpwalk -c public -v1 target

# Web reconnaissance
gobuster dir -u http://target -w wordlist.txt -x php,html
ffuf -w wordlist.txt -u http://target/FUZZ
whatweb target
nikto -h target
wpscan --url target --enumerate p,t,u
```

Nmap's scripting engine can also provide additional enumeration capabilities:

```text
--script vuln
--script smb-enum-shares
--script http-enum
--script ssl-enum-ciphers
```

For beginners, the important concept is to understand **what each scan is trying to discover** rather than simply memorizing commands. Port scanning identifies reachable services, service detection identifies technologies and versions, and application enumeration attempts to identify accessible functionality.

---

## 🌐 Web Application Attacks

Web application testing focuses on identifying weaknesses in how an application handles requests, authentication, authorization, input, files, sessions, and backend processing. Tools such as **Burp Suite** and **OWASP ZAP** are commonly used to intercept and inspect HTTP requests during authorized testing.

| Category              | What to Understand                                                       |
| --------------------- | ------------------------------------------------------------------------ |
| **SQL Injection**     | Testing whether user input can alter database queries                    |
| **XSS**               | Testing whether untrusted input can execute in a user's browser          |
| **CSRF**              | Examining whether unauthorized actions can be triggered through requests |
| **SSRF**              | Testing whether server-side requests can reach unintended resources      |
| **XXE**               | Examining unsafe XML entity processing                                   |
| **IDOR**              | Testing authorization around object or resource identifiers              |
| **File Upload**       | Checking whether uploaded files are properly validated                   |
| **LFI / RFI**         | Testing unsafe file inclusion behavior                                   |
| **Command Injection** | Determining whether input reaches operating-system commands              |
| **Deserialization**   | Examining unsafe processing of serialized objects                        |
| **Fuzzing**           | Discovering unexpected parameters, endpoints, or application behavior    |

Tools such as **Wfuzz** and **ffuf** can assist with parameter and endpoint discovery, while the **OWASP Top 10** provides a useful reference for common categories of web application security risks.

---

## 💣 Exploitation Frameworks

Exploitation frameworks provide organized environments for security testing. **Metasploit** is widely used for studying and validating known vulnerabilities in controlled environments. Other platforms such as **Cobalt Strike**, **Sliver**, **Havoc**, and **Mythic** are associated with red-team and command-and-control activities, while **Searchsploit** can be used to search locally available Exploit-DB information.

```text
Metasploit       → Exploitation framework
Cobalt Strike    → Commercial red-team platform
Sliver / Havoc   → Open-source C2 frameworks
Searchsploit     → Local exploit research
Msfvenom         → Payload generation
```

A basic Metasploit workflow involves selecting an appropriate module, configuring the authorized target and required options, and executing the module within the defined engagement scope.

---

## 🚪 Initial Access Techniques

Initial access refers to obtaining the first authorized foothold into a target environment. Common scenarios studied during red-team exercises include phishing simulations, exploitation of vulnerable public-facing services, weak or default credentials, malicious USB simulations, supply-chain trust relationships, and cloud-storage misconfigurations.

The purpose of studying these techniques in a red-team engagement is not simply to obtain access, but to demonstrate how an attacker could potentially enter an environment and how defenders could detect and prevent that activity.

---

## ⬆️ Privilege Escalation

Privilege escalation occurs when an attacker moves from a lower-privileged account to a more privileged level, such as local administrator or root. The investigation normally begins with enumeration of operating-system configuration, users, permissions, services, scheduled tasks, credentials, and security controls.

Common enumeration tools include:

* **LinPEAS**
* **WinPEAS**
* **Linux Exploit Suggester**
* **PowerUp**
* **Seatbelt**

For Linux-focused enumeration, the dedicated Linux command reference can be used alongside the privilege-escalation section. Windows environments can similarly be examined using Windows privilege-escalation checks.

---

## ↔️ Lateral Movement

Lateral movement describes the process of moving from one compromised or authorized system to another within an environment. During a red-team exercise, this stage is useful for demonstrating the potential impact of compromised credentials or excessive privileges.

Common concepts include **Pass-the-Hash**, **Pass-the-Ticket**, remote execution, WMI, WinRM, SSH pivoting, and RDP. Tools associated with these activities include **Impacket**, **Rubeus**, **Mimikatz**, **Evil-WinRM**, **Proxychains**, and **FreeRDP**.

The important beginner concept is that lateral movement is not simply "hacking another computer." It involves understanding trust relationships, authentication mechanisms, network segmentation, credentials, and available remote-management services.

---

## 🔒 Persistence

Persistence refers to mechanisms that allow continued access after an initial foothold. In authorized red-team exercises, persistence techniques are used to test whether defenders can detect unauthorized changes.

Examples include:

| Platform             | Areas Commonly Studied                                          |
| -------------------- | --------------------------------------------------------------- |
| **Linux**            | Cron jobs, `.bashrc`, SSH authorized keys, systemd services     |
| **Windows**          | Registry Run keys, scheduled tasks, WMI subscriptions, services |
| **Active Directory** | Golden/Silver Tickets, DCSync rights, AdminSDHolder             |
| **Cloud**            | IAM roles and persistent access keys                            |

Persistence should only be tested when explicitly included in the Rules of Engagement because it can create long-lasting changes to the target environment.

---

## 🕹️ Command & Control (C2)

Command and Control describes the communication mechanism between an authorized red-team operator and an agent operating inside the test environment. Important concepts include **beaconing intervals**, **jitter**, **C2 profiles**, **DNS/HTTP(S) communication**, and **redirectors**.

Commonly discussed frameworks include:

**Cobalt Strike, Sliver, Mythic, Havoc, and Brute Ratel.**

For beginners, understanding the architecture is more important than memorizing individual commands: an operator controls infrastructure, the test agent communicates with that infrastructure, and defenders attempt to identify the resulting network and endpoint behavior.

---

## 🏢 Active Directory Attacks

Active Directory testing focuses on authentication, authorization, delegation, trust relationships, and privilege paths within Windows domain environments. Tools such as **BloodHound**, **Rubeus**, **Impacket**, and **Mimikatz** are frequently associated with AD security research and authorized red-team exercises.

| Attack / Technique      | Tool / Reference         |
| ----------------------- | ------------------------ |
| **Kerberoasting**       | `GetUserSPNs.py`, Rubeus |
| **AS-REP Roasting**     | `GetNPUsers.py`          |
| **DCSync**              | Mimikatz, Impacket       |
| **Golden Ticket**       | Mimikatz                 |
| **Silver Ticket**       | Mimikatz                 |
| **Zerologon**           | CVE-2020-1472 research   |
| **BloodHound Analysis** | SharpHound + BloodHound  |
| **Delegation Abuse**    | Rubeus, Impacket         |

BloodHound is particularly useful for beginners because it helps visualize relationships and potential privilege paths instead of requiring every relationship to be understood from command-line output alone.

---

## 🔑 Password Attacks

Password testing examines the strength and security of authentication credentials. Offline hash analysis and controlled password testing are different from online attacks because they involve different risks and controls.

Common tools include **Hashcat**, **John the Ripper**, and **Hydra**, while **RockYou** and **SecLists** are commonly referenced as wordlist collections.

```bash
# Offline hash testing
hashcat -m 1000 hashes.txt rockyou.txt
hashcat -m 1800 hashes.txt rockyou.txt

john --wordlist=rockyou.txt hashes.txt

# Authorized online authentication testing
hydra -l admin -P rockyou.txt ssh://target
```

Password spraying requires particular care because repeated authentication attempts can trigger account lockouts or affect legitimate users. It should therefore only be performed within clearly defined testing limits.

---

## 📶 Wireless Attacks

Wireless security testing examines how wireless networks are configured and protected. The **Aircrack-ng** suite provides several tools for studying wireless security, while **Wifite** can automate parts of wireless auditing.

| Tool               | Purpose                                 |
| ------------------ | --------------------------------------- |
| `airmon-ng`        | Enable monitor mode                     |
| `airodump-ng`      | Capture wireless traffic and handshakes |
| `aireplay-ng`      | Wireless packet-injection testing       |
| `aircrack-ng`      | WPA/WPA2 handshake analysis             |
| `hashcat -m 22000` | WPA-related hash processing             |
| `wifite`           | Automated wireless auditing             |

Wireless testing should always be performed against networks specifically included in the authorized scope.

---

## 🎭 Social Engineering

Social engineering focuses on the human side of security rather than only technical vulnerabilities. Authorized exercises can include phishing simulations, pretexting, vishing, physical-security assessments, and security-awareness exercises.

**GoPhish** can be used for authorized phishing-awareness campaigns. Clone pages and credential-harvesting simulations should only be used in controlled exercises with appropriate authorization and safeguards.

The objective is to measure awareness and improve defenses rather than collect or misuse real credentials.

---

## 📝 Reporting

Reporting is one of the most important parts of a professional red-team engagement. A technically successful test has limited value if the organization cannot understand what happened, why it matters, and how to improve its security.

A professional report normally includes:

1. **Executive Summary** — A concise explanation of the overall security impact for non-technical stakeholders.
2. **Scope & Methodology** — What was tested, how it was tested, and what limitations applied.
3. **Findings by Severity** — Security findings organized according to their assessed risk, with CVSS scoring where appropriate.
4. **Attack Narrative** — A clear walkthrough showing how individual findings connected during the engagement.
5. **Evidence** — Relevant screenshots, logs, timestamps, and other supporting information.
6. **Remediation** — Practical recommendations for reducing or eliminating the identified risks.
7. **Appendix** — Supporting technical information and relevant tool output.

A good report should allow both technical teams and management to understand the same engagement from their respective perspectives.

---

## 🧠 Red Team Mindset

Red teaming is not simply about collecting offensive tools or memorizing attack commands. The real skill is understanding **how systems are connected, where trust exists, how weaknesses can be chained together, and how defenders can detect those behaviors**.

A strong red-team learning path therefore combines reconnaissance, networking, web security, operating systems, Active Directory, authentication, cloud security, detection engineering, and professional reporting.

> **Learn the technique → understand the risk → test only within scope → document the evidence → help improve the defense.**

---

⬅️ [Back to Main README](../README.md)
