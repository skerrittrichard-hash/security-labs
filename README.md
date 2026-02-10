# Security Labs v2 - CompTIA Security+ SY0-701 Hands-On Exercises

## Overview

This repository documents hands-on cybersecurity labs aligned with **CompTIA Security+ SY0-701** certification objectives. Each exercise combines attack methodology, practical exploitation, and forensic analysis to build real-world security competency.

## Purpose

These labs provide practical experience with:
- **Attack Techniques** - Understanding how attackers compromise systems
- **Vulnerability Exploitation** - Leveraging common weaknesses (buffer overflow, directory traversal, weak authentication)
- **Post-Exploitation** - Persistence mechanisms, privilege escalation, lateral movement
- **Forensic Analysis** - Detecting and analyzing attack artifacts in system logs
- **Defense Mechanisms** - Identifying controls and mitigations for each attack type

**Target Audience:** Security+ exam candidates, penetration testers, security professionals

## Exercises

### [Exercise 1: Honeypot Testing](./Exercise-1-Honeypot)
**Activity:** 1.3.1 - Testing a Honeypot  
**Objective:** Deploy and test a honeypot to detect attack attempts  
**Tools:** Kali Linux, Valhalla Honeypot, nmap, Telnet, FTP  
**Key Learning:** Deception technology, attack detection, logging mechanisms  
**Duration:** 30-45 minutes  
**Screenshots:** 7

### [Exercise 2: Dictionary & Brute Force Attack](./Exercise-2-Dictionary-Brute-Force)
**Activity:** 2.2.1, 2.2.2 - Password Attacks  
**Objective:** Compromise credentials using dictionary and brute force attacks  
**Tools:** Metasploit, Hydra, nmap, Telnet, FTP  
**Targets:** Weak authentication on Telnet and FTP services  
**Key Learning:** Authentication vulnerabilities, credential compromise, password cracking  
**Duration:** 45-60 minutes  
**Difficulty:** Intermediate  
**Screenshots:** 3

### [Exercise 3: Buffer Overflow - MS08-067](./Exercise-3-Buffer-Overflow)
**Activity:** 2.5.1 - Performing a Buffer Overflow  
**Objective:** Exploit buffer overflow vulnerability for remote code execution  
**Tools:** Metasploit Framework, Windows XP, Kali Linux  
**Vulnerability:** MS08-067 NetAPI Buffer Overflow (CVSS 10.0)  
**Key Learning:** Buffer overflow mechanics, RCE, post-exploitation, Meterpreter shells  
**Duration:** 45-60 minutes  
**Difficulty:** Intermediate  
**Screenshots:** 6

### [Exercise 4: Directory Traversal Attack & Forensics](./Exercise-4-Directory-Traversal)
**Activity:** 2.13.1 - Recognizing Directory Traversal  
**Objective:** Perform directory traversal to access sensitive files and analyze attack logs  
**Tools:** DVWA, Web browser, PuTTY, Apache2 logs  
**Key Learning:** Path traversal vulnerabilities, web application security, log forensics  
**Duration:** 30-45 minutes  
**Difficulty:** Beginner to Intermediate  
**Screenshots:** 2

## Lab Environment

**Computers Required:**
- Kali Linux VM (attacker system)
- Windows XP-PRO VM (legacy target system)
- Metasploitable2 VM (vulnerable Linux target)
- Host PC (web-based attacks)

**Network:** Lab network isolated from production, intentionally vulnerable VMs for learning purposes

## CompTIA Security+ Alignment

| Exercise | Module | Objectives | Topics |
|----------|--------|-----------|--------|
| 1 | General Security Concepts | 1.1, 1.2, 1.3 | Security controls, detection mechanisms |
| 2 | Threats, Attacks, Vulnerabilities | 2.1, 2.2, 2.3 | Attack methodologies, credential attacks |
| 3 | Threats, Attacks, Vulnerabilities | 2.1, 2.4, 2.5 | Buffer overflow, RCE, post-exploitation |
| 4 | Threats, Attacks, Vulnerabilities | 2.1, 2.6 | Web vulnerabilities, forensic analysis |

## Security+ Exam Focus Areas Covered

- **Attack Vectors:** Dictionary attacks, brute force, buffer overflow, path traversal
- **Vulnerability Assessment:** Service enumeration, weakness identification
- **Exploitation Techniques:** Metasploit usage, payload delivery, RCE
- **Post-Exploitation:** Persistence mechanisms, lateral movement, privilege escalation
- **Detection & Response:** Log analysis, artifact identification, forensic evidence
- **Defense Mechanisms:** Input validation, account lockout, access controls, patching

## Getting Started

1. **Review the activity companion** (CompTIA Security+ SY0-701 Activity Companion)
2. **Set up lab environment** - Configure KVM, Windows XP, Metasploitable2, Kali
3. **Work through exercises sequentially** - Each builds on foundational concepts
4. **Document findings** - Take screenshots, note commands, analyze results
5. **Review forensic evidence** - Examine logs for attack artifacts

## Key Takeaways

### Why These Attacks Matter
- **Honeypots** → Detection of early-stage compromise
- **Dictionary/Brute Force** → Most common initial access method
- **Buffer Overflow** → Legacy systems remain critical risks (Conficker worm)
- **Directory Traversal** → Common web app vulnerability leading to information disclosure

### Real-World Context
- MS08-067 compromised millions of systems via Conficker worm
- Dictionary attacks remain top attack vector (weak password reuse)
- Web application vulnerabilities (OWASP Top 10) affect 90% of applications
- Honeypots detect 100% of attacks they're designed to catch (baseline)

## Professional Notes

**Disclaimer:** These labs are designed for authorized security training in isolated environments only. Unauthorized access to computer systems is illegal.

**Lab Integrity:**
- All exercises performed in controlled, isolated lab environments
- Target systems are intentionally vulnerable for learning purposes
- No real-world systems targeted or compromised
- Purpose is defensive security education

**Transparency:** These labs were completed as part of CompTIA Security+ SY0-701 coursework.

## Next Steps

After completing these 4 exercises, continue with:
- **CySA+ Certification** - Advanced threat analysis and response
- **Penetration Testing** - Real-world vulnerability assessment
- **Incident Response** - Forensic analysis and threat hunting
- **Threat Intelligence** - Understanding attacker tactics and campaigns

## Resources

- **CompTIA Security+ Exam Objectives:** https://www.comptia.org/certifications/security
- **OWASP Top 10:** https://owasp.org/www-project-top-ten/
- **MITRE ATT&CK Framework:** https://attack.mitre.org/
- **Metasploit Documentation:** https://docs.rapid7.com/metasploit/

---

**Repository Status:** Complete (4/4 Exercises)  
**Last Updated:** February 2026  
**Certification Target:** CompTIA Security+ SY0-701  
**Lab Duration Total:** ~3-4 hours hands-on  
**Difficulty Range:** Beginner to Intermediate

**Contact/Questions:** Refer to individual exercise READMEs for detailed command syntax and findings.
