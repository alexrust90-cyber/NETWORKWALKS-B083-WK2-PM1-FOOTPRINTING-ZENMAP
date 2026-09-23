<div align="center">
 
PENETRATION TESTING REPORT

FOOTPRINTING, NETWORK SCANNING AND VULNERABILITY ASSESSMENT/ANALYSIS PHASES

| Field | Information |
|:---:|:---:|
| Cybersecurity Professional | Alexandra Rustamova |
| Program/Batch | B083-Networkwalks |
| Date | 17 September 2026 |
| Modules Completed | W2-PM1 Footprinting with multiple Kali tools<br>W2-PM2: GHDB based Footprinting Attacks<br>W2-PM3: Maltego based Footprinting Attacks<br>W2-PM4: theHarvester based Footprinting Attacks<br>W2-PM5 Zenmap based Network Scanning |
| Client/Target | 1. Networkwalks (secured with permission already)<br>2. Microsoft.com (Target domain specified in the theHarvester training exercise for passive reconnaissance)<br>3. My own local LAN Network |
| Permission secured from client? | Yes |
| Phases covered | Phase 1. Reconnaissance and Footprinting<br>Phase 2. Scanning and Network Discovery<br>Phase 3. Vulnerability Assessment/Analysis<br>4-5. In Progress |

</div>

---

### **1. LIABILITY DISCLAIMER**

I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.   

### **2. INTRODUCTION**

This report documents my Week 2 work as part of my ongoing internship program at Networkwalks. It covers several network security and reconnaissance activities, including footprinting the `networkwalks.com` domain using multiple Kali Linux tools (W2-PM1), scanning my own local network using Zenmap (W2-PM5), and additional reconnaissance exercises using the Google Hacking Database (GHDB) (W2-PM2), Maltego (W2-PM3), and theHarvester (W2-PM4).

The activities focus on different reconnaissance and information-gathering techniques, from collecting publicly available information about a target to identifying live hosts and services within a network.

For each activity, I documented the commands or actions performed, the results observed, screenshots as evidence, and a short explanation of why the information could be relevant from a security perspective.

### **3. TOOLS USED**

| Tool | Purpose |
|---|---|
| Kali Linux | Operating system used for reconnaissance activities |
| whois | Find who owns the domain, when it was registered, and its name servers |
| whatweb | Fingerprint web technologies (server, CMS, plugins, IP) |
| nslookup | Resolve the domain name to its IP address using DNS |
| curl -I | Read the HTTP response headers of the website |
| wafw00f | Detect whether a Web Application Firewall protects the site |
| dnsrecon | Enumerate all DNS records (NS, MX, SPF, TXT, SRV) |
| exploit-db/GHDB | Used to find specialized Google dorks for discovering publicly indexed information about a target |
| Maltego | Used to visualize and investigate relationships between entities such as domains, email addresses, people and infrastructure |
| theHarvester | Used to collect publicly available information such as email addresses, subdomains, hostnames and IP addresses from multiple sources |
| Zenmap (Nmap GUI) | Scan the local subnet to find live hosts, IPs and MAC addresses |
| Kali Linux Terminal | Used to run networking commands and identify local IP and MAC addresses associated with network interfaces and connected devices |

### **4. ACTIVITIES PERFORMED**

**4.1. Footprinting with multiple Kali tools**

As part of the reconnaissance phase, I analyzed the `networkwalks.com` domain using six different tools available in Kali Linux: **WHOIS, WhatWeb, Nslookup, Curl, Wafw00f, and DNSRecon**. Each tool provided a different perspective of the target, allowing me to gradually build a broader picture of its domain, DNS, and web infrastructure.

I started with **WHOIS**, which provided publicly available registration details and helped identify the domain's name servers. This information gave an initial view of the domain's registration and hosting-related infrastructure.

Next, I ran **WhatWeb** to determine which technologies were being used by the website. Among the technologies identified were **WordPress 7.1** and **WP Download Manager 3.3.58**, as well as additional information that was publicly exposed by the site.

I then used **Nslookup** to perform a DNS lookup and determine the IP address associated with the domain. The lookup returned **192.232.216.135**.

With **Curl**, using the `-I` option, I examined the HTTP response headers returned by the web server. This revealed additional details about the web application and showed that the WordPress REST API endpoint `/wp-json/` was accessible.

