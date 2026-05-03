## Course Title: Ethical Hacking Course #: CS 4069

| **CS 4064** | **Ethical Hacking** | **Lab01** | **Spring 2026** |
| ----------- | ------------------- | --------- | --------------- |
| Name:       | Sarah Eid           |           |                 |
| Student ID: | S22107757           | Section:  | 2               |

**Lab01 - Advanced Footprinting with Google Dorks**

**Objective:** To help students understand and practice advanced Google Dorking techniques for uncovering sensitive information, including exposed login pages, backup files, cloud configurations, and more. The lab will guide students through challenging real-world scenarios while reinforcing ethical hacking principles.

**Part 1: Google Dorking Basics**

- **Introduction to Google Dorks:**
  - Explain how Google Dorks are powerful search operators used to uncover hidden information on the internet. These techniques can be used to locate sensitive files, vulnerable services, exposed login pages, and more.

Google Dorks are advanced search operators used to create complex queries for extracting sensitive or hidden information that is not typically visible through standard searches. By using specific operators like intitle:, inurl:, and site:, we can uncover sensitive files, including VPN configuration files, static keys, and private directories containing sensitive information.

- - Discuss the importance of using these tools in ethical penetration testing while maintaining legal and ethical boundaries.

Using tools like Google Dorks in ethical penetration testing helps security professionals identify vulnerabilities by simulating hacker techniques. This approach enhances an organization's security and prevents unauthorized access. Assessments must be conducted with explicit permission, aligning with legal and ethical standards. Unauthorized operations shift from protective measures to illegal attacks.

**Part 2: Advanced Google Dork Tasks**

**Challenge 1: Finding Sensitive Backup Files**

- **Google Dork Examples:**
  - inurl:/backup/ filetype:sql (Look for SQL database dumps)
  - inurl:/old/ filetype:bak (Look for backup files)
  - intitle:"index of" "parent directory" inurl:/.bak/ (Look for exposed .bak files)
- **Objective:**  
   Students will identify sites storing backup files in publicly accessible directories, potentially containing database dumps or sensitive configuration files.
- **Challenge Outcome:**  
   Students should explain what types of information they found and analyze the risks associated with exposing such backup files.

**Google Dork Used:** site:github.com inurl:backup filetype:sql

I found a SQL script located in a public GitHub repository belonging to Microsoft. While this specific file is a public sample, if a similar file were found on a private company's server. Exposing backup files provides an attacker with a blueprint of the organization's data structure and the actual data itself without needing to bypass the live application's security.

---
**Challenge 2: Searching for Exposed Login Pages**

- **Google Dork Examples:**
  - intitle:"login" inurl:admin (Search for admin login pages)
  - inurl:login "username" "password" (Look for login pages containing "username" and "password" in the source code)
  - inurl:admin intext:"forgot password" (Look for forgotten password links)
- **Objective:**  
   Challenge students to find exposed login pages and assess the security risks of weak or improperly secured login interfaces.
- **Challenge Outcome:**  
   Students should identify any login pages and explain why these pages might be vulnerable to brute-force attacks or unauthorized access.

Google Dork Used: "Trinity College" intitle:"login" inurl:admin

I found a login page for the iModules (now Anthology) administrative portal specifically for Trinity College. Publicly exposing the "front door" to a sensitive management system increases the attack surface of the institution. Security best practices recommend restricting these pages so they are only accessible from the university's internal network or via a secure VPN.

---
**Challenge 3: Exposing Cloud Configuration Files**

- **Google Dork Examples:**
  - intitle:"index of" "config" "cloud" (Look for exposed cloud configuration files)
  - filetype:json "aws_access_key_id" (Search for JSON configuration files containing AWS access keys)
  - filetype:env "DATABASE_URL" (Look for environment files that might contain sensitive database URLs)
- **Objective:**  
   Students will search for exposed cloud configuration files that could reveal sensitive information, such as access keys or database connection details.
- **Challenge Outcome:**  
   Students should identify any cloud-related configuration files and evaluate the severity of exposing such information.

**Google Dork Used:** filetype:env "DB_PASSWORD" -github.com

I found sample data, this file tells an attacker exactly what technologies the organization is using (PostgreSQL, ElasticSearch, Kibana). They can now look for specific vulnerabilities (CVEs) related to those software versions.

---
**Challenge 4. Identifying Exposed Database Management Systems (DBMS)**

**Task:**  
Challenge students to search for publicly exposed databases (e.g., phpMyAdmin, MongoDB) and other database management systems that are left unprotected.

**Google Dork Example:**

- inurl:phpmyadmin (Look for exposed phpMyAdmin instances)
- intitle:"phpMyAdmin" "login" (Find phpMyAdmin login pages)
- inurl:adminer (Look for exposed Adminer database management interfaces)

**Google Dork Used:** intitle:"Adminer" inurl:adminer.php

I found a live Adminer database management interface at "<https://экономныймагазин.рф/adminer.php>." Exposing a database management tool like Adminer directly to the internet is a critical security flaw. Access should be restricted to internal IP addresses only or hidden behind a secure VPN.

---
**Challenge 5: Finding Financial Reports and Documents**

- **Google Dork Examples:**
  - intitle:"index of" "financial report" filetype:pdf (Look for financial reports in PDF format)
  - filetype:xls "budget" "confidential" (Look for confidential budget spreadsheets)
- **Objective:**  
   Challenge students to find exposed financial documents and evaluate the impact of these leaks on an organization's reputation and security.
- **Challenge Outcome:**  
   Students should identify any financial documents found and discuss how the leakage of such documents could be used in attacks like corporate espionage or fraud.

**Google Dork Used:** filetype:pdf "internal use only" "financial report" 2024

I found a detailed Monthly Financial Report for February (FY24) typically intended for internal board members or management rather than the general public. Sensitive documents should be stored in a password-protected environment or a secure cloud storage solution rather than a public-facing web directory.

---
**Challenge 6: Exposed Vulnerability Scanner Results**

- **Google Dork Examples:**
  - filetype:xml "vulnerability report" (Look for vulnerability scanner reports in XML format)
  - intitle:"vulnerability" "scan report" (Search for web pages containing vulnerability scan reports)
- **Objective:**  
   Students will search for vulnerability scanner results and analyze the risks of exposing such sensitive data, which could provide attackers with a roadmap for exploiting vulnerabilities.
- **Challenge Outcome:**  
   Students should explain the potential risks associated with exposing vulnerability reports and recommend how to secure these results properly.

**Reflection:**

After completing this lab, reflect on the following:

- How did the use of Google Dorks help uncover sensitive information?

They allowed me to bypass the "front end" of websites and find files that administrators likely didn't realize were public (like monthly financials and database managers).

- What potential security risks can arise from exposing such data?

Data breaches, identity theft, and providing attackers with a direct path to exploit systems (especially via vulnerability reports).

- What ethical considerations should be kept in mind when using these techniques in real-world scenarios?

Finding this data is for educational/defense purposes only. Accessing private data or attempting to log in to the "Adminer" page we found would be illegal.

- How would you responsibly disclose a vulnerability you discovered during your research?

If this were a real discovery, i would look for a "Security" or "Vulnerability Disclosure" policy on the organization's website and send an encrypted email to their IT team.
