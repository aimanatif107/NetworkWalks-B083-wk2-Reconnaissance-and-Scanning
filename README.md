# 🛡️ Penetration Testing Report: Footprinting & Reconnaissance
### W2-PM-FINAL | CYBERSECURITY & ETHICAL HACKING INTERNSHIP

| Project Metadata | Details |
| :--- | :--- |
| **Pentester Name** | Aiman Atif |
| **Program / Batch** | B083 - Networkwalks Cybersecurity Internship |
| **Date** | 18-09-2026 |
| **Modules Completed** | W2-PM1 (Kali Tools), W2-PM2 (GHDB), W2-PM3 (Maltego), W2-PM4 (theHarvester), W2-PM5 (Zenmap) |
| **Client / Target** | 1. `networkwalks.com` (Secured written permission)<br>2. `microsoft.com` (Passive OSINT only)<br>3. Local LAN Network (Owned by tester) |
| **Permission Secured?** | **Yes** (See `LOA-Permission-Letter.pdf` in repository) |
| **Phases Covered** | **Phase 1:** Reconnaissance & Footprinting<br>**Phase 2:** Scanning & Network Discovery |

---

## ⚠️ 1. Liability Disclaimer
I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purposes only. Do not use anything from here to break the law. The instructor, the authors, and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job, and a permanent record. In most countries, unauthorized access is a crime even when nothing is damaged.

---

## 📖 2. Introduction
This report covers the **Footprinting, Reconnaissance, and Network Scanning** phases of a penetration test conducted during Week 2 of the Networkwalks Cybersecurity Internship. 

The objective was to simulate how an attacker moves from gathering passive public information (OSINT) to actively mapping live hosts on a network. Activities include domain fingerprinting, Google Hacking Database (GHDB) dorking, visual link analysis, automated email harvesting, and local subnet discovery. All commands were executed in **Kali Linux** and **Windows (Zenmap)**. Every step below includes the methodology, the result observed, and a short note on why the finding matters from an attacker's point of view.

---

## 🛠️ 3. Tools Used

| Tool | Purpose |
| :--- | :--- |
| **Kali Linux & Windows** | Operating systems used for reconnaissance activities. |
| **WHOIS, whatweb, nslookup, curl, wafw00f, dnsrecon** | (PM1) Fingerprint domain registration, web technologies, IPs, HTTP headers, WAFs, and DNS records. |
| **Google Hacking Database (GHDB)** | (PM2) Passive recon using advanced Google Dorks to find exposed cameras and open directories. |
| **Maltego CE** | (PM3) Visual link analysis and OSINT gathering for email addresses and domain infrastructure. |
| **theHarvester** | (PM4) Automated harvesting of emails, subdomains, and hosts from public search engines and PGP servers. |
| **Zenmap (Nmap GUI)** | (PM5) Active network scanning to find live hosts, IPs, and MAC addresses on the local subnet. |

---

## 🕵️ 4. Activities Performed

### 4.1 Module 1: Footprinting with Multiple Kali Tools
I performed active reconnaissance against the `networkwalks.com` domain using six Kali Linux tools to build a complete infrastructure profile:
*   **WHOIS:** Identified domain registration details, expiry dates, and the hosting provider via Name Servers.
*   **whatweb:** Fingerprinted the web stack, identifying specific CMS versions (e.g., WordPress) and plugins.
*   **nslookup:** Resolved the domain name to its actual hosting IP address.
*   **curl -I:** Inspected HTTP response headers, exposing server banners and hidden API endpoints (e.g., `/wp-json/`).
*   **wafw00f:** Probed the target to detect the presence of a Web Application Firewall (e.g., ModSecurity/Cloudflare).
*   **dnsrecon:** Enumerated the entire DNS footprint, including MX (mail) records, SPF policies, and subdomains.

### 4.2 Module 2: Footprinting with GHDB (Google Hacking)
Using the Exploit-DB Google Hacking Database, I performed completely passive reconnaissance to find sensitive data accidentally indexed by Google:
*   **Task 1 (Cameras):** Used dorks like `intitle:"webcamXP" inurl:8080` to locate 10 live, exposed, and vulnerable security camera feeds accessible without authentication.
*   **Task 2 (Open Directories):** Used dorks like `intitle:"index of" "parent directory" mathematics pdf` to locate 10 open server directories containing downloadable academic PDF ebooks.

### 4.3 Module 3: Footprinting with Maltego
I utilized **Maltego Community Edition** to perform visual link analysis on `networkwalks.com`. By running DNS and WHOIS transforms against the Domain entity, I successfully harvested publicly associated email addresses and mapped the organization's digital relationships.

### 4.4 Module 4: Footprinting with theHarvester
I used `theHarvester` in Kali Linux to automate OSINT gathering against `microsoft.com`:
*   **Task 1:** Queried the **Baidu** search engine with a limit of 1000 results.
*   **Task 2:** Queried **all** supported public sources (PGP servers, Shodan, search engines) with a limit of 50 results to harvest corporate email formats and forgotten subdomains.

