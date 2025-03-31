# Baker Street Corporation | Linux Server Hardening Report

## 🧠 Project Summary  
This system hardening project was conducted on a production-like Ubuntu 24.04 server used by Baker Street Corporation. The goal was to minimize attack surfaces, enforce best practices for access control, secure critical files and services, and automate recurring security tasks.

The engagement followed industry-standard hardening guidelines and included auditing users, removing insecure services, applying password policies, configuring firewalls, and validating log management settings.

---

## 🎯 Scope

- **Target System:** `Baker_Street_Linux_Server (Ubuntu 24.04.1 LTS)`  
- **Engagement Type:** Hands-on system hardening and auditing  
- **Time Frame:** Multi-day audit and configuration  
- **Objectives:**
  - Perform full OS backup  
  - Lock down user accounts and privileges  
  - Remove legacy services and insecure packages  
  - Enforce secure file and SSH configurations  
  - Automate recurring audit tasks via scripts and cron jobs  

---

## 🛠️ Tools & Skills Used  

- **Core Tools:** Bash, UFW, Tripwire, Lynis, `tar`, `find`, `chmod`, `usermod`, `crontab`  
- **Skills Developed:**  
  - Linux user/group management  
  - Secure shell configuration  
  - Firewall and package management  
  - File permission auditing  
  - Script automation and scheduling  
  - Service and log management  

---

## 📋 Executive Summary  

### 🔐 Key Strengths Implemented  

- All terminated user accounts were removed or locked  
- Password policy with complexity and expiration was enforced  
- Root SSH login disabled and port restrictions applied  
- Vulnerable packages (e.g., Telnet, RSH) were removed  
- Logging system (journald) and logrotate configured for space optimization  
- Cron jobs scheduled to run recurring hardening scripts  

### ❗ Risk Mitigations Achieved  

| Risk Area             | Mitigation Summary                                                                 |
|-----------------------|------------------------------------------------------------------------------------|
| Credential Exposure   | Enforced password policy, expired old credentials                                 |
| Remote Access Risks   | Secured SSH access, disabled root login, enabled protocol 2                       |
| File Access Violations| Removed world-accessible home files, enforced script-level group access          |
| Legacy Software       | Removed MySQL, Samba, Telnet, and RSH                                             |
| Insecure Logging      | Persistent logs limited to 300MB and rotated daily                                |

---

## 🗂️ Findings & Configuration Summary  

### 🔧 Pre-Hardening System Backup  
- Backup location: `/backup/baker_street_backup.tar.gz`  
- Exclusions: `/proc`, `/sys`, `/dev`, `/tmp`, `/mnt`, `/run`, and the backup dir  
- Command:
```bash
sudo tar -cvpzf /backup/baker_street_backup.tar.gz --exclude=/backup --exclude=/proc --exclude=/tmp --exclude=/mnt --exclude=/sys --exclude=/dev --exclude=/run /

