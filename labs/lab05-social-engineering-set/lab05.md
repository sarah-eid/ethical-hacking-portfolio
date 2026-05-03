## Course Title: Ethical Hacking Course #: CS 4069

| **CS 4069** | **Ethical Hacking** | **Lab05** | **Spring 2026** |
| ----------- | ------------------- | --------- | --------------- |
| Name:       | Sarah Eid           |           |                 |
| Student ID: | S22107757           |           |                 |

**Lab 5 - Social Engineering Attacks - Explore the Social Engineer Toolkit (SET)**

**Objectives**

Many exploits begin with a social engineering attack that is designed to obtain credentials or plant malware to create entry points into the target network. One of the tools used to perform these social engineering attacks is the Social Engineer Toolkit (SET), developed by David Kennedy.

- Launching SET and exploring the toolkit
- Cloning a website to obtain user credentials
- Capturing and viewing user credentials

**Background / Scenario**

In this activity, you will **_clone a website and obtain user credentials_**. This activity is performed under carefully controlled conditions within a virtual environment. SET tools should only be used for penetration testing in situations where you have written permission to perform social engineering exploits.

In an actual penetration test, this procedure could be used to reveal problems with user security training and the need to take measures to educate users about various types of phishing attacks.

**Instructions**

**Part 1: Launching SET and Exploring the Toolkit**

**Step 1: Load the SET application.**

- Start Kali Linux using the username **kali** and the password **kali**. Open a terminal session from the menu bar at the top of the screen.
- SET must be run as root. Use the **sudo -i** command to obtain persistent root access. At the prompt, enter the command **setoolkit** to load the SET menu system. The Social Engineering Toolkit can also be run from the **Applications >Social Engineering Tools >social engineering toolkit (root)** choice on the Kali menu.

┌──(kali㉿Kali)-\[~\]

└─\$ **sudo -i**

\[sudo\] password for kali:

┌──(root㉿Kali)-\[~\]

└─# **setoolkit**

- After reading the disclaimer, enter **y** to accept the terms of service.

**Step 2: Examine the Available Social-Engineering Attacks.**

- At the SET prompt, enter **1** and press **Enter** to access the Social-Engineering Attacks submenu.
- Select each option to see a brief description of each exploit and what the tool does for each.

**Note**: Some options may not have a choice. In that case, use **CTRL-C** or enter **99** to return to the main menu.

Which option creates a DVD or USB thumb drive that will autorun malicious software when inserted into the target device?

**_Infectious Media Generator (Option 3 in the Social-Engineering Attacks menu)_**

How could this functionality be used in a penetration test?

**_Plant infected USB drives to gain remote access when employees insert them out of curiosity_**

**Part 2: Cloning a website to Obtain User Credentials**

In this part of the lab, you will create a perfect copy of the login page for a website. The fake login page will gather all credentials submitted to it and then redirect the user to the real website.

**Step 1: Investigate Web Attack Vectors in SET.**

- From the Social-Engineering Attacks submenu, choose **2) Website Attack Vectors** to begin the web site cloning exploit.
- Review the brief attack description of each type of attack.

Which type of attack will you choose to create a cloned website to obtain login credentials for users on the target network?

**_Option 2 - Website Attack Vectors (then inside that menu, Option 3 - Credential Harvester Attack Method, then Option 2 - Site Cloner)_**

Select **3) Credential Harvester Attack Method** from the menu. A description of the ways to configure this exploit is displayed.

Which method enables you to use a custom website for the exploit that you create?

**_ption 3 - Custom Import (This allows you to import your own HTML file instead of cloning a live site)_**

**Step 2: Clone the DVWA.vm Login Screen.**

In this step, you will create a cloned website that duplicates the DVWA.vm login website. The SET application creates a website hosted on your Kali Linux computer. When the target users enter their credentials in the cloned website, the credentials and the users will be redirected to the real website without being aware of the exploit. This is similar to an on-path attack.

- In this lab, we are using the internal website hosted on the DVWA.vm virtual machine. To see what the website looks like, open the Kali Firefox browser, and enter the URL **<http://DVWA.vm/>**. The login screen will appear. If the URL is not found, enter <http://10.6.6.13/> to access the web server using its IP address.

What is the URL of the login screen?

**_10.6.6.13/login.php_**

**_<http://DVWA.vm/>_**

