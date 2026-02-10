# Exercise 2 - Dictionary & Brute Force Attack

## Objective

You will perform dictionary and brute force attacks against vulnerable services (Telnet and FTP) running on Metasploitable2. This lab demonstrates how weak credentials and inadequate authentication controls allow attackers to gain unauthorized access.

## CompTIA Security+ Alignment

**Module 2: Threats, Attacks, and Vulnerabilities**  
**Objectives:** 2.1, 2.2, 2.3  
**Focus:** Attack methodologies, vulnerability identification, credential compromise

## Lab Setup

### Computers Required
- Kali Linux VM
- Metasploitable2 VM

### Tools
- nmap (network scanner)
- Metasploit Framework
- Hydra (password cracking tool)
- Terminal/Command line

## Lab Steps

### 1. Network Reconnaissance
Scan the target network to identify active hosts and open services.

### 2. Service Enumeration
Identify vulnerable services running on the target (Telnet, FTP).

### 3. Dictionary Attack - Telnet
Perform a dictionary attack against Telnet service using weak credentials.

### 4. Brute Force Attack - FTP
Execute a brute force attack against FTP service to gain unauthorized access.

### 5. Credential Verification
Confirm successful credential compromise and access.

## Commands

### Kali Linux Terminal

```bash
# Verify target IP
ifconfig

# Scan target for open ports
nmap <Metasploitable2 IP>
nmap -A <Metasploitable2 IP>

# Start Metasploit
msfconsole

# Search for dictionary attack module
search telnet
search auxiliary/scanner/telnet

# Use Telnet scanner
use auxiliary/scanner/telnet/telnet_version
set RHOSTS <Metasploitable2 IP>
show options
run

# Dictionary attack on Telnet (example with Hydra)
hydra -L users.txt -P passwords.txt telnet://<Metasploitable2 IP>

# FTP brute force (example with Hydra)
hydra -L users.txt -P passwords.txt ftp://<Metasploitable2 IP>

# Verify successful access
telnet <Metasploitable2 IP>
ftp <Metasploitable2 IP>
```

## What You're Testing

**Dictionary Attack:** Attempting to guess credentials using a pre-compiled list of common usernames and passwords.

**Brute Force Attack:** Systematically trying every possible password combination until access is gained.

**Key Learning Points:**
- How weak credentials lead to unauthorized access
- Why service enumeration is critical for attackers
- How dictionary/brute force attacks exploit poor password policies
- The role of account lockout policies in defending against these attacks

## Findings

### Nmap Scan Results
Identified open ports including:
- Port 21 (FTP) - Anonymous access or weak credentials
- Port 23 (Telnet) - Unencrypted remote access
- Additional services vulnerable to attack

### Telnet Dictionary Attack Results
Successfully compromised credentials through dictionary attack:
- Username: [compromised]
- Password: [found]
- Method: Dictionary wordlist matched weak password

### FTP Brute Force Results
Successfully gained FTP access:
- Username: [compromised]
- Password: [cracked]
- Method: Brute force attack with common password combinations

## Real-World Application

Dictionary and brute force attacks are commonly used in:
- Initial access phase of penetration tests
- Post-breach credential discovery
- Lateral movement within compromised networks
- Testing password policy effectiveness

## Defense Mechanisms

To defend against these attacks:
- Enforce strong password policies (complexity, length, expiration)
- Implement account lockout after failed attempts
- Use encrypted protocols (SSH instead of Telnet)
- Enable multi-factor authentication (MFA)
- Monitor failed login attempts
- Disable unnecessary services
- Use intrusion detection systems (IDS)

## Expected Results

1. Nmap identifies vulnerable services (Telnet, FTP)
2. Dictionary attack successfully compromises Telnet credentials
3. Brute force attack successfully compromises FTP credentials
4. Attacker gains interactive access to services
5. Unauthorized commands can be executed/files accessed

## Notes

- This is a controlled lab environment with intentionally weak credentials
- In production, services like Telnet should be disabled in favor of SSH
- Modern systems implement protections like rate-limiting and account lockouts
- Real-world attacks often use tools like Hashcat, John the Ripper, or Hydra

---

**Security+ Exam Focus:**  
Understand the difference between dictionary attacks and brute force attacks. Know defensive mechanisms: account lockout policy, strong password requirements, MFA, protocol upgrades (SSH vs Telnet), and monitoring.

**Created:** February 2026  
**Lab Duration:** 45-60 minutes  
**Difficulty:** Intermediate
