# 🪟 Windows Commands Arsenal

> **A practical Windows CLI reference for system administration, digital forensics, SOC operations, network troubleshooting, Active Directory enumeration, and authorized security testing.**

[![Platform](https://img.shields.io/badge/Platform-Windows-blue?style=flat-square)](#)
[![CMD](https://img.shields.io/badge/CMD-Reference-black?style=flat-square)](#)
[![PowerShell](https://img.shields.io/badge/PowerShell-Reference-5391FE?style=flat-square)](#)
[![Security](https://img.shields.io/badge/Focus-Cybersecurity-red?style=flat-square)](#)
[![Forensics](https://img.shields.io/badge/Focus-Digital%20Forensics-purple?style=flat-square)](#)

---

## 📌 About

This repository contains a structured collection of **Windows CMD and PowerShell commands** commonly useful for:

* 🖥️ Windows administration
* 🔍 Digital forensics
* 🛡️ SOC and blue-team investigations
* 🌐 Network troubleshooting
* 👤 User and privilege auditing
* ⚙️ Process and service analysis
* 📜 Windows Event Log investigation
* 🏢 Active Directory enumeration
* 🔐 Security configuration auditing
* 🎯 Authorized security testing

The commands are organized by category and include practical examples to make them easier to understand in real-world scenarios.

> ⚠️ **Responsible Use:** Run commands only on systems you own or have explicit authorization to administer, investigate, or test.

---

# 📑 Table of Contents

|  # | Section                                                                |
| -: | ---------------------------------------------------------------------- |
| 01 | [System Information](#-01-system-information)                          |
| 02 | [Networking](#-02-networking)                                          |
| 03 | [File & Directory Management](#-03-file--directory-management)         |
| 04 | [Users & Groups](#-04-users--groups)                                   |
| 05 | [Processes & Services](#-05-processes--services)                       |
| 06 | [Registry](#-06-registry)                                              |
| 07 | [Event Logs & Auditing](#-07-event-logs--auditing)                     |
| 08 | [PowerShell Essentials](#-08-powershell-essentials)                    |
| 09 | [PowerShell Remoting](#-09-powershell-remoting)                        |
| 10 | [Active Directory](#-10-active-directory-enumeration)                  |
| 11 | [Security & Privilege Checks](#-11-windows-security--privilege-checks) |
| 12 | [Security Tools](#-12-security-tools)                                  |
| 13 | [Digital Forensics Workflow](#-13-digital-forensics-workflow)          |
| 14 | [Quick Reference](#-14-quick-reference)                                |

---

# 🖥️ 01. System Information

Useful commands for identifying the operating system, hardware, patches, users, policies, and drivers.

| Command                                      | Purpose                              | Real-World Use                                         |
| -------------------------------------------- | ------------------------------------ | ------------------------------------------------------ |
| `systeminfo`                                 | Displays detailed system information | Identify OS, RAM, architecture, patches, and hostname  |
| `hostname`                                   | Displays computer name               | Identify the machine under investigation               |
| `ver`                                        | Displays Windows version             | Quickly identify Windows version                       |
| `wmic os get caption,version,osarchitecture` | Displays OS information              | Check OS version and architecture                      |
| `wmic qfe list`                              | Lists installed hotfixes             | Verify installed security updates                      |
| `set`                                        | Displays environment variables       | Troubleshoot system configuration                      |
| `echo %USERNAME%`                            | Displays current user                | Identify the active account                            |
| `echo %PATH%`                                | Displays PATH variable               | Troubleshoot executable lookup                         |
| `gpresult /r`                                | Displays applied Group Policy        | Review policies affecting a workstation                |
| `driverquery`                                | Lists installed drivers              | Investigate installed or unexpected drivers            |
| `tasklist /svc`                              | Maps processes to services           | Determine which services are associated with processes |

### Example

```cmd
hostname
whoami
systeminfo
wmic qfe list
```

**Scenario:** An administrator receives a suspicious-system report and needs basic information before beginning troubleshooting or investigation.

---

# 🌐 02. Networking

## Network Configuration

| Command              | Purpose                        | Real-World Use                                      |
| -------------------- | ------------------------------ | --------------------------------------------------- |
| `ipconfig`           | Displays IP configuration      | Quickly inspect network settings                    |
| `ipconfig /all`      | Detailed adapter configuration | Troubleshoot DNS, DHCP, gateway, and adapter issues |
| `ipconfig /release`  | Releases DHCP lease            | Reset DHCP configuration                            |
| `ipconfig /renew`    | Renews DHCP lease              | Request a new DHCP configuration                    |
| `ipconfig /flushdns` | Clears DNS cache               | Resolve stale DNS entries                           |
| `arp -a`             | Displays ARP cache             | Review recently resolved local devices              |
| `route print`        | Displays routing table         | Troubleshoot routing problems                       |

## Network Connections

| Command                              | Purpose                              | Real-World Use                                         |
| ------------------------------------ | ------------------------------------ | ------------------------------------------------------ |
| `netstat -ano`                       | Displays connections and PIDs        | Identify processes associated with network connections |
| `netstat -ab`                        | Displays connections and executables | Investigate applications making connections            |
| `ping target`                        | Tests connectivity                   | Verify whether a host is reachable                     |
| `ping -t target`                     | Continuous connectivity test         | Monitor intermittent connectivity                      |
| `tracert target`                     | Traces network path                  | Identify routing failures                              |
| `nslookup domain.com`                | Performs DNS lookup                  | Troubleshoot DNS resolution                            |
| `netsh advfirewall show allprofiles` | Displays firewall status             | Audit Windows Firewall configuration                   |

## Wi-Fi

| Command                                         | Purpose                              | Real-World Use                                |
| ----------------------------------------------- | ------------------------------------ | --------------------------------------------- |
| `netsh wlan show profiles`                      | Lists saved Wi-Fi profiles           | Audit wireless configurations                 |
| `netsh wlan show profile name="SSID" key=clear` | Displays saved Wi-Fi profile details | Recover credentials from an authorized system |

## SMB

| Command                  | Purpose                | Real-World Use                     |
| ------------------------ | ---------------------- | ---------------------------------- |
| `net use \\target\share` | Connects to SMB share  | Access an authorized network share |
| `net view \\target`      | Lists available shares | Review authorized SMB resources    |

### Example

```cmd
ipconfig /all
netstat -ano
arp -a
route print
```

**Scenario:** A SOC analyst is investigating an endpoint with unexpected network activity.

---

# 📂 03. File & Directory Management

| Command                        | Purpose                       | Real-World Use                         |
| ------------------------------ | ----------------------------- | -------------------------------------- |
| `dir`                          | Lists directory contents      | Inspect files in a directory           |
| `dir /a`                       | Includes hidden files         | Find hidden files during investigation |
| `dir /s /b *.txt`              | Recursive file search         | Locate text files                      |
| `cd /d D:\path`                | Changes drive and directory   | Navigate to investigation data         |
| `copy src dst`                 | Copies files                  | Create a backup                        |
| `xcopy src dst /E /H /C /I`    | Copies directories            | Copy investigation data                |
| `robocopy src dst /MIR`        | Mirrors directories           | Synchronize authorized backups         |
| `type file.txt`                | Displays file contents        | Inspect a text file or log             |
| `findstr /si "password" *.txt` | Searches text recursively     | Locate potentially exposed information |
| `fc file1 file2`               | Compares files                | Identify differences between files     |
| `icacls file`                  | Displays permissions          | Audit file access                      |
| `attrib +h +s file`            | Adds hidden/system attributes | Test hidden-file detection             |
| `attrib -h -s file`            | Removes attributes            | Restore file visibility                |
| `takeown /f file`              | Takes ownership               | Recover access to an authorized file   |
| `mklink link target`           | Creates symbolic link         | Create filesystem links                |

### Example — File Comparison

```cmd
fc config_old.txt config_new.txt
```

**Scenario:** An administrator wants to determine whether a configuration file changed between two versions.

---

# 👤 04. Users & Groups

| Command                                       | Purpose                     | Real-World Use                          |
| --------------------------------------------- | --------------------------- | --------------------------------------- |
| `whoami`                                      | Shows current user          | Identify active account                 |
| `whoami /priv`                                | Shows privileges            | Review assigned privileges              |
| `whoami /groups`                              | Shows group membership      | Audit security groups                   |
| `net user`                                    | Lists local users           | Audit local accounts                    |
| `net user username`                           | Displays account details    | Investigate a specific user             |
| `net localgroup administrators`               | Lists local administrators  | Audit privileged accounts               |
| `net accounts`                                | Displays password policy    | Review password and lockout settings    |
| `query user`                                  | Shows logged-in users       | Identify active sessions                |
| `net user username password /add`             | Creates a local user        | Create a test account in a lab          |
| `net user username /delete`                   | Deletes a local user        | Remove an obsolete test account         |
| `net localgroup administrators username /add` | Adds user to Administrators | Authorized administrative configuration |

### Example — Privileged Account Review

```cmd
net user
net localgroup administrators
whoami /groups
```

**Scenario:** An administrator is performing a periodic review of local privileged accounts.

---

# ⚙️ 05. Processes & Services

## Processes

| Command                       | Purpose                      | Real-World Use               |
| ----------------------------- | ---------------------------- | ---------------------------- |
| `tasklist`                    | Lists running processes      | Identify active applications |
| `tasklist /svc`               | Shows processes and services | Map services to processes    |
| `taskkill /PID 1234 /F`       | Terminates a process         | Stop a frozen application    |
| `taskkill /IM notepad.exe /F` | Terminates by name           | Close a stuck application    |
| `wmic process list brief`     | Lists processes using WMI    | Perform process inventory    |

## Services

| Command                | Purpose                        | Real-World Use                     |
| ---------------------- | ------------------------------ | ---------------------------------- |
| `sc query`             | Lists services                 | Review Windows services            |
| `sc query state=all`   | Lists all services             | Audit running and stopped services |
| `sc qc servicename`    | Displays service configuration | Inspect service executable path    |
| `sc start servicename` | Starts service                 | Start an authorized service        |
| `sc stop servicename`  | Stops service                  | Stop a malfunctioning service      |
| `net start`            | Lists running services         | Quickly review active services     |

## Scheduled Tasks

| Command                       | Purpose                | Real-World Use                         |
| ----------------------------- | ---------------------- | -------------------------------------- |
| `schtasks /query /fo LIST /v` | Lists scheduled tasks  | Investigate scheduled execution        |
| `schtasks /create ...`        | Creates scheduled task | Create a test task in a controlled lab |

### Example

```cmd
tasklist
tasklist /svc
sc query state=all
schtasks /query /fo LIST /v
```

**Scenario:** A security analyst investigates an unknown process that starts automatically.

---

# 🗝️ 06. Registry

| Command                            | Purpose               | Real-World Use                         |
| ---------------------------------- | --------------------- | -------------------------------------- |
| `reg query HKLM\Software`          | Queries registry      | Inspect software configuration         |
| `regedit`                          | Opens Registry Editor | Perform manual registry investigation  |
| `reg add ...\Run`                  | Adds startup entry    | Test Windows startup behavior in a lab |
| `reg delete ...\Run`               | Removes startup entry | Remove an unwanted startup entry       |
| `reg save HKLM\SAM sam.save`       | Saves SAM hive        | Authorized forensic acquisition        |
| `reg save HKLM\SYSTEM system.save` | Saves SYSTEM hive     | Authorized forensic acquisition        |

### Common Autorun Locations

| Registry Location                                    | Purpose                          |
| ---------------------------------------------------- | -------------------------------- |
| `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` | User-level startup applications  |
| `HKLM\Software\Microsoft\Windows\CurrentVersion\Run` | System-wide startup applications |
| `HKLM\System\CurrentControlSet\Services`             | Windows services                 |

### Example

```cmd
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

**Scenario:** During malware investigation, an analyst checks common startup locations for unexpected applications.

---

# 📜 07. Event Logs & Auditing

## Event Log Commands

| Command                                        | Purpose               | Real-World Use                      |
| ---------------------------------------------- | --------------------- | ----------------------------------- |
| `eventvwr`                                     | Opens Event Viewer    | Investigate Windows events          |
| `wevtutil el`                                  | Lists event channels  | Discover available logs             |
| `wevtutil qe Security /c:10 /rd:true /f:text`  | Queries Security log  | Review recent security events       |
| `auditpol /get /category:*`                    | Displays audit policy | Determine which auditing is enabled |
| `Get-WinEvent -LogName Security -MaxEvents 20` | Reads Security events | Investigate recent activity         |

## Important Event IDs

| Event ID | Description                | Investigation Use                     |
| -------: | -------------------------- | ------------------------------------- |
| **4624** | Successful logon           | Investigate successful authentication |
| **4625** | Failed logon               | Investigate failed authentication     |
| **4688** | Process creation           | Investigate process execution         |
| **4720** | User account created       | Detect unexpected account creation    |
| **1102** | Security audit log cleared | Investigate possible log tampering    |

### Example

```powershell
Get-WinEvent -LogName Security -MaxEvents 50
```

**Scenario:** A SOC analyst investigates repeated failed authentication attempts on a Windows workstation.

> ⚠️ Avoid clearing security logs during an investigation because doing so can destroy evidence.

---

# 💻 08. PowerShell Essentials

| Command                                      | Purpose                        | Real-World Use                  |
| -------------------------------------------- | ------------------------------ | ------------------------------- |
| `Get-Process`                                | Lists processes                | Monitor applications            |
| `Get-Service`                                | Lists services                 | Audit Windows services          |
| `Get-ChildItem -Recurse -Force`              | Recursive file listing         | Find hidden files               |
| `Get-Content file.txt`                       | Reads file                     | Inspect logs                    |
| `Select-String -Path *.log -Pattern "error"` | Searches text                  | Find errors in logs             |
| `Get-LocalUser`                              | Lists local users              | Audit accounts                  |
| `Get-LocalGroup`                             | Lists local groups             | Review groups                   |
| `Get-NetIPConfiguration`                     | Displays network configuration | Troubleshoot networking         |
| `Test-NetConnection target -Port 443`        | Tests TCP connectivity         | Verify HTTPS connectivity       |
| `Invoke-WebRequest -Uri url -OutFile file`   | Retrieves a web resource       | Download an authorized file     |
| `Invoke-RestMethod`                          | Calls REST APIs                | Query internal services         |
| `Get-ExecutionPolicy`                        | Displays execution policy      | Review PowerShell security      |
| `New-Item -ItemType File -Path file.txt`     | Creates a file                 | Generate a test file            |
| `Get-Acl file \| Format-List`                | Displays ACLs                  | Audit file permissions          |
| `Get-Hotfix`                                 | Lists installed hotfixes       | Check patch status              |
| `$PSVersionTable`                            | Shows PowerShell information   | Identify PowerShell environment |
| `Get-History`                                | Shows session history          | Review commands executed        |

### Example — Network Troubleshooting

```powershell
Test-NetConnection example.com -Port 443
```

**Scenario:** An administrator wants to determine whether an HTTPS endpoint is reachable from a workstation.

---

# 🔐 09. PowerShell Remoting

| Command                                                        | Purpose               | Real-World Use                    |
| -------------------------------------------------------------- | --------------------- | --------------------------------- |
| `Enter-PSSession -ComputerName target -Credential domain\user` | Opens remote session  | Troubleshoot an authorized server |
| `Invoke-Command -ComputerName target -ScriptBlock { whoami }`  | Runs command remotely | Verify remote execution context   |

> PowerShell Remoting should be configured and used according to the organization's authentication and access-control policies.

---

# 🏢 10. Active Directory Enumeration

| Command                             | Purpose                      | Real-World Use                                         |
| ----------------------------------- | ---------------------------- | ------------------------------------------------------ |
| `net user /domain`                  | Lists domain users           | Audit domain accounts                                  |
| `net group "Domain Admins" /domain` | Lists Domain Admin members   | Review privileged accounts                             |
| `net accounts /domain`              | Shows domain password policy | Review authentication policy                           |
| `nltest /domain_trusts`             | Displays domain trusts       | Understand AD relationships                            |
| `dsquery user`                      | Queries AD users             | Search directory accounts                              |
| `dsquery computer`                  | Queries AD computers         | Inventory domain systems                               |
| `Get-ADUser -Filter *`              | Lists AD users               | Perform directory inventory                            |
| `Get-ADGroupMember "Domain Admins"` | Lists group members          | Audit privileged access                                |
| `Get-ADComputer -Filter *`          | Lists domain computers       | Build asset inventory                                  |
| `klist`                             | Displays Kerberos tickets    | Review authentication tickets                          |
| `setspn -T domain -Q */*`           | Queries SPNs                 | Identify service accounts in an authorized environment |

### Example — Domain Admin Review

```powershell
Get-ADGroupMember "Domain Admins"
```

**Scenario:** An organization performs a periodic review of highly privileged Active Directory accounts.

---

# 🛠️ 11. Windows Security & Privilege Checks

These commands can help identify **security-relevant configuration issues** during authorized assessments.

| Command                                                                                 | Security Check               | Real-World Purpose                        |
| --------------------------------------------------------------------------------------- | ---------------------------- | ----------------------------------------- |
| `whoami /priv`                                                                          | Assigned privileges          | Review account privileges                 |
| `reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated` | MSI configuration            | Identify potentially unsafe configuration |
| `reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated` | User MSI configuration       | Compare configuration                     |
| `wmic service get name,displayname,pathname,startmode`                                  | Service configuration        | Review service executable paths           |
| `schtasks /query /fo LIST /v`                                                           | Scheduled tasks              | Identify high-privilege tasks             |
| `cmdkey /list`                                                                          | Stored credential references | Audit saved credentials                   |
| `findstr /si password *.xml *.ini *.txt *.config`                                       | Potential secrets            | Identify accidentally exposed credentials |
| `wmic /namespace:\\root\SecurityCenter2 path AntiVirusProduct get displayName`          | Security products            | Identify installed antivirus              |

---

# 🏢 12. Active Directory Security Tools

| Tool           | Primary Purpose            | Example Use                                                               |
| -------------- | -------------------------- | ------------------------------------------------------------------------- |
| **BloodHound** | AD relationship analysis   | Visualize relationships between users, groups, computers, and permissions |
| **SharpHound** | BloodHound data collection | Collect authorized AD relationship data                                   |
| **PowerView**  | AD enumeration             | Perform directory security research                                       |
| **Rubeus**     | Kerberos security testing  | Analyze Kerberos authentication                                           |
| **NetExec**    | Windows/SMB/AD enumeration | Perform authorized network enumeration                                    |

> ⚠️ These tools can perform security-sensitive operations. Use them only in an authorized lab or assessment.

---

# 🔎 13. Security Enumeration Tools

| Tool                   | Focus                            | Real-World Use                                              |
| ---------------------- | -------------------------------- | ----------------------------------------------------------- |
| **WinPEAS**            | Windows security enumeration     | Identify potentially insecure configurations                |
| **Seatbelt**           | Windows host enumeration         | Collect security-relevant system information                |
| **PowerUp**            | Windows privilege checks         | Identify common misconfigurations                           |
| **Sysinternals Suite** | Windows administration/forensics | Investigate processes, files, autoruns, and system activity |
| **BloodHound**         | Active Directory                 | Analyze privilege relationships                             |
| **SharpHound**         | Active Directory                 | Collect BloodHound data                                     |
| **Rubeus**             | Kerberos                         | Perform authorized Kerberos research                        |
| **NetExec**            | Network/AD                       | Perform authorized Windows enumeration                      |

---

# 🧪 14. Digital Forensics Workflow

A simple Windows endpoint investigation can follow this workflow:

|  Phase | Objective               | Useful Commands                    |
| -----: | ----------------------- | ---------------------------------- |
| **01** | Identify system         | `hostname`, `systeminfo`           |
| **02** | Identify users          | `whoami`, `query user`             |
| **03** | Analyze processes       | `tasklist`, `Get-Process`          |
| **04** | Analyze network         | `ipconfig /all`, `netstat -ano`    |
| **05** | Analyze services        | `sc query`, `Get-Service`          |
| **06** | Analyze scheduled tasks | `schtasks /query /fo LIST /v`      |
| **07** | Analyze files           | `dir /a`, `findstr`, `fc`          |
| **08** | Analyze registry        | `reg query`                        |
| **09** | Analyze event logs      | `wevtutil`, `Get-WinEvent`         |
| **10** | Document findings       | Evidence, timestamps, observations |

---

# ⚡ 15. Quick Reference

| Category                | Primary Commands                                   |
| ----------------------- | -------------------------------------------------- |
| 🖥️ **System**          | `systeminfo`, `hostname`, `ver`, `whoami`          |
| 🌐 **Network**          | `ipconfig`, `netstat`, `arp`, `route`, `nslookup`  |
| 📂 **Files**            | `dir`, `findstr`, `type`, `fc`, `icacls`           |
| 👤 **Users**            | `whoami`, `net user`, `query user`                 |
| ⚙️ **Processes**        | `tasklist`, `taskkill`                             |
| 🔧 **Services**         | `sc`, `net start`, `Get-Service`                   |
| 📜 **Logs**             | `wevtutil`, `Get-WinEvent`, `eventvwr`             |
| 🗝️ **Registry**        | `reg query`, `regedit`                             |
| 💻 **PowerShell**       | `Get-Process`, `Get-Service`, `Get-Acl`            |
| 🏢 **Active Directory** | `net user /domain`, `Get-ADUser`, `Get-ADComputer` |
| 🔐 **Security**         | `whoami /priv`, `auditpol`, `cmdkey`               |
| 🧪 **Forensics**        | Event Logs, Processes, Services, Registry, Network |

---

# ⚠️ Responsible Use

| Rule                      | Guidance                                                        |
| ------------------------- | --------------------------------------------------------------- |
| 🔐 **Authorization**      | Only test systems you own or have explicit permission to assess |
| 🛡️ **Security Controls** | Do not unnecessarily disable Defender or Windows Firewall       |
| 👤 **Accounts**           | Do not create unauthorized accounts                             |
| ⚙️ **Services**           | Do not modify production services without authorization         |
| 📜 **Logs**               | Preserve logs when performing forensic investigations           |
| 🔑 **Credentials**        | Treat discovered credentials as sensitive information           |
| 🧪 **Labs**               | Use isolated virtual machines for security experimentation      |
| 📝 **Documentation**      | Record commands, timestamps, findings, and evidence             |

---

# 🎓 Recommended Practice Environment

For learning Windows security safely:

```text
                 ┌──────────────────────┐
                 │    Windows Client    │
                 │                      │
                 │ CMD / PowerShell     │
                 │ Event Logs           │
                 │ Registry             │
                 │ Services             │
                 └──────────┬───────────┘
                            │
                     Isolated Network
                            │
                 ┌──────────▼───────────┐
                 │    Windows Server    │
                 │                      │
                 │ Active Directory     │
                 │ DNS / Users / Groups │
                 └──────────┬───────────┘
                            │
                     Security Lab
                            │
                 ┌──────────▼───────────┐
                 │      Kali Linux      │
                 │                      │
                 │ Nmap / Wireshark     │
                 │ BloodHound           │
                 └──────────────────────┘
```

This setup lets you practice **Windows administration, Active Directory, network analysis, event-log investigation, and security testing** without interacting with systems you do not control.

---

## 📚 Learning Areas

```text
Windows Administration
        │
        ├── CMD
        ├── PowerShell
        ├── Services
        └── Registry
                │
                ▼
        Windows Security
                │
        ┌───────┼────────┐
        ▼       ▼        ▼
      SOC    Forensics    AD
        │       │         │
        └───────┼─────────┘
                ▼
       Authorized Security Testing
```

---

## ⭐ Contributing

Contributions are welcome.

If you want to improve this reference:

1. Fork the repository.
2. Create a feature branch.
3. Add or improve commands.
4. Include a clear description and practical example.
5. Verify commands before submitting.
6. Open a pull request.

---

## 📄 License

This project is intended for **educational, defensive, administrative, and authorized security-testing purposes**.

---

### 🔙 Navigation

[⬅️ Back to Main README](../README.md)
