# Exercise 4 - Directory Traversal Attack & Forensics

## Objective

You will perform a directory traversal attack against a vulnerable web application (DVWA), accessing files outside the intended directory structure. You will then examine the attack artifacts left in Apache2 access logs to understand how to detect directory traversal attacks.

## CompTIA Security+ Alignment

**Module 2: Threats, Attacks, and Vulnerabilities**  
**Objectives:** 2.1, 2.6  
**Focus:** Web application vulnerabilities, attack detection, forensic analysis

## Lab Setup

### Computers Required
- Host PC
- Metasploitable2 VM

### Tools
- Web browser
- DVWA (Damn Vulnerable Web Application)
- PuTTY or SSH client
- Linux terminal
- Apache2 access logs

## Lab Steps

### 1. Reconnaissance
Access DVWA on Metasploitable2 and identify vulnerable endpoints.

### 2. Vulnerability Identification
Locate the File Inclusion vulnerability in DVWA.

### 3. Attack Execution
Perform directory traversal using ../ sequences to access /etc/passwd.

### 4. Log Analysis
SSH to Metasploitable2 and examine Apache2 access logs for attack artifacts.

### 5. Forensic Evidence
Identify and document the directory traversal attack in the logs.

## Commands

### Host PC - Web Browser

```
http://<Metasploitable2 IP>/dvwa/vulnerabilities/fi/
```

**Attack Payload:**
```
<Metasploitable2 IP>/dvwa/vulnerabilities/fi/?page=../../../../../etc/passwd
```

### Metasploitable2 - SSH (via PuTTY or Terminal)

```bash
# SSH to Metasploitable2
ssh msfadmin@<Metasploitable2 IP>

# Password: msfadmin

# Navigate to Apache logs
cd /
ls
cd var
ls 
cd log
ls
cd apache2
ls

# View access log with directory traversal attempts
cat access.log

# Search for specific traversal patterns
grep "etc/passwd" access.log
grep "\.\." access.log
```

## What You're Testing

**Directory Traversal Vulnerability:** Also known as "path traversal," this vulnerability allows attackers to access files and directories outside the intended directory structure by using relative path sequences like `../`.

**Attack Mechanics:**
1. Web application improperly validates user input in file include parameters
2. Attacker provides `../` sequences to move up directory tree
3. Attacker accesses sensitive files (/etc/passwd, /etc/shadow, config files)
4. Information disclosure or system compromise occurs

**Key Learning Points:**
- How file inclusion vulnerabilities enable directory traversal
- Why input validation is critical for web security
- How to recognize traversal attempts in access logs
- Difference between access logs and detailed forensic analysis

## Findings

### Attack Execution
Successfully performed directory traversal:
- Vulnerable parameter: `?page=` in DVWA File Inclusion module
- Attack vector: `../../../../../etc/passwd`
- Result: Successfully displayed system user accounts (/etc/passwd)
- Information disclosed: Usernames, UIDs, GIDs, home directories

### Forensic Evidence
Apache2 access log artifacts show:
- Source IP of attacker
- HTTP request with traversal payload
- URL-encoded sequences visible in logs
- Timestamp of attack
- HTTP response code (typically 200 for successful traversal)

**Log Entry Example:**
```
<IP> - - [timestamp] "GET /dvwa/vulnerabilities/fi/?page=../../../../../etc/passwd HTTP/1.1" 200 <bytes>
```

### System Impact
- Sensitive file contents exposed (/etc/passwd)
- Potential for configuration file disclosure
- Possible leakage of database credentials
- Information gathering for further attacks

## Real-World Application

Directory traversal is commonly seen in:
- Web application penetration tests
- Content management system (CMS) exploits
- File upload/download functionality abuse
- Configuration file disclosure attacks
- Preparation for privilege escalation

## Defense Mechanisms

To defend against directory traversal attacks:
- **Input Validation:** Whitelist allowed filenames/paths only
- **Path Canonicalization:** Convert paths to absolute form and verify they're within allowed directory
- **Reject Traversal Sequences:** Block `../`, `..\\`, and encoded variations
- **Use Safe APIs:** Avoid direct file operations with user input
- **Principle of Least Privilege:** Run web server with minimal file system permissions
- **Web Application Firewall (WAF):** Detect and block traversal patterns
- **File Permissions:** Restrict readable files to those necessary for application
- **Logging & Monitoring:** Alert on suspicious patterns in access logs

## Expected Results

1. DVWA File Inclusion vulnerability identified
2. Directory traversal payload successfully crafted
3. /etc/passwd file contents displayed in browser
4. SSH connection to Metasploitable2 established
5. Apache2 access logs located and retrieved
6. Directory traversal attack visible in access logs
7. Source IP, timestamp, and payload identifiable in logs

## Notes

- DVWA is intentionally vulnerable for learning purposes
- Real-world applications should implement strict input validation
- Directory traversal variants: `..%2F`, `..%255F`, `..;/` (encoding bypasses)
- Access logs are crucial for post-incident forensics
- Modern frameworks (Django, Laravel, Rails) provide safe file handling by default

---

**Security+ Exam Focus:**  
Understand directory traversal as a path traversal attack. Know defensive mechanisms: input validation, path canonicalization, WAF rules. Understand how to identify traversal attempts in logs. This is a common web application vulnerability on the Security+ exam.

**Created:** February 2026  
**Activity File:** 2.13.1-DirTrav.txt  
**Lab Duration:** 30-45 minutes  
**Difficulty:** Beginner to Intermediate