### 4.5 Module 5: Network Scanning with Zenmap
Moving to Phase 2 (Scanning), I used **Zenmap** to perform network discovery on my own local LAN:
*   Used Windows `ipconfig` and `getmac` to identify my local subnet (e.g., `192.168.x.0/24`) and MAC address.
*   Executed a **Ping Scan** in Zenmap to discover all live hosts on the network.
*   Documented the IP and MAC addresses of discovered devices and generated a visual **Network Topology PDF**.

---

## ⚠️ 5. Risk Analysis / Impact

Based on the information collected, I identified the following potential risks:

| # | Risk / Finding | Evidence / Observation | Potential Impact | Risk Level |
| :--- | :--- | :--- | :--- | :--- |
| **1** | **Web Technology Exposure** | `whatweb` and `curl` exposed exact CMS and plugin versions. | Attackers can cross-reference versions with CVE databases to launch targeted exploits. | 🟠 Medium |
| **2** | **Exposed Infrastructure** | `dnsrecon` and `nslookup` mapped mail servers and actual IPs. | Allows attackers to bypass proxy protections and target backend infrastructure directly. | 🟠 Medium |
| **3** | **WAF Fingerprinting** | `wafw00f` identified the specific WAF in use. | Attackers can tailor their payloads to bypass the specific firewall rules identified. | 🟢 Low |
| **4** | **Leaked Sensitive Files (GHDB)** | Google Dorks exposed open directories and live security cameras. | Severe privacy breach; internal documents or physical security feeds are accessible to anyone. | 🔴 Critical |
| **5** | **Harvested Emails & Subdomains** | `Maltego` and `theHarvester` found employee emails and dev portals. | Emails are used for targeted Spear-Phishing; subdomains often have weaker security than the main site. | 🟠 Medium |
| **6** | **Rogue/Unknown LAN Devices** | `Zenmap` discovered multiple live hosts on the local subnet. | Unauthorized or compromised devices may be present on the internal network. | 🟠 Medium |

*(Risk Key: 🔴 Critical | 🟠 Medium | 🟢 Low)*

---

## 🛡️ 6. Recommendations

Based on the observations from these activities, I recommend the following security improvements:
1.  **Implement Directory Defanging:** Disable directory listing on all web servers (Apache/Nginx) to prevent GHDB "Index of" dorks from exposing files.
2.  **Mask Server Banners:** Configure web servers and WAFs to strip version numbers from HTTP headers to thwart automated fingerprinting.
3.  **Review Public OSINT Leakage:** Regularly run `theHarvester` and Maltego against your own organization to identify and remove exposed employee emails and forgotten subdomains.
4.  **Secure IoT Devices:** Ensure all network cameras and IoT devices are placed behind a firewall/NAT and require strong, non-default authentication.
5.  **Internal Network Monitoring:** Perform routine internal Nmap/Zenmap scans to maintain an accurate inventory of connected devices and identify rogue hardware.

---

## 📝 7. Conclusion
During Week 2 of the Cybersecurity & Ethical Hacking internship, I completed practical activities covering the critical first phases of a penetration test. 

The exercises demonstrated that **information gathering is the most dangerous phase of an attack** because it is entirely passive and hard to detect. By utilizing tools like GHDB, Maltego, and theHarvester, an attacker can build a comprehensive map of an organization's attack surface without ever triggering an intrusion detection system. Furthermore, transitioning into active scanning with Zenmap highlighted how easily internal networks can be mapped once initial access or physical proximity is achieved.

A core takeaway from this week is that **defenders must think like attackers**. Running these exact same footprinting tools against our own infrastructure is the only way to discover what we are accidentally leaking to the public internet.

---

## 📂 8. Evidences Collected (Repository Structure)

All terminal outputs, screenshots, and generated reports are organized in the following directory structure within this repository:

```text
📦 Week2-Ethical-Hacking-Project
 ┣ 📂 Module1-Kali-Tools
 ┃ ┣ 📂 outputs/          # .txt files of whois, whatweb, dnsrecon, etc.
 ┃ ┗ 📂 screenshots/      # Terminal evidence
 ┣ 📂 Module2-GHDB
 ┃ ┣ 📜 GHDB_Findings.md  # Tables of 10 Cameras & 10 Math PDF Directories
 ┃ ┗ 📂 screenshots/      # Google search & open directory evidence
 ┣ 📂 Module3-Maltego
 ┃ ┗ 📂 screenshots/      # Maltego graph and harvested emails
 ┣ 📂 Module4-theHarvester
 ┃ ┣ 📂 outputs/          # .txt files of Baidu and 'All' source scans
 ┃ ┗ 📂 screenshots/      
 ┣ 📂 Module5-Zenmap
 ┃ ┣ 📜 Zenmap_Topology.pdf # Generated network map
 ┃ ┗ 📂 screenshots/      # ipconfig and Zenmap host discovery evidence
 ┣ 📜 LOA-Permission-Letter.pdf # Signed authorization from Networkwalks
 ┗ 📜 README.md             # This final report
```

<div align="center">
  <h3>👤 Author & Project Information</h3>
  <b>Pentester:</b> Aiman Atif | Cybersecurity Intern<br>
  <b>Program:</b> Networkwalks Cybersecurity Internship (Batch B083)<br>
  <b>Date:</b> 18-09-2026 </div>