After that, I used **Wafw00f** to check for the presence of a Web Application Firewall (WAF). The scan identified **ModSecurity (SpiderLabs)** as the WAF protecting the website.

Finally, I used **DNSRecon** to gather additional DNS information. The enumeration revealed records related to name servers, mail servers, SPF/TXT records, service records, and DNS software.

By combining the results from all six tools, I was able to collect information from several different layers of the target's public-facing infrastructure. This demonstrated how multiple reconnaissance techniques can be used together to build a more complete understanding of a target before moving into the scanning phase.

**4.2. GHDB based Footprinting Attacks**

***Task 1 — Exposed Security Cameras***

For this task, I used the **Google Hacking Database (GHDB)** through Exploit-DB to practice passive reconnaissance using Google search operators, also known as Google dorks. The objective was to identify security cameras that were publicly indexed and accessible from the Internet without directly scanning or interacting with the target systems.

I used GHDB dorks specifically designed to locate exposed camera interfaces and reviewed the search results to determine whether the identified links were accessible. The exercise resulted in **10 publicly accessible camera links**, which I documented together with the corresponding dork used to locate each result.

| N° | Link | Relevant Dork | Username/password (if any) |
|---|---|---|---|
| 1 | https://www.lmc.edu/webcam.htm | intitle:"Webcam" inurl:WebCam.htm | -/- |
| 2 | http://82.127.206.236/axis-cgi/mjpg/video.cgi?resolution=704x480&camera=1&dummy=1620387728755 | inurl:"axis-cgi/mjpg" | -/- |
| 3 | http://109.233.191.130:8080/ | inurl:"view/index.shtml" | -/- |
| 4 | http://80.152.138.183/ViewerFrame?Mode=Motion&Language=0 | intitle:"Network Camera NetworkCamera" | -/- |
| 5 | http://100.37.240.26:93/ViewerFrame?Mode=Motion&Language=4 | intitle:"Network Camera NetworkCamera" | -/- |
| 6 | https://www.skylinewebcams.com/es/webcam/argentina/tierra-del-fuego/ushuaia/plaza-islas-malvinas.html | inurl:webcam site:skylinewebcams.com inurl:roma | -/- |
| 7 | http://139.64.168.120:8080/ | intitle:"webcamXP" inurl:8080 | -/- |
| 8 | http://109.206.96.249:8080/ | inurl:/multi.html intitle:webcam | -/- |
| 9 | http://99.114.240.169:8080/ | inurl:/multi.html intitle:webcam | -/- |
| 10 | http://83.41.12.44/ | intitle:"webcamxp" "Flash JPEG Stream" | -/- |


These findings demonstrate how information unintentionally indexed by search engines can expose Internet-facing devices and provide useful information during the reconnaissance stage of a security assessment.

***Task 2 — Publicly Indexed Mathematics Ebooks***

As a second GHDB exercise, I used Google dorks to identify publicly indexed listings containing downloadable mathematics ebooks in PDF format. Unlike Task 1, which focused on exposed security camera interfaces, this task focused on discovering publicly accessible documents and files.

I recorded **10 relevant listings**, together with the dork used to locate each result. This exercise demonstrated how search-engine operators can be used during reconnaissance to identify files and other information that may be publicly indexed without the need to directly scan the target.

| N° | Link | Relevant Dork | Username/password (if any) |
|---|---|---|---|
| 1 | https://drive.google.com/drive/folders/1dK9v1CnFiLGFVbUlqDk2Dmk-Fc9bPuDn | "math" "ebook" "Google Drive" | -/- |
| 2 | https://www.scribd.com/document/1026430085/Mathematics-Its-Power-and-Utility-10th-Edition-complete-guide | "math" "ebook" "pdf" "free download" | -/- |
| 3 | https://pressbooks.atlanticoer-relatlantique.ca/healthmath/ | "math" "ebook" "pdf" "free download" | -/- |
| 4 | https://www.yumpu.com/en/document/view/63680981/read-ebook-ultimate-guide-to-the-math-act-read-pdf-ebook | "math" "ebook" "pdf" "free download" | -/- |
| 5 | https://www.freebookcentre.net/SpecialCat/Free-Mathematics-Books-Download.html | allintitle:math ebook pdf free download | -/- |
| 6 | https://infobooks.org/free-pdf-books/math/#google_vignette | allintitle:math ebook pdf free download | -/- |
| 7 | https://archive.org/details/AdditionTrueOrFalse_201307/CK_12_Algebra_Explorations__Pre_K_through_Grade_7/ | allintitle:math ebook pdf free download | -/- |
| 8 | https://www.mrbartonmaths.com/resources/keystage3/the-maths-ebook.pdf | allintitle:math ebook pdf free download | -/- |
| 9 | https://www.mrbartonmaths.com/resources/keystage3/the-maths-ebook.pdf | allintitle:math ebook pdf free download | -/- |
| 10 | https://www.ulm.edu.pk/departments/admin/upload/downloads/202110030921.pdf | allintitle:math ebook pdf free download | -/- |

