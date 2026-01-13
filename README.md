# Valhalla Honeypot Security Lab

A hands-on Security+ lab demonstrating attack reconnaissance, exploitation, and real-time threat detection using Valhalla honeypot software on Windows XP Pro target with Kali Linux attacker VM.

## Lab Objective

Understand and practice the complete attack chain: reconnaissance → service enumeration → exploitation → detection/logging, while documenting how honeypots detect and log attack attempts in real-time.

## Lab Architecture

- **Target System:** Windows XP Pro (192.168.4.55)
  - Valhalla honeypot software running
  - Multiple vulnerable services intentionally enabled
  - Real-time monitoring and logging
  
- **Attacker System:** Kali Linux (192.168.4.x)
  - Network reconnaissance tools
  - Service interaction and exploitation
  - Attack staging
  
- **Network:** Isolated VMware network (192.168.4.0/24)

## Valhalla Honeypot Configuration

The honeypot was configured with the following intentionally vulnerable services:

| Service | Port | Credentials | Purpose |
|---------|------|-------------|---------|
| WEB Server | 80 | - | HTTP banner grabbing, web reconnaissance |
| FTP Server | 21 | administrator/password | File access exploitation, credential testing |
| TELNET | 23 | root, admin, bobby | Interactive shell access, plaintext credential capture |
| SMTP | 25 | Various | Email service reconnaissance |
| POP3 | 110 | Various | Mail service enumeration |
| FINGER | 79 | - | User enumeration |
| TFTP | 69 | - | Trivial file transfer |
| ECHO | 7 | - | Service availability probing |
| DAYTIME | 37 | - | Timestamp service |

**Figure 1:** Initial Valhalla honeypot configuration screenshot shows all services enabled and listening.

## Attack Progression

### Phase 1: Connectivity & Baseline

**Objective:** Verify lab network connectivity between attacker and target.

**Command:** `ping 192.168.4.55`

**Result:** Successful ICMP echo replies confirm network path open.

**Figure 2:** Ping from Kali to honeypot verifies connectivity (5:14:38 AM).

---

### Phase 2: Reconnaissance & Service Enumeration

**Objective:** Identify open services and gather intelligence on target system.

**Command:** `nmap 192.168.4.55`

**Results:**
- 990 closed ports (security by obscurity failure)
- 9 open ports identified matching Valhalla configuration
- Service versions/banners collected
- Scan completed in 1.69 seconds

**Honeypot Detection:**
- Valhalla immediately flagged FTP probe attempts
- Timestamps: 5:14:38 AM - connection, reconnection, disconnect

**Security+ Concept:** Active vs. Passive Reconnaissance
- Nmap is active reconnaissance (intrusive, detectable)
- Honeypot logging demonstrates real-time detection capabilities
- Incident response: These logs become forensic evidence

**Figure 3:** Nmap scan results with simultaneous honeypot detection logs showing invasion attempts.

---

### Phase 3: HTTP Banner Grabbing & Service Identification

**Objective:** Identify web server software version and gather HTTP metadata.

**Method:** Direct HTTP connection via Firefox to http://192.168.4.55

**Captured Information:**
- **Server Banner:** IIS 5.0 (Windows 2000 era, highly vulnerable)
- **HTTP Response:** 200 OK
- **Content-Type:** text/html
- **Connection:** close
- **Service Response:** "Get lost!" (honeypot trap message)

**Attack Significance:**
- Version identification enables targeted exploit research
- IIS 5.0 has known CVEs (buffer overflows, path traversal, etc.)
- Honeypot detected and logged every request

**Honeypot Logs:**
```
5:18:10 AM) The IP 192.168.4.55 tried to invade by web (GET /)
5:18:10 AM) The IP 192.168.4.55 tried to invade by web (GET favicon.ico)
```

**Figure 4:** Firefox HTTP connection showing IIS 5.0 banner with honeypot detection logs.

---

### Phase 4: FTP Exploitation & File System Access

**Objective:** Attempt credential exploitation against FTP service and access file system.

**Method:** FTP client connection with credential attempts

**Successful Exploit:**
- **Server Banner:** Wu-FTPd 1.7.8 (outdated, vulnerable)
- **Credentials Used:** administrator / (weak password)
- **Authentication Result:** 230 User logged in
- **Access Granted:** Full directory listing with file permissions
  - drwxrwxrwx (world-writable) directories
  - Files listed: index.htm, other system files
  - Permissions reveal weak access controls

**Attack Chain:**
1. Service enumeration (port 21 open)
2. Banner grabbing (WU-FTPd 1.7.8 identified)
3. Credential attempt (administrator account guessed)
4. Successful authentication
5. Unauthorized file system access

**Honeypot Detection:**
```
5:21:48 AM) The IP 192.168.4.55 tried to invade by (USER administrator)
5:21:48 AM) The IP 192.168.4.55 tried to invade by (PASSWORD [redacted])
[Multiple FTP commands logged: SYST, FEAT, EPSY, PASV, LIST]
User authenticated on FTP
```

