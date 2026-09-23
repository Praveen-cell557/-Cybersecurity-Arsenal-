# 🔵 Blue Teaming — Defensive Security Playbook

> **Detection, monitoring, incident response, digital forensics, threat hunting, and system hardening reference for defenders, SOC analysts, and cybersecurity learners.**

---

## 📁 Table of Contents

* [Core Mindset](#-core-mindset)
* [Monitoring & SIEM](#-monitoring--siem)
* [Log Analysis](#-log-analysis)
* [Threat Hunting](#-threat-hunting)
* [Incident Response](#-incident-response)
* [Digital Forensics](#-digital-forensics)
* [Malware Analysis Basics](#-malware-analysis-basics)
* [Network Defense](#-network-defense)
* [Endpoint Hardening](#-endpoint-hardening)
* [Active Directory Defense](#-active-directory-defense)
* [Detection Engineering](#-detection-engineering)
* [Useful Frameworks](#-useful-frameworks)

---

## 🧠 Core Mindset

Blue teaming is centered around a continuous cycle:

```text
Prevent → Detect → Respond → Recover → Learn
```

The goal is not simply to build stronger security boundaries. Defenders also need to assume that some attacks may bypass preventive controls and ensure that suspicious activity can be detected and investigated quickly.

A strong blue-team approach focuses on reducing **dwell time**, improving visibility, identifying detection gaps, responding to incidents efficiently, and using lessons from previous incidents to strengthen future defenses.

---

## 📊 Monitoring & SIEM

Security monitoring provides defenders with visibility into what is happening across systems, applications, endpoints, and networks. A **SIEM (Security Information and Event Management)** platform brings logs and security events into a centralized location where analysts can search, correlate, investigate, and create detections.

| Tool                    | Purpose                                                                 |
| ----------------------- | ----------------------------------------------------------------------- |
| **Splunk**              | Enterprise log aggregation and investigation using SPL                  |
| **Elastic Stack (ELK)** | Elasticsearch, Logstash, and Kibana for centralized security monitoring |
| **Wazuh**               | Open-source security monitoring and XDR/SIEM capabilities               |
| **Graylog**             | Centralized log management and analysis                                 |
| **Microsoft Sentinel**  | Cloud-native SIEM/SOAR platform                                         |
| **Security Onion**      | Linux distribution focused on network security monitoring and detection |

For example, a Splunk query can be used to identify repeated Windows authentication failures:

```spl
index=windows EventCode=4625
| stats count by user, src_ip
| where count > 5
```

An Elastic/KQL-style investigation can similarly search for Windows authentication failure events:

```text
event.code:4625 and source.ip:*
| stats count() by user.name
```

The important concept for beginners is that a SIEM is not simply a place to store logs. It turns large amounts of security telemetry into searchable information that analysts can use for **detection, investigation, and response**.

---

## 📜 Log Analysis

Logs are one of the most important sources of evidence available to a defender. Different log sources provide different perspectives on an event, so analysts need to understand what each source can reveal.

| Log Source                       | What to Look For                                  |
| -------------------------------- | ------------------------------------------------- |
| **Windows Security 4624 / 4625** | Successful and failed authentication activity     |
| **Windows 4688**                 | Process creation and suspicious command execution |
| **Windows 4672**                 | Special privileges assigned to a logon            |
| **Sysmon Event ID 1**            | Process creation, command line, and hashes        |
| **Sysmon Event ID 3**            | Network connections                               |
| **Sysmon Event ID 11**           | File creation                                     |
| **Linux `/var/log/auth.log`**    | SSH authentication and sudo-related activity      |
| **Web server logs**              | Suspicious requests and scanning patterns         |
| **DNS logs**                     | Suspicious domains and possible beaconing         |
| **Firewall / proxy logs**        | Unusual connections and potential data movement   |

Linux authentication logs can be quickly reviewed from the command line:

```bash
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -nr
```

On Windows, PowerShell can retrieve failed authentication events:

```powershell
Get-WinEvent -FilterHashtable @{LogName='Security';Id=4625} |
Select TimeCreated,Message
```

The objective is not to look at every log manually. Analysts look for **patterns, anomalies, unusual behavior, and events that support an investigation hypothesis**.

---

## 🕵️ Threat Hunting

Threat hunting is a proactive approach to security monitoring. Instead of waiting for an alert, the analyst starts with a reasonable hypothesis and searches available telemetry for evidence that supports or disproves it.

A basic hunting process looks like this:

```text
1. Form a hypothesis
        ↓
2. Search available telemetry
        ↓
3. Validate suspicious activity
        ↓
4. Investigate and document
        ↓
5. Improve detections
```

For example, a defender might investigate whether attackers are abusing legitimate Windows utilities for execution. Other useful hunting leads include encoded PowerShell commands, unusual parent-child process relationships, unexpected outbound connections, newly created scheduled tasks, and unusual authentication patterns.

Examples of suspicious behaviors worth investigating include:

```text
certutil.exe
mshta.exe
regsvr32.exe

powershell.exe -enc ...

winword.exe → powershell.exe

Unexpected outbound connection → non-standard port
```

**MITRE ATT&CK Navigator** can be used to map hunting and detection coverage against adversary techniques and identify areas where visibility is limited.

---

## 🚨 Incident Response

Incident response provides a structured process for handling confirmed or suspected security incidents. The original lifecycle referenced here is based on **NIST SP 800-61**.

```text
1. Preparation
        ↓
2. Detection & Analysis
        ↓
3. Containment, Eradication & Recovery
        ↓
4. Post-Incident Activity
```

During the initial response, defenders should focus on preserving evidence while limiting further damage. Depending on the incident, this can involve isolating affected systems, preserving logs, capturing volatile information, identifying the initial affected system, determining the scope of the incident, containing compromised accounts, removing persistence, and restoring systems from known-good backups.

### First-Response Checklist

```text
[ ] Isolate the affected host at the network level
[ ] Preserve volatile information where possible
[ ] Capture running processes and network connections
[ ] Preserve relevant logs
[ ] Identify the initial affected system
[ ] Determine the scope of the incident
[ ] Check for lateral movement
[ ] Rotate compromised credentials
[ ] Apply appropriate containment
[ ] Remove persistence mechanisms
[ ] Restore from known-good backups
[ ] Complete a post-incident review
[ ] Improve detections based on lessons learned
```

For live Windows triage:

```powershell
Get-Process | Sort CPU -Descending | Select -First 10

netstat -ano

Get-NetTCPConnection -State Established
```

For Linux:

```bash
ps aux --sort=-%cpu | head

ss -tulnp

lsof -i

who -a
```

Incident response should always consider the organization's evidence-preservation requirements and established incident-response procedures.

---

## 🔬 Digital Forensics

Digital forensics focuses on collecting, preserving, and analyzing digital evidence. It can involve memory, disks, filesystems, processes, network connections, browser artifacts, authentication records, and system timelines.

| Tool                     | Purpose                                      |
| ------------------------ | -------------------------------------------- |
| **Volatility 3**         | Memory forensics                             |
| **Autopsy / Sleuth Kit** | Disk and filesystem investigation            |
| **FTK Imager**           | Disk and memory imaging                      |
| **KAPE**                 | Windows artifact collection and triage       |
| **Redline**              | Endpoint investigation and timeline analysis |
| **Timesketch**           | Collaborative timeline analysis              |

A basic Volatility workflow might include:

```bash
vol.py -f memory.raw windows.info

vol.py -f memory.raw windows.pslist

vol.py -f memory.raw windows.netscan

vol.py -f memory.raw windows.malfind
```

One of the most important forensic principles is maintaining **chain of custody**. Investigators should document how evidence was collected, handled, transferred, and analyzed. Hashing can be used to help verify evidence integrity.

```bash
sha256sum image.dd
```

The goal is to ensure that evidence remains trustworthy throughout the investigation.

---

## 🦠 Malware Analysis Basics

Malware analysis generally begins with **static analysis**, where a sample is examined without executing it. Analysts can inspect file types, strings, hashes, metadata, headers, and other characteristics.

```bash
file sample.bin

strings sample.bin | less

sha256sum sample.bin

exiftool sample.bin
```

Tools such as **PEStudio** and **CFF Explorer** can provide additional information about Windows PE files.

Dynamic analysis involves observing what malware does while it executes. This must be performed in a properly isolated analysis environment.

Common tools and environments include:

* **Cuckoo Sandbox**
* **ANY.RUN**
* **Joe Sandbox**
* **Process Monitor**
* **Process Explorer**
* **Wireshark**

Malware should be analyzed in an **isolated, snapshot-capable virtual machine** rather than on a production system or everyday host machine.

---

## 🌐 Network Defense

Network defense focuses on identifying, monitoring, and controlling suspicious network activity. Network security monitoring provides visibility into communication between systems and can help identify scanning, command-and-control traffic, suspicious connections, and other abnormal behavior.

| Tool                   | Purpose                                         |
| ---------------------- | ----------------------------------------------- |
| **Snort / Suricata**   | Network IDS/IPS                                 |
| **Zeek**               | Network traffic analysis                        |
| **pfSense / OPNsense** | Firewall platforms                              |
| **Wireshark**          | Packet analysis                                 |
| **Nmap**               | Authorized self-scanning and exposure discovery |

A simple Suricata rule example is:

```text
alert tcp any any -> $HOME_NET 4444
(msg:"Possible reverse shell port"; sid:1000001;)
```

In a real environment, detection rules should be tested and tuned carefully because overly broad rules can generate significant false positives.

---

## 🖥️ Endpoint Hardening

Endpoint hardening reduces the number of ways an attacker can successfully execute code, obtain privileges, or move through an environment.

Common defensive practices include:

* Enable **Sysmon** with an appropriate configuration.
* Use **application allowlisting** such as AppLocker or WDAC where appropriate.
* Disable unnecessary services and exposed ports.
* Apply **least privilege** and avoid using domain-admin accounts for everyday tasks.
* Maintain a structured patch-management process.
* Track vulnerabilities and prioritize relevant issues.
* Deploy an appropriate **EDR** solution.
* Disable legacy protocols such as SMBv1 where they are not required.
* Review LLMNR and NBT-NS usage in Windows environments.
* Enable **PowerShell Script Block Logging**.
* Use **Constrained Language Mode** where appropriate.

Hardening is most effective when combined with monitoring. Preventive controls reduce opportunities for attack, while telemetry helps identify activity that bypasses those controls.

---

## 🏢 Active Directory Defense

Active Directory is a critical security boundary in many Windows environments, so protecting identity infrastructure is particularly important.

Defensive measures include implementing a **tiered administration model**, regularly auditing privileged groups, monitoring authentication behavior, restricting unnecessary DCSync permissions, and using **LAPS** to provide unique local administrator passwords.

Organizations should also monitor for indicators associated with **Kerberoasting, AS-REP roasting, Golden Tickets, and Silver Tickets**. Regularly reviewing domain privileges and using **BloodHound** within an organization's own environment can help identify risky privilege relationships before they become an attacker pathway.

Additional controls include reducing unnecessary NTLM usage and using appropriate protections such as **Kerberos** and **SMB signing** where applicable.

---

## 🛠️ Detection Engineering

Detection engineering is the process of turning security knowledge into repeatable detections. Instead of relying only on manually investigating alerts, defenders create rules that identify known suspicious behaviors.

**Sigma** provides a vendor-agnostic format for describing detections.

```yaml
title: Suspicious Encoded PowerShell Command

logsource:
  category: process_creation
  product: windows

detection:
  selection:
    Image|endswith: '\powershell.exe'
    CommandLine|contains: '-enc'

  condition: selection

level: high
```

A detection-as-code workflow can be represented as:

```text
Detection idea
      ↓
Sigma rule
      ↓
Convert for SIEM
      ↓
Deploy
      ↓
Test
      ↓
Tune false positives
      ↓
Monitor performance
```

**Atomic Red Team** can be used in controlled environments to test whether defensive detections correctly identify behaviors associated with MITRE ATT&CK techniques.

---

## 📚 Useful Frameworks

| Framework            | Use                                                     |
| -------------------- | ------------------------------------------------------- |
| **MITRE ATT&CK**     | Adversary tactics and techniques knowledge base         |
| **MITRE D3FEND**     | Defensive techniques mapped against adversary behaviors |
| **NIST CSF**         | Cybersecurity risk-management framework                 |
| **CIS Controls**     | Prioritized security practices                          |
| **Cyber Kill Chain** | Attack lifecycle model                                  |
| **Atomic Red Team**  | Controlled testing of ATT&CK-related detections         |

These frameworks help defenders organize security programs rather than relying on isolated tools. For example, ATT&CK can help describe adversary behavior, D3FEND can help organize defensive techniques, and the CIS Controls can provide prioritized security practices.

---

## 🔵 Blue Team Mindset

Blue teaming is more than watching dashboards and responding to alerts. A strong defender tries to understand **what normal activity looks like**, identify deviations, investigate them using reliable evidence, and continuously improve security controls.

The overall defensive cycle can be summarized as:

```text
        ┌───────────────┐
        │    PREVENT    │
        └───────┬───────┘
                ↓
        ┌───────────────┐
        │    DETECT     │
        └───────┬───────┘
                ↓
        ┌───────────────┐
        │    RESPOND    │
        └───────┬───────┘
                ↓
        ┌───────────────┐
        │    RECOVER    │
        └───────┬───────┘
                ↓
        ┌───────────────┐
        │     LEARN     │
        └───────┬───────┘
                │
                └──────────→ Improve Defense
```

> **Good blue teaming is not about preventing every attack. It is about building enough visibility, resilience, and response capability to detect attacks, limit their impact, recover effectively, and continuously improve.**

---

⬅️ [Back to Main README](../README.md)