Reconnaissance is the first stage of an attack, where public information about a target is gathered before direct interaction. GHDB uses specialized Google dorks to help identify exposed resources such as cameras, directories, login pages, and documents. Because the information is obtained through Google, this technique can be used for passive footprinting and also by defenders to identify and reduce their organization's public exposure.

**4.3. Maltego based Footprinting Attacks**

For this task, I installed and configured Maltego on a Kali Linux and prepared it to run reconnaissance transforms. With authorization from the organization, I used the `networkwalks.com` domain as the target and ran email-related transforms to identify publicly available email addresses associated with the domain. The goal was to practice using Maltego to discover and visualize relationships between a target domain and related information.

<img width="1919" height="899" alt="maltego" src="https://github.com/user-attachments/assets/75e9efdf-21c2-42cc-9202-90368b13e72b" />


The email-related transform was successfully executed against the `networkwalks.com` domain, but it did not produce useful email results. Maltego displayed a warning that a valid Google API engine ID was not configured, which limited the search capability of the transform.

As I was using the free version of Maltego, the available credits and search-engine configuration also limited the scope of the investigation. Therefore, I could not perform a complete email enumeration or confirm that all publicly available email addresses associated with the domain had been identified. The result was documented as a limitation of the exercise rather than as evidence that no email addresses exist.

**4.4. theHarvester based Footprinting Attacks**

In this task, I used **theHarvester** in Kali Linux to practice passive reconnaissance and information gathering from publicly available sources. Using **Baidu** as the selected search engine, I searched for email addresses and subdomains associated with `microsoft.com`, with the result limit set to 1000.

***Command Used***

```bash
theHarvester -d microsoft.com -l 1000 -b baidu
```

This command runs **theHarvester** against the `microsoft.com` domain using **Baidu** as the selected data source.

* `-d microsoft.com` — specifies the target domain.
* `-l 1000` — sets the maximum number of results to 1000.
* `-b baidu` — specifies Baidu as the source for gathering information.

***Multi-Source Search***

To expand the reconnaissance, I also ran theHarvester using all available data sources supported by the tool:

```bash id="0b2f1x"
theHarvester -d microsoft.com -l 50 -b all
```

This command searches for publicly available information related to `microsoft.com` across multiple sources, with the results limited to 50. The output was saved and screenshots were captured as evidence for the report.

 ***Conclusion***

theHarvester demonstrated how publicly available information such as email addresses, subdomains, and hosts can be collected from multiple sources without directly interacting with the target. This type of passive reconnaissance helps security professionals understand an organization's public exposure and identify information that may need to be reviewed or protected.

**4.5. Network Scanning with Zenmap**

For the second activity, I worked with **Zenmap** to examine my local network and identify the devices that were currently active. The task focused on determining my computer's local IP address and subnet, discovering reachable hosts, identifying their IP and MAC addresses, and creating a visual representation of the network.

I began by running the `ipconfig` command in Kali Linux Terminal to obtain my local network configuration, including the IP address and subnet information. Then I used this subnet as the target range in Zenmap and selected the **Ping Scan** profile to check which devices were responding on the network.

The results from the practical exercise showed three active hosts:

* `192.168.56.101`
* `192.168.56.100`
* `192.168.56.1`

The scan also returned three corresponding MAC addresses for the discovered devices.

Once the host discovery process was completed, I used Zenmap's **Topology** feature to visualize the network connections. I enabled the legend to make the diagram easier to interpret and exported the resulting topology as a PDF, following the requirements of the practical exercise.

