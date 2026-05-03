## Course Title: Ethical Hacking Course #: CS 4069

| **CS 4064** | **Ethical Hacking** | **Lab02** | **Spring 2026** |
| ----------- | ------------------- | --------- | --------------- |
| Name:       | Sarah Eid           |           |                 |
| Student ID: | S22107757           | Section:  | 2               |

**Lab02 - Passive footprinting and reconnaissance on target (authorized)**

**Objective:**

Students perform a passive OSINT-only reconnaissance on the organization abc using publicly available information. No scanning, no exploitation, no login attempts, no form submissions, no direct interaction beyond normal web browsing and public search queries.

**Scope and rules:**\
Target: abc's primary domain and any publicly visible subdomains that appear through open sources.

*Allowed actions:* viewing public web pages, collecting public URLs, using OSINT tools that query third-party sources, downloading publicly available files from abc's site for local metadata analysis.

*Not allowed:* port scanning, directory brute forcing, vulnerability scanning, password guessing, contacting employees, sending emails, interacting with authenticated areas, using aggressive crawling, or any action that could degrade service.

**Tools used (brief overview)**:\
a) theHarvester: collects publicly exposed emails, names, and subdomains from open sources.\
b) Sherlock: checks whether a username exists across common social platforms, useful for correlating public identities.\
c) ExifTool: extracts metadata from public files (PDFs, images) downloaded from abc's public site.\
d) OSINT Framework: a structured map of OSINT sources that helps students choose the next step logically instead of guessing.

**Deploying a Pre-Built Customized Kali VM on AMD or Intel Chip-based Computer**

**Note**: Go to the next part if you have M1/M2 MacOS or other ARM-based devices that can support UTM.

**Step 1: Download and install VirtualBox.**

VMware Workstation Player and VirtualBox are two virtualization programs that you can download and install to run the Kali VM file. In this lab, you will use the VirtualBox application.

