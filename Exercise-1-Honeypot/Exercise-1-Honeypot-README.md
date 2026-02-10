# Exercise 1 - Honeypot

## Objective

You will use Kali Linux to test a Honeypot running on XP-PRO. This lab demonstrates how honeypots detect and log attack attempts.

## Lab Setup

### Computers Required
- Kali Linux VM
- XP-Pro VM (running Valhalla Honeypot 1.8)

### Tools
- Valhalla Honeypot 1.8
- Linux terminal
- nmap
- telnet client
- FTP client

## Lab Steps

### 1. Initial Setup
Configure Valhalla Honeypot on XP-PRO and verify connectivity from Kali.

### 2. Reconnaissance
Scan the honeypot target to identify open ports and services.

### 3. Attack Simulation
Test honeypot response to:
- FTP connection attempts
- Telnet access attempts
- Service enumeration

### 4. Log Analysis
Examine what the honeypot logged during the attack attempts.

## Commands

### Kali Linux Terminal

```bash
# Verify network connectivity
ping <XP-PRO IP>

# Scan target for open ports and services
nmap <XP-PRO IP>

# Clear terminal
clear

# Attempt FTP connection
ftp <XP-PRO IP>
administrator
password
dir
bye

# Attempt Telnet connection
telnet <XP-PRO IP>
administrator
password
letmein
getlost!
```

## What You're Testing

**Honeypot Detection:** The Valhalla honeypot appears as a legitimate system with vulnerable services (FTP, Telnet), but actually logs and detects all interaction attempts.

**Key Learning Points:**
- How honeypots detect unauthorized access attempts
- What information is logged during attacks
- How to identify fake services vs. real ones
- Forensic evidence left by attackers

## Real-World Application

Honeypots are used in production environments to:
- Detect early-stage attacks before they hit real systems
- Gather intelligence on attacker behavior and techniques
- Alert security teams to intrusion attempts
- Provide evidence for incident response investigations

## Expected Results

1. Nmap should identify open ports (FTP, Telnet)
2. FTP and Telnet connections should succeed
3. Honeypot should log all connection attempts
4. Log file should show source IP, commands executed, and timestamps

## Notes

- This is a safe, controlled lab environment
- The honeypot is intentionally vulnerable
- In production, honeypots run on isolated network segments
- Modern honeypots (like Valhalla) can emulate many operating systems and services

---

**Security+ Exam Focus:**  
Understand honeypots as a detective control mechanism. Be familiar with terms like "deception technology" and how honeypots support incident detection and response.

**Created:** February 2026  
**Activity File:** 1.3.1-Honeypot.txt  
**Lab Duration:** 30-45 minutes