**5. RISK ANALYSIS/IMPACT**

Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks.

| # | Risk/Finding | Evidence/Observation | Potential impact | Risk Level |
|---|---|---|---|---|
| 1 | Domain registration and infrastructure information exposed | WHOIS revealed GoDaddy as registrar and HostGator/DomainControl as name servers. Registration and expiry dates are also publicly available | Information can support reconnaissance and help attackers understand the domain's infrastructure | 🟢 Low |
| 2 | Web technology information exposed | WhatWeb identified WordPress and WP Download Manager | Attackers may use exposed technology/version information to identify software requiring further security review | 🟠 Medium |
| 3 | Server IP address identifiable | Nslookup resolved the domain to 192.232.216.135 | Provides information about the network location of the web service | 🟢 Low |
| 4 | HTTP technical information exposed | Curl returned HTTP response headers and exposed /wp-json/ | May assist technology fingerprinting and further enumeration | 🟢 Low |
| 5 | WAF technology identifiable | Wafw00f identified ModSecurity (SpiderLabs) | Reveals information about the web application's security architecture | 🟢 Low |
| 6 | DNS infrastructure information exposed | DNSRecon identified DNS, mail, and service-related records | DNS information can help build a broader infrastructure profile | 🟠 Medium |
| 7 | Publicly indexed security camera interfaces identified | GHDB searches identified 10 publicly accessible camera links | Exposed devices may reveal information about systems or environments that should not be publicly accessible | 🟠 Medium |
| 8 | Publicly indexed documents identified | GHDB searches identified 10 publicly accessible mathematics ebook PDF listings | Demonstrates how search engines  can expose publicly indexed files and resources | 🟢 Low |
| 9 | Email enumeration limited by API configuration | Maltego's email-related transform was executed, but the Google API engine ID was not configured and no useful email results were obtained | The exercise demonstrates a reconnaissance limitation rather than a confirmed exposure | 🟢 Low |
| 10 | Public email and subdomain information collected | theHarvester was used with Baidu and multiple sources to collect publicly availbale information related to microsoft.com | Publicly exposed email addresses, subdomains and hosts can contribute to an organization's reconnaissance profile | 🟠 Medium |
| 11 | Multiple live hosts visible on local network | Zenmap identified three live hosts in the example network | Unknown or unauthorized devices may potentially be present on a network | 🟠 Medium |

Risk Level Key

- 🔴 **Critical**
- 🟠 **Medium**
- 🟢 **Low**

The risks listed above are based on observations made during the footprinting and network scanning exercises and should not be considered confirmed vulnerabilities.

These practical activities focused mainly on gathering information and identifying active hosts and services. No exploitation or vulnerability verification was carried out during these modules.

For this reason, findings such as exposed software versions, IP addresses, or DNS records do not necessarily indicate that a system is vulnerable. Additional authorized security testing would be required to determine whether any of these findings could be exploited.

**6. RECOMMENDATIONS**

| #  | Finding                                                    | Recommendation                                                                                                                                                                                                                                |
| -- | ---------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1  | Domain registration and infrastructure information exposed | Enable domain privacy where appropriate and minimize publicly available administrative information that is not required for legitimate purposes.                                                                                              |
| 2  | Web technology information exposed                         | Keep WordPress and all installed plugins updated, remove unused components, and regularly assess exposed software for known vulnerabilities.                                                                                                  |
| 3  | Server IP address identifiable                             | Protect the origin server with appropriate network controls and, where applicable, a reverse proxy or CDN. Restrict direct access to trusted sources where operationally feasible.                                                            |
| 4  | HTTP technical information exposed                         | Review response headers to minimize unnecessary technical disclosure and verify that the publicly accessible `/wp-json/` endpoint exposes only information required by the application.                                                       |
| 5  | WAF technology identifiable                                | Keep ModSecurity and its rulesets properly maintained, regularly review WAF configurations and logs, and validate that security controls are functioning as intended.                                                                         |
| 6  | DNS infrastructure information exposed                     | Review DNS records regularly and remove unnecessary or obsolete entries. Avoid exposing records that unnecessarily disclose internal systems or services.                                                                                     |
| 7  | Multiple live hosts visible on local network               | Maintain an up-to-date inventory of authorized devices, investigate unidentified hosts, and apply appropriate network segmentation and access controls.                                                                                       |
| 8  | Publicly indexed security camera interfaces identified     | Review Internet-facing camera systems and ensure that they require strong authentication and appropriate access controls. Remove unnecessary public exposure and regularly review search-engine indexing for unintentionally exposed devices. |
| 9  | Publicly indexed documents identified                      | Review publicly accessible files and directories to ensure that only intended content is indexed. Remove unnecessary files and use appropriate access controls for resources that should not be publicly available.                           |
| 10 | Maltego email enumeration limited by API configuration     | Configure the required API integrations where authorized and available, or use alternative approved data sources to validate the reconnaissance results. Document tool and API limitations when complete enumeration is not possible.         |
| 11 | Public email and subdomain information collected           | Review publicly exposed email addresses and subdomains regularly. Remove unnecessary or obsolete entries and ensure that exposed accounts and services use appropriate authentication and security controls.                                  |