a.  Navigate to
    [[https://www.virtualbox.org/]{.underline}](https://www.virtualbox.org/).
    Click the download link on this page.

b.  Choose and download the appropriate installation file based on your
    operating system.

c.  After the VirtualBox installation file is downloaded, run the
    installer and accept the default installation settings.

**Step 2: Download the pre-built customized Kali.**

a.  Navigate to the [[Resource
    Hub]{.underline}](https://skillsforall.com/resources/lab-downloads?courseLang=en-US)
    from skillsforall.com.

b.  Download the OVA file for this course. Note the location of the
    downloaded OVA file on your computer.

**Step 3: Deploy the VM in VirtualBox.**

a.  Open **VirtualBox**.

b.  Click **File** \> **Import Appliance** to import the downloaded OVA
    file, **Kali.ova**. Click **Next** to continue.

c.  Review the appliance settings. Increase the amount of RAM if
    desired. Click **Finish** to continue.

d.  Click **Start** to power up the newly created VM after the appliance
    has been imported.

**Deploying a Pre-Built Customized Kali VM on ARM M1/M2 Chip-based
Computer**

**Note**: Do the previous part if you have an AMD or Intel Chip-based
Computer.

**Step 1: Download and install UTM.**

In this lab, you will use the free version of the UTM app.

a.  Navigate to
    [[https://mac.getutm.app/]{.underline}](https://mac.getutm.app/).
    Click **Download** to download the free version.

b.  After the file is downloaded, install UTM.

**Step 2: Download and load the pre-built customized Kali.**

a.  Navigate to the [[Resource
    Hub]{.underline}](https://skillsforall.com/resources/lab-downloads?courseLang=en-US)
    from skillsforall.com.

b.  Download the Kali.utm.zip file. Note the location of the downloaded
    Kali.utm.zip file.

c.  Unzip the zip archive.

Double-click the unzipped file to open the VM in UTM.

**Passive Reconnaissance:**

**Task 1:** Establish the footprint with theHarvester\
Student does a theHarvester run for abc's domain using one or two approved public sources.\
Student records,

- discovered email addresses (if any), and inferred email format

- discovered hosts or subdomains\
  Outcome: a seed list of subdomains and 3--5 candidate usernames
  derived from emails (for example, j.smith from <j.smith@abc.com>).

theHarvester -d example.com -b all

**Task 2:** plan pivots using OSINT Framework\
Student uses OSINT Framework to choose follow-up paths based on Task 1 outputs.\
Student writes a short plan of 4--6 pivots, for example,

- username research for identified handles

- document and metadata research for files hosted on abc's site

- domain research for public references to subdomains\
  Outcome: a clear, justifiable recon plan.

Using OSINT Framework and Task 1 outcomes:

**Identity Correlation**

- Focus on unique names found in email addresses

- Search these names across social platforms

- Cross-reference for organizational affiliation

**Department Analysis**

- hr@example.com → HR/recruiting department research

- it@example.com → web/IT infrastructure team

- LinkedIn: target organization employees

**Document Metadata Hunt**

- Search example.com for public PDFs:

  - Annual reports

  - Whitepapers

  - Research papers

- Extract author names from documents

**Social Media Correlation**

- Use Sherlock on username candidates

- Focus on LinkedIn, GitHub, Twitter

- Look for organization affiliation in bios

**Task 3:** collect public documents and extract metadata with ExifTool\
Student identifies 2--4 publicly downloadable files from abc's site (press kit PDFs, brochures, images, reports).\
Student downloads them and runs ExifTool locally.\
Student records for each file,

- author/creator, creation and modification dates, software/tool used

- any identifiers or location hints if present\
  Outcome: at least two meaningful pivots, for example, an author name
  that becomes a username candidate, a tool name that suggests a tech
  stack component, or a location hint to validate publicly listed office
  information.

**Task 4:** correlate public identities with Sherlock\
Student takes 3--6 username candidates from Task 1 and Task 3 and checks them with Sherlock.\
Student records only public, non-sensitive findings,

- which platforms show an existing account

- any public evidence connecting the account to abc (bio, employer text,
  public posts)\
  Outcome: a short list of "likely relevant" public profiles, clearly
  labeled as confirmed or unconfirmed.

**Final deliverable:** reconnaissance summary (1--2 pages)\
Students submit a concise report containing,

- domain map: main domain plus key discovered subdomains, with a
  one-line likely purpose each

- email pattern: inferred format and any discovered emails (plus clearly
  labeled hypotheses)

**Email Pattern**

**Inferred Format:** first.last@example.com (e.g., jane.doe@example.com)\
**Regional
Variations:** first.last@[country].example.com (e.g., @uk.example.com)\
**Discovered Emails (Sample):**

- jane.doe@example.com

- john.smith@example.com

- hr@example.com (HR/recruitment)

- it@example.com (web/IT team)

- people and usernames: correlated handles and public evidence, labeled
  as confirmed or unconfirmed

- metadata highlights: the top metadata findings from ExifTool and what
  each suggests

1.  **Adobe InDesign 17.1 (Macintosh)** -- Creator software\
    *Suggests:* The organization's marketing/design team uses Adobe Creative Cloud
    on macOS for professional document creation.

2.  **Encryption: Standard V5.6 (256-bit)** -- PDF security\
    *Suggests:* Corporate documents with sensitivity, likely internal-facing but
    shared publicly with protection.

3.  **AVIF Image Format** -- Modern web image type\
    *Suggests:* Organization web/development teams use next-gen,
    performance-optimized image formats for faster loading.

- next validation steps: 5 passive-only steps that would be appropriate
  for the next recon phase (no scanning)

**Next Validation Steps (Passive Only)**

1.  LinkedIn search for target organization employees with discovered email patterns

2.  GitHub search for organization-related repositories by discovered usernames

3.  Google Alerts for new [example.com](https://example.com/) domain registrations