**Security+ Concepts:**
- Weak password policies
- Default/predictable credentials
- Unauthorized access exploitation
- File permission misconfigurations
- Service-level compromise

**Figure 5:** FTP authenticated session with directory listing and honeypot detection logs showing full attack chain.

---

### Phase 5: TELNET Brute-Force & Interactive Shell Access (In Progress)

**Objective:** Attempt credential brute-forcing against TELNET service and gain interactive shell access.

**Method:** TELNET client with dictionary-based credential attacks

**Attack Strategy:**
- Attempting multiple username/password combinations
- Targeting common accounts: root, administrator, bobby, guest
- Testing weak passwords: password, apples, etc.
- Unencrypted plaintext transmission (TELNET security weakness)

**Attempted Credentials:**
```
Login: administrator / Password: password
Login: bobby / Password: apples
[Additional attempts queued]
```

**Honeypot Detection:**
```
5:23:57 AM) The IP 192.168.4.55 tried to invade by Netbios1 (12345)
5:26:16 AM) The IP 192.168.4.55 tried to invade by telnet (USER ...)
5:26:25 AM) The IP 192.168.4.55 tried to invade by telnet (PASSWORD ...)
5:26:34 AM) The IP 192.168.4.55 tried to invade by telnet (PASSWORD apples)
```

**Honeypot Capabilities Demonstrated:**
- Captures every authentication attempt
- Logs username/password attempts in real-time
- Timestamps each action for forensic analysis
- Provides early warning of brute-force attacks

**Figure 6:** TELNET interactive session with credential attempts and comprehensive honeypot detection logs.

---

## Security+ Objectives Covered

✅ **Threat Assessment & Analysis**
- Identifying vulnerabilities in legacy systems
- Reconnaissance and enumeration techniques
- Active vs. passive information gathering

✅ **Vulnerability Management**
- Service version identification
- Weakness exploitation
- Legacy system exposure

✅ **Incident Detection & Response**
- Real-time threat logging
- Attack evidence collection
- Forensic timeline reconstruction
- Honeypot deployment as detection tool

✅ **Network Security**
- Service port enumeration
- Protocol exploitation (FTP, TELNET, HTTP)
- Weak credential policies

✅ **Access Control**
- Credential brute-forcing
- Authentication bypass
- File permission exploitation

## Lab Learning Outcomes

1. **Reconnaissance Skills:** Understand how attackers identify target systems and services
2. **Exploitation Techniques:** Practice real-world attack methods (banner grabbing, credential attempts, file access)
3. **Detection & Logging:** Recognize how honeypots detect attacks and log evidence
4. **Forensic Analysis:** Analyze attack logs to understand attacker methodology and timeline
5. **System Hardening:** Identify configuration weaknesses (exposed services, weak credentials, legacy software)

## Key Vulnerabilities Identified

- **Unnecessary Services:** Multiple unneeded services running (DAYTIME, ECHO, FINGER, etc.)
- **Legacy Software:** Windows XP Pro, IIS 5.0, Wu-FTPd 1.7.8 with known exploits
- **Weak Credentials:** Simple, guessable usernames and passwords
- **Plaintext Protocols:** TELNET, FTP transmit credentials unencrypted
- **File Permissions:** World-writable directories and files
- **No Service Hardening:** Default configurations with minimal security

## Tools Used

- **Valhalla Honeypot:** Real-time attack detection and logging
- **Nmap:** Network reconnaissance and service enumeration
- **FTP Client:** File transfer and authentication testing
- **TELNET Client:** Interactive service interaction and credential attempts
- **Firefox:** HTTP banner grabbing and web service testing
- **Kali Linux:** Attack staging platform with integrated pentesting tools

## Honeypot Value Proposition

This lab demonstrates why honeypots are valuable in security:

1. **Early Warning System:** Detects intrusion attempts before they reach production systems
2. **Forensic Evidence:** Captures complete attack timeline with timestamps
3. **Attack Characterization:** Logs specific techniques, tools, and targets used
4. **Threat Intelligence:** Reveals attacker methodology and skill level
5. **No False Negatives:** Every attack is logged (unlike IDS/IPS which can miss attacks)

## Next Steps

- [ ] Achieve successful TELNET authentication
- [ ] Execute system reconnaissance commands (whoami, id, cat /etc/passwd)
- [ ] Document privilege escalation attempts
- [ ] Analyze complete honeypot logs for forensic reconstruction
- [ ] Demonstrate system compromise indicators
- [ ] Test honeypot detection against various attack tools

## Transparency Note

This lab documentation was created with assistance from Claude AI. Attack methodology, Security+ concept mapping, and lab structure were developed through collaborative analysis. All technical work (lab configuration, actual attacks, screenshot capture) was performed hands-on by the student.

## References

- CompTIA Security+ Exam Objectives (SY0-701)
- OWASP Top 10 and vulnerability assessment methodologies
- NIST Cybersecurity Framework - Detect function
- Honeypot deployment best practices
- Incident response and forensic analysis principles

---

**Lab Status:** In Progress  
**Last Updated:** January 13, 2026  
**Next Session:** Continue exploitation and forensic analysis phase
