# Lab 02: System Audit

**Student Name:** Ben Kishman  
**Date:** 05/Feb/2026

---

## Section 1: System Inventory

| Component | Specification |
|-----------|---------------|
| Operating System | Windows 11 Home version 10.0.26200 |
| Total Installed RAM | 16 GB |
| CPU Model & Clock Speed | AMD Ryzen 7 5700U 1801Mhz/1.8Ghz |
| Storage Capacity | 1 TB |

---

## Section 2: The Access Control Model

### Model Definition
My operating system (Windows 11) uses **Discretionary Access Control (DAC)** as its primary Access Control Model.

**Definition:** Discretionary Access Control (DAC) is a model where the owner of a resource/object manually decides who can read, write, and execute (R/W/X) files. Source: https://csrc.nist.gov/glossary/term/discretionary_access_control

### Relationship to Permissions
In DAC, the file owner can assign R/W/X permissions to specific users or groups, allowing granular control over who can read, modify, or execute files. This allows a network administrator to set varying levels of permissions to different groups or individual users based on necessity and the principle of least privilege.

### Principle of Least Privilege (PoLP) Application
Users are given R/W/X only to files and and resources they absolutely need in order to do their jobs. In addition, admin users are also given limited privilege, such as when installing system-wide programs. In this case, admins must elevate privileges with user account control (UAC) to approve such changes. This prevents unauthorized users from affecting critical portions of the device or network without logging privilege escalation requests. https://csrc.nist.gov/glossary/term/least_privilege

**Concrete Example:**
- Windows: System32 is a critical filepath in Windows 11. Because of how important Sys32 is, access is limited to the least amount of users as possible. Standard users are not owners of the data and are denied R/W/X capability to Sys32. Administrators cannot R/W/X in Sys32 without elevating privilege through UAC. The system account is the only account considered the owner of Sys32 and therefore has full control.

---

## Section 3: Top Process Analysis & Risk

### Process 1:
- **Process Name:** Firefox.exe
- **Process ID (PID):** 2428
- **Resource Consumption:** 2.2GB

**Security Risk Hypothesis:**
Web browsers frequently interact with the open internet which makes them vulnerable to malicious web pages hosting malware, such as watering holes, or Adversary-in-the-middle (AitM) attacks when unencrypted. Firefox runs at the user level and has lower access, but is often used to store credentials for user accounts, credit card information, or other sensitive personal information. If compromised, an attacker could collect all of this information for follow on attacks or identify theft. Alternatively, credentials could be used for lateral movement elsewhere on the device if credentials are re-used in the network. Firefox could also be used as an initial foothold on a target device with the intent to escape into the operating system proper, potentially with harvested stored credentials.

### Process 2:
- **Process Name:** Discord.exe
- **Process ID (PID):** 13128
- **Resource Consumption:** 267.3MB

**Security Risk Hypothesis:**
Similar to web browsers, Discord frequently interacts with the open internet, but generally interacts directly with the Discrod backend servers instead of privately hosted web resources. However, Discord users are still vulnerable to social engineering attacks, or malicious bots which require installation on private servers. If Discord were compromised, an attacker may be able to steal my authorization tokens for remote access. This could be used to masquerade as me for further attacks against other Discord users. Alternatively, while Discord is only run at the standard user level (not admin), Discord reads keyboard input and could be used to steal credentials via keylogger which could enable lateral movement or escalation if they capture admin credentials. Because Discord's function is communication, its traffic in and out of a network is not as scrutinized, and it could make for a discreet method of covert data exfiltration.

### Process 3:
- **Process Name:** NordVPN.exe
- **Process ID (PID):** 13196
- **Resource Consumption:** 156.3MB

**Security Risk Hypothesis:**
VPN software is designed to keep users safe; however, users are still vulnerable to social engineering attacks to harvest credentials. NordVPN runs at the administrator level and at much higher risk for system compromise. If it were compromised, an attacker would have ability to modify routing tables to redirect my traffic for Adversary-in-the-Middle (AitM) attacks against me. Through AiTM attacks they could potentially intercept account credentials, authorization tokens, modify certificates, or direct my traffic to malicious sites or C2 servers hosting malware.

---

## Section 4: Submission Checklist

- [X] File named correctly: System-Audit.md
- [X] All sections completed with accurate information
- [X] Proper Markdown formatting used
- [X] Spell-checked and proofread
- [X] Committed to GitHub with meaningful message (e.g., "Lab 02: Initial System Audit")
- [X] Repository link verified
