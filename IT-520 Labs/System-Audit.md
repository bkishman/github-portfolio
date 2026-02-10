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
My operating system (Windows 11) uses Discretionary Access Control (DAC) as its primary Access Control Model.

Definition: Discretionary Access Control (DAC) is a model where the owner of a resource/object manually decides who can read, edit, and execute files. Source: https://csrc.nist.gov/glossary/term/discretionary_access_control

### Relationship to Permissions
In DAC, the file owner can assign R/W/X permissions to specific users or groups, allowing granular control over who can read, modify, or execute files.

### Principle of Least Privilege (PoLP) Application
Users are given R/W/X only to files and and resources they absolutely need in order to do their jobs. In addition, admin users are also given limited privilege, such as when installing system-wide programs. In this case, admins must elevate privileges with user account control (UAC) to approve such changes. This prevents unauthorized users from affecting critical portions of the device or network without logging privilege escalation requests.

Concrete Example:
- Windows: System32 is a critical filepath in Windows 11. Because of how important Sys32 is, access is controlled by DAC. Standard users are not owners and are denied R/W/X. Administrators cannot do so without elevating privilege through UAC. The system account is the only account considered the owner of Sys32 and therefore has full control.

---

## Section 3: Top Process Analysis & Risk

### Process 1:
- Process Name: Firefox.exe
- Process ID (PID): 2428
- Resource Consumption: 1.6MB

**Security Risk Hypothesis:**
If Firefox were compromised the attacker would have access to all my saved passwords, browser history, saved credit card information, and potentially serve as a landing spot for malicious users to escape into the operating system for pivoting and/or privilege escalation.

### Process 2:
- Process Name: Discord.exe
- Process ID (PID): 13128
- Resource Consumption: 86.6MB

**Security Risk Hypothesis:**
If Discord were compromised, an attacker may be able to steal my authorization tokens for remote access. This could be used to masquerade as me for further attacks. Alternatively, Discrod reads keyboard input and could be used to steal credentials elsewhere on my device.

### Process 3:
- Process Name: NordVPN.exe
- Process ID (PID): 13196
- Resource Consumption: 156.3MB

**Security Risk Hypothesis:**
If NordVPN were compromised, an attacker would be able to conduct Adversary-in-the-Middle (AitM) attacks against me, and potentially intercept account credentials, authorization tokens, or inject malicious payloads into my HTTP(S), DNS, or other types of traffic.

---

## Section 4: Submission Checklist

- [X] File named correctly: System-Audit.md
- [X] All sections completed with accurate information
- [X] Proper Markdown formatting used
- [X] Spell-checked and proofread
- [X] Committed to GitHub with meaningful message (e.g., "Lab 02: Initial System Audit")
- [X] Repository link verified
