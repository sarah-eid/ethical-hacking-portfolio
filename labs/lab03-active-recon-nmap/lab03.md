## Course Title: Ethical Hacking Course #: CS 4069

| **CS 4069** | **Ethical Hacking** | **Lab03** | **Spring 2026** |
| ----------- | ------------------- | --------- | --------------- |
| Name:       | Sarah Eid           |           |                 |
| Student ID: | S22107757           | Section:  | 2               |

**Lab03 - Advanced Network Scanning and Vulnerability Enumeration with Nmap**

**Objective:**

In this lab, you will:

• Perform host discovery and service enumeration using Nmap

• Conduct advanced port scanning techniques

• Use NSE scripts for vulnerability detection

• Validate vulnerabilities using the NIST National Vulnerability Database

• Complete a challenge-based reconnaissance task

**Important:**

Only scan systems that are part of your authorized lab environment (e.g., 10.6.6.x range, gravemind.vm, or other Docker targets visible from your Kali VM).

**Part 1: Host Discovery and Target Identification**

Step 1: Verify Network Connectivity

Start and log into the Cisco Ethical Hacker Kali VM.

Open a terminal window.

Verify that the known lab target is reachable:

┌──(kali㉿Kali)-\[~\]

└─\$ ping -c5 10.6.6.23

Alternatively:

┌──(kali㉿Kali)-\[~\]

└─\$ ping -c5 gravemind.vm

Was the host reachable?

Yes, the host responded successfully to ping requests.

Step 2: Discover Additional Lab Targets

Since the Cisco Ethical Hacker environment includes multiple Docker-based targets, discover active hosts in the lab network:

┌──(kali㉿Kali)-\[~\]

└─\$ sudo nmap -sn 10.6.6.0/24

List all active IP addresses discovered in the subnet.

---
Select one additional active host (other than 10.6.6.23) for scanning in later sections.

Write the selected IP:

MAC Address: 02:42:0A:06:06:0B (Unknown)

Nmap scan report for juice-shop.vm (10.6.6.12)

**Part 2: Port Scanning and Service Enumeration**

Step 1: Default Scan with Version Detection

Run:

┌──(kali㉿Kali)-\[~\]

└─\$ nmap -sV 10.6.6.23

What ports are open?

---
The open ports detected were 21, 22, 53, 80, 139, and 445.

What services and versions are running?

The scan revealed vsFTPd 3.0.3 on port 21, OpenSSH 7.9p1 on port 22, ISC BIND 9.11.5 on port 53, nginx 1.14.2 on port 80, and Samba services on ports 139 and 445.

Step 2: TCP SYN Scan (Stealth Scan)

┌──(kali㉿Kali)-\[~\]

└─\$ sudo nmap -sS 10.6.6.23

Compare the results with the previous scan.

Were there any differences?

The SYN scan detected the same six open ports (21, 22, 53, 80, 139, and 445) as the version detection scan, but without showing service versions.

There were no differences in the open ports, only the absence of version details in the SYN scan.

Why is SYN scan commonly used in penetration testing?

A SYN scan is commonly used because it is faster and more stealthy since it does not complete the full TCP handshake

Step 3: Full Port Scan

By default, Nmap scans only the top 1000 ports. Perform a full scan:

┌──(kali㉿Kali)-\[~\]

└─\$ sudo nmap -sS -p- 10.6.6.23

Were any additional ports discovered?

No additional ports were discovered, as the full scan revealed the same six open ports.

Explain why scanning all 65535 ports can be important.

Scanning all 65535 ports is important because some services may run on non-standard ports that a default scan would not detect.

**Part 3: Operating System Detection and Aggressive Scan**

Step 1: OS Detection

┌──(kali㉿Kali)-\[~\]

└─\$ sudo nmap -O 10.6.6.23

What operating system is detected?

The operating system was detected as Linux, specifically a Linux kernel version between 4.15 and 5.8.

Step 2: Aggressive Scan

┌──(kali㉿Kali)-\[~\]

└─\$ sudo nmap -A 10.6.6.23

What additional information did the -A scan reveal?

Examples may include:

• Service banners

• Script results

• Traceroute

• Host scripts

The -A scan revealed service banners, anonymous FTP login access, SMB configuration details, host script results, operating system information, and traceroute data.

**Part 4: Vulnerability Enumeration with NSE**

Step 1: Vulners Script

Run the vulners script:

┌──(kali㉿Kali)-\[~\]

└─\$ nmap -sV --script vulners --script-args mincvss=4 10.6.6.23

---
Which service shows known vulnerabilities?

The scan discovered multiple high-severity vulnerabilities affecting vsftpd, OpenSSH, ISC BIND, and nginx services.

List one CVE with CVSS score 5 or above.

OpenSSH appears the most vulnerable, with several vulnerabilities scoring as high as 9.8.

Step 2: Validate Using NIST

Go to the National Vulnerability Database:

<https://nvd.nist.gov/vuln/search>

Search for the CVE identified above.

What severity level is assigned by NIST?

Critical

Provide a short explanation of what the vulnerability allows an attacker to do.

This vulnerability allows an attacker to execute arbitrary code on the target system, potentially leading to full system compromise.

**Part 5: NSE Script Categories**

Step 1: Default Scripts

┌──(kali㉿Kali)-\[~\]

└─\$ sudo nmap -sC 10.6.6.23

What additional information was revealed?

The script scan revealed anonymous FTP access, SMB security settings, DNS version information, and the system hostname.

Step 2: Vulnerability Category

┌──(kali㉿Kali)-\[~\]

└─\$ sudo nmap --script vuln 10.6.6.23

---
Which vulnerability script provided the most meaningful output?

The http-vuln-cve2011-3192 script provided the most meaningful output. It identified a confirmed Apache Byterange Filter DoS vulnerability (CVE-2011-3192) on port 80, including the CVE ID, disclosure date, and multiple reference links.

**Part 6: Challenge-Based Investigation** _(Complete any_ **_one of the three challenges_**_; the remaining two are optional but highly recommended for deeper practice.)_

Challenge 1: Identify the Most Critical Service

Using your full scan results:

• Identify the service with the highest CVSS score

• Identify the port number

• Identify the associated CVE

• Explain why it represents the highest risk

**Service with the highest CVSS score:** OpenSSH 7.9p1 on port **22/tcp**

**Port number:** 22

**Associated CVE:** CVE-2023-38408 (CVSS: 9.8)

**It represents the highest risk:**

- CVSS score of 9.8 (Critical) - the highest across all discovered services
- Multiple public exploits are available for this CVE
- SSH is a remote access service, meaning exploitation could give an attacker full remote control of the system
- The version running (OpenSSH 7.9p1) is outdated and unpatched
