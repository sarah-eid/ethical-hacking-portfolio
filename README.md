# Ethical Hacking Portfolio - CS4069 | Spring 2026

**Course:** Ethical Hacking (CS4069)  
**Student:** Sarah Eid  
**Institution:** Effat University  
**Term:** Spring 2026

---

## Course Overview

This portfolio documents my hands-on ethical hacking coursework, covering the full penetration testing lifecycle from reconnaissance to exploitation and reporting. All work was conducted in isolated lab environments (Kali Linux, Docker, WebSploit, DVWA) with explicit authorization.

### Key Technical Areas
- **Reconnaissance:** Google Dorks, OSINT, theHarvester, Sherlock, ExifTool
- **Scanning & Enumeration:** Nmap (SYN scan, OS detection, NSE scripts)
- **Vulnerability Assessment:** OpenVAS, CVE validation via NVD
- **Exploitation:** SQL injection (manual + sqlmap), XSS (reflected/stored/DOM), Social Engineering Toolkit
- **Post-Exploitation:** Password cracking (Hashcat, CUPP), session hijacking
- **Reporting:** Executive summaries, technical findings, remediation

---
## Repository Structure

```
ethical-hacking-portfolio/
├── README.md
├── labs/
│   ├── lab01-footprinting-google-dorks/
│   │   └── lab01.md
│   ├── lab02-passive-recon-osint/
│   │   └── lab02.md 
│   ├── lab03-active-recon-nmap/
│   │   └── lab03.md + screenshots/
│   ├── lab05-social-engineering-set/
│   │   └── lab05.md + screenshots/
│   ├── lab06-sql-injection/
│   │   └── lab06.md + screenshots/
│   └── lab07-password-cracking/
│       └── lab07.md + screenshots/
├── final-project/
│   └── ethical-hacking-final-report.md
└── tools-cheatsheet.md
```
---

## Lab Environment

| Component | Specification |
|-----------|---------------|
| Host OS | Windows 11 |
| Virtualization | Oracle VirtualBox / UTM (ARM) |
| Attack VM | Kali Linux (customized) |
| Target Lab | WebSploit Labs, DVWA, SQLi-LABS, custom Docker containers |
| Network Range | 10.6.6.0/24 (isolated lab network) |

---

## Labs

### Lab 01: Advanced Footprinting with Google Dorks
**Techniques:** Search operators (`intitle:`, `inurl:`, `filetype:`), exposed backups, login pages, cloud configs, DBMS interfaces, financial docs

**Key Find:** Found exposed Adminer database interface (`adminer.php`) and internal financial reports marked "internal use only"

---

### Lab 02: Passive Reconnaissance (OSINT)
**Tools:** theHarvester, Sherlock, ExifTool, OSINT Framework

**Deliverable:** Email pattern inference (`first.last@company.com`), metadata extraction from public PDFs (revealed Adobe Creative Cloud on macOS), social media correlation

---

### Lab 03: Active Reconnaissance with Nmap
**Techniques:** Host discovery (`-sn`), SYN stealth scan (`-sS`), version detection (`-sV`), OS fingerprinting (`-O`), aggressive scan (`-A`), NSE vulnerability scripts

**Critical Find:** OpenSSH 7.9p1 with CVE-2023-38408 (CVSS 9.8 — Critical)

---

### Lab 04: Vulnerability Scanning
**Tool:** OpenVAS via TryHackMe

**Outcome:** Completed full vulnerability scanning room, authenticated scans, report interpretation

---

### Lab 05: Social Engineering with SET
**Attack:** Website cloning + credential harvesting

**Demo:** Cloned DVWA login page, captured credentials (`some.user@gmail.com` / `Pa55w0rdd!`), generated XML report

---

### Lab 06: SQL Injection
**Manual Techniques:** Authentication bypass (`' OR '1'='1'--`), error-based, UNION-based (extracted database `dvwa`, tables `users`/`guestbook`, password hashes)

**Automated:** sqlmap with cookie authentication, database enumeration, table dumping

**Passwords Cracked:** `admin` → `password`, `pablo` → `Letmein`

---

### Lab 07: Password Cracking
**Tools:** Hashcat (dictionary attack on MD5 hashes), CUPP (custom wordlist generation)

**Demo:** Cracked 5/5 passwords using rockyou.txt; generated 37,000 password candidates from OSINT about fictional target "John Smith"

---

## Final Project: Web Application Penetration Test

**Team:** Sarah Eid, Abeer Hussain, Nancy Elhaddad  
**Client:** Simulated company with never-before-tested internal web app

### Vulnerabilities Discovered

| Vulnerability | Impact | CVSS (simulated) |
|---------------|--------|------------------|
| SQL Injection (UNION-based) | Full database compromise, credential theft | Critical (9.8) |
| Cross-Site Scripting (Stored + Reflected) | Session hijacking, account takeover | High (7.4) |

### Manual Exploitation Highlights

**SQLi Authentication Bypass:**
```sql
' OR '1'='1'-- 
```

**UNION Extraction:**
```sql
1' UNION SELECT user, password FROM users#
```

**XSS Payloads:**
```javascript
<script>alert('XSS')</script>
<img src=x onerror=alert('XSS')>
<ScRiPt>alert('XSS')</ScRiPt>
```

### Remediation Provided
- **SQLi:** Parameterized queries (prepared statements)
- **XSS:** Output encoding (`htmlspecialchars()` + HttpOnly cookies + CSP)

---

## Tools & Techniques Reference

| Category | Tools |
|----------|-------|
| OSINT | theHarvester, Sherlock, ExifTool, OSINT Framework |
| Scanning | Nmap, masscan |
| Vulnerability | OpenVAS, NVD, NSE |
| Exploitation | sqlmap, SET, Burp Suite (conceptual) |
| Password | Hashcat, CUPP, rockyou.txt |
| Environment | Kali Linux, Docker, VirtualBox, UTM |

---

## Ethical Compliance

All activities were performed in:
- Isolated lab environments (10.6.6.0/24)
- Authorized targets (DVWA, SQLi-LABS, WebSploit)
- No production systems or real credentials

> *"If you find data you shouldn't see, you stop. You don't touch. You document and disclose responsibly."*

---

## Skills Summary

| Skill | Proficiency |
|-------|-------------|
| Google Dorks | ✅ Advanced |
| OSINT Collection | ✅ Confident |
| Nmap Scanning | ✅ Full suite (SYN, UDP, NSE) |
| SQL Manual Injection | ✅ UNION + Error-based |
| sqlmap Automation | ✅ Confident |
| XSS (Reflected/Stored) | ✅ Bypass techniques |
| Password Cracking | ✅ Dictionary + Custom wordlists |
| Report Writing | ✅ Executive + Technical |

---
**Note:** Screenshots are omitted from this public portfolio for ethical reasons. 
All commands and outputs shown are from authorized lab environments using 
placeholder/ anonymized data. Screenshots are available upon request.

---
*Last Updated: Spring 2026*