These recommendations are intended as security-hardening measures based on the information observed during the footprinting and network discovery exercises. The identified findings do not, by themselves, confirm the existence of exploitable vulnerabilities. Their security significance should be assessed in the context of the organization's architecture, configuration, and security requirements, followed by authorized validation where appropriate.

**7. Conclusion**

During **Week 2 of my Cybersecurity & Ethical Hacking internship**, I worked on several areas of the security assessment process, including **footprinting, OSINT, and network scanning**. These activities allowed me to practice gathering publicly available information about organizations and identifying active hosts within a local network.

For the footprinting and reconnaissance activities, I used **WHOIS, WhatWeb, Nslookup, Curl, Wafw00f, DNSRecon, GHDB, Maltego, and theHarvester**. Each tool provided a different type of information, helping me understand how multiple sources and techniques can be combined to build a broader picture of a target's public-facing environment.

I also used **Zenmap** to examine my local network, identify active hosts, collect IP and MAC address information, and generate a network topology. This helped me better understand how network discovery can be used to map devices and understand network structure.

One of the main lessons from this week was the importance of **reconnaissance and information gathering before further security testing**. I also learned that not every piece of publicly available information represents a vulnerability and that findings must be interpreted in context.

Finally, these activities reinforced the importance of **accurate documentation, risk assessment, and authorized testing**. All exercises documented in this report were conducted within the assigned educational and internship scope.


**8. Evidences Collected**

<img width="1920" height="896" alt="whois" src="https://github.com/user-attachments/assets/d1c2755c-00fe-439e-a8c0-d325ce895af3" />
<img width="1920" height="896" alt="whatweb" src="https://github.com/user-attachments/assets/ab3ea5bf-19df-47a3-a831-89f1f372b693" />
<img width="1920" height="896" alt="nslookup" src="https://github.com/user-attachments/assets/14008809-2ed4-4bfa-b9c8-5a77a3eb314d" />
<img width="1920" height="896" alt="curl" src="https://github.com/user-attachments/assets/1cbcb292-4fc5-45cf-9f94-bce92b9f1120" />
<img width="1920" height="896" alt="wafw00f" src="https://github.com/user-attachments/assets/e919c6df-26ba-4f46-b65e-15eb76d5354e" />
<img width="1920" height="896" alt="dnsrecon" src="https://github.com/user-attachments/assets/6983f64c-6e3e-4cd2-b2a0-f5c1a50e02e3" />
<img width="1919" height="895" alt="theHarvester2" src="https://github.com/user-attachments/assets/ed6903fd-52e5-455d-8253-1b7fec793ded" />
<img width="1919" height="899" alt="theHarvester" src="https://github.com/user-attachments/assets/31ac03c8-cd95-4058-b416-8b7b6c7c2095" />
<img width="1920" height="896" alt="zenmap host" src="https://github.com/user-attachments/assets/8f6aa061-ed02-4632-898f-fa277b71e7e3" />
[zenmap topology.pdf](https://github.com/user-attachments/files/32357581/zenmap.topology.pdf)

---

Author 
Alexandra Rustamova
Cybersecurity professional B083
LinkedIn https://www.linkedin.com/in/alexandra-rustamova-631a1439a/

---

Project Information
Program Name: Cybersecurity program at Networkwalks | Week: 02 | Repository: GitHub
  