- Return to the terminal session. Select **2) Site Cloner** from the **Credential Harvester Attack Method** menu. Information describing which IP address is needed to host the fake website and to receive the POST data is displayed. Enter the web attacker IP address at the prompt. This is the IP address of the virtual Kali internal interface on the 10.6.6.0/24 network. In an actual exploit, this would be the external (internet facing) address of the attack computer.
- At the prompt, enter the IP address **10.6.6.1**.
- Next, enter the URL of the website that you want to clone. This is the URL of the DVWA website, **<http://DVWA.vm>**.
- When the website is cloned, the following message appears on the terminal.

**Note**: No prompt will be returned to you. This is because a listener is now active on port 80 on the Kali computer and all port 80 traffic will be redirected to this screen. Do not close the terminal window. Continue to Part 3.

**Part 3: Capturing and Viewing User Credentials**

**Step 1: Create the Social Engineering Exploit.**

In a "real-life" exploit, at this point, a phishing exploit containing a link or QR code that sends the user to the fake website is created and sent. In this lab, an html document is created to direct the user to the fake webpage. This document simulates a distributed phishing URL. It could be distributed as a file attachment in phishing emails.

- Open the Kali Linux Mousepad text editor using the **Applications > Favorites > Text Editor** choice from the menu. Enter the HTML code shown into the Mousepad document.

**&lt;html&gt;**

**&lt;head&gt;**

**&lt;meta http-equiv="refresh" content="0; url=<http://10.6.6.1/>" /&gt;**

**&lt;/head&gt;**

**&lt;/html&gt;**

- Select **File > Save** from the Mousepad menu. Name the document **Great_link.html** and save it in the **/home/kali/Desktop** Folder. The icon appears on the Kali desktop.
- Close the Mousepad application.

**Step 2: Capture User Credentials.**

The purpose of the cloned website is to present a web page that looks identical to the one that the user is expecting. A good hacker would create a fake URL that would be very similar to the actual URL, so that unless the user inspects the URL very closely, it would go unnoticed.

- Double-click the desktop icon for the **Great_link.html** page. The DVWA login page that you viewed in **Part 2, Step 2a** should appear in a browser window.

What URL appears on the browser now? Is it the same as the URL you recorded in Part 2, Step 2a?

**_10.6.6.1_**

- Enter some information in the Username and Password fields and click **Login** to send the form.

Username: **<some.user@gmail.com>**

Password: **Pa55w0rdd!**

What is the URL after you entered the information and clicked the Login button? Is it the same as the URL you recorded in Part 2, Step 2a?

&nbsp;**_Yes, it redirects back to the real site_**

What happened?

**_After entering credentials on the fake cloned website and clicking Login, the credentials were captured by the Social Engineer Toolkit (SET) running on the attacker's machine (10.6.6.1). The terminal output shows the captured username and password fields. The victim was then likely redirected to the real DVWA website without realizing their credentials were stolen._**

---
**Step 3: View the Captured Information.**

- Return to the terminal session that is running the SET application. Output from the login attempt should appear, similar to what is shown:

\[\*\] WE GOT A HIT! Printing the output:

POSSIBLE USERNAME FIELD FOUND: username=<some.user@gmail.com>

POSSIBLE PASSWORD FIELD FOUND: password=Pa55w0rdd!

POSSIBLE USERNAME FIELD FOUND: Login=Login

POSSIBLE USERNAME FIELD FOUND: user_token=69c0375a6ee98b96a5b643eed1e97f94

\[\*\] WHEN YOU'RE FINISHED, HIT CONTROL-C TO GENERATE A REPORT.

---
- To save the report in XML format to use in other penetration testing applications, enter **CTRL**\-**C**. The report file name and path are returned. Select the path and filename and right-click to copy the selection.

Continue to enter **99** and press **enter** until you have exited setoolkit. To view the content of the XML file, you need to place the filename in double-quotes (") because it contains spaces and special characters. Use the **cat** command to see the information that is saved. The file path shown is the default path for the lab VM when this lab was created.

┌──(root㉿Kali)-\[~\]

└─# **cat /root/.set/reports/YOUR-FILENME**

---
What information did the cloned web page gather?

**_Username, password, login button value, and user_token_**

What could a penetration tester do with this information?

**_Log into the real website, access sensitive data, and launch further attacks_**

How could an ethical hacker use this procedure in a test?

**_Test phishing vulnerability, assess employee security awareness, recommend MFA and training_**
