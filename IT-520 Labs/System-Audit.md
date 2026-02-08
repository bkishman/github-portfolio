# Lab 02: System Audit

**Student Name:** Ben Kishman  
**Date:** 05/Feb/2026

---

## Section 1: System Inventory

| Component | Specification |
|-----------|---------------|
| Operating System | Windows 11 |
| Total Installed RAM | 16 GB |
| CPU Model & Clock Speed | AMD Ryzen 7 5700U 1801Mhz/1.8Ghz |

---

## Section 2: The Access Control Model

### Model Definition
My operating system (Windows 11) uses Discretionary Access Control (DAC) as its primary Access Control Model.

Definition: Discretionary Access Control (DAC) is a model where the owner of a resource decides who can access it.

### Relationship to Permissions
In DAC, the file owner can assign R/W/X permissions to specific users or groups, allowing granular control over who can read, modify, or execute files.

### Principle of Least Privilege (PoLP) Application
Normal users are not admins, and only admins can make system-wide changes or OS level changes. Admins also do not have full time admin privilege, and only execute elevated authority when needed.

Concrete Example:
- Windows: An administrator wants to install a new browser for all users on the device. Because this is system-wide it requires User Access Control (UAC) authority. The admin is granted temporary authority to install the software.

---

## Section 3: Top Process Analysis & Risk

### Process 1:
- Process Name: Firefox.exe
- Process ID (PID): 2428
- Resource Consumption: 1.6MB

**Security Risk Hypothesis:**
If Firefox were compromised the attacker would have access to all my saved passwords and browser history, and potentially be able to escape into the operating system for privilege escalation.

### Process 2:
- Process Name: Discord.exe
- Process ID (PID): 13128
- Resource Consumption: 86.6MB

**Security Risk Hypothesis:**
If Discord were compromised the attackers would be able to see my communications with friends and classmates. While there is not any valuable corporate or confidental information to be found there, an attacker can glean personal information about me.

### Process 3:
- Process Name: NordVPN.exe
- Process ID (PID): 13196
- Resource Consumption: 156.3MB

**Security Risk Hypothesis:**
If an attacker were to compromise my NordVPN they would be abel to conduct Adversary-in-the-Middle (AitM) attacks against me, and potentially intercept account credentials or inject malicious payloads into my HTTPS traffic.

---

## Section 4: Submission Checklist

- [X] File named correctly: System-Audit.md
- [X] All sections completed with accurate information
- [X] Proper Markdown formatting used
- [X] Spell-checked and proofread
- [X] Committed to GitHub with meaningful message (e.g., "Lab 02: Initial System Audit")
- [X] Repository link verified
