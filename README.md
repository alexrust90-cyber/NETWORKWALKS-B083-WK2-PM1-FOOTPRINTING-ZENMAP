<div align="center">
 
PENETRATION TESTING REPORT

FOOTPRINTING AND NETWORK SCANNING PHASES

| Field | Information |
|:---:|:---:|
| Cybersecurity Professional | Alexandra Rustamova |
| Program/Batch | B083-Networkwalks |
| Date | 17 September 2026 |
| Modules Completed | W2-PM1 Footprinting with multiple Kali tools<br>W2-PM2: GHDB based Footprinting Attacks<br>W2-PM3: Maltego based Footprinting Attacks<br>W2-PM4: theHarvester based Footprinting Attacks<br>W2-PM5 Zenmap based Network Scanning |
| Client/Target | 1. Networkwalks (secured with permission already)<br>2. My own local LAN Network |
| Permission secured from client? | Yes |
| Phases covered | Phase 1. Reconnaissance and Footprinting<br>Phase 2. Scanning and Network Discovery<br>Phase 3-5. In Progress |

</div>

---

**1. LIABILITY DISCLAIMER**

I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.   

**2. INTRODUCTION**

This report documents my Week 2 work as part of my ongoing internship program at Networkwalks. It covers two related areas of network security: footprinting the `networkwalks.com` domain using multiple Kali Linux tools (W2-PM1), and scanning my own local network using Zenmap (W2-PM5).
  
The two modules focus on different stages of the process. The first focuses on gathering publicly available information about a target, while the second focuses on identifying live hosts and services within a network. Together, they demonstrate how an attacker can move from initial information gathering to building a clearer picture of the target environment.
  
For both activities, I used Kali Linux. Each step in the report includes the exact command or action performed, the result I observed, a screenshot as evidence, and a short explanation of why the finding could be relevant from an attacker's perspective.

**3. TOOLS USED**

| Tool | Purpose |
|---|---|
| Kali Linux | Operating system used for reconnaissance activities |
| whois | Find who owns the domain, when it was registered, and its name servers |
| whatweb | Fingerprint web technologies (server, CMS, plugins, IP) |
| nslookup | Resolve the domain name to its IP address using DNS |
| curl -I | Read the HTTP response headers of the website |
| wafw00f | Detect whether a Web Application Firewall protects the site |
| dnsrecon | Enumerate all DNS records (NS, MX, SPF, TXT, SRV) |
| Zenmap (Nmap GUI) | Scan the local subnet to find live hosts, IPs and MAC addresses |
| Kali Linux Terminal | Used to run networking commands and identify local IP and MAC addresses associated with network interfaces and connected devices |

**4. ACTIVITIES PERFORMED**

**4.1. Footprinting and Reconnaissance**

As part of the reconnaissance phase, I analyzed the `networkwalks.com` domain using six different tools available in Kali Linux: **WHOIS, WhatWeb, Nslookup, Curl, Wafw00f, and DNSRecon**. Each tool provided a different perspective of the target, allowing me to gradually build a broader picture of its domain, DNS, and web infrastructure.

I started with **WHOIS**, which provided publicly available registration details and helped identify the domain's name servers. This information gave an initial view of the domain's registration and hosting-related infrastructure.

Next, I ran **WhatWeb** to determine which technologies were being used by the website. Among the technologies identified were **WordPress 7.1** and **WP Download Manager 3.3.58**, as well as additional information that was publicly exposed by the site.

I then used **Nslookup** to perform a DNS lookup and determine the IP address associated with the domain. The lookup returned **192.232.216.135**.

With **Curl**, using the `-I` option, I examined the HTTP response headers returned by the web server. This revealed additional details about the web application and showed that the WordPress REST API endpoint `/wp-json/` was accessible.

After that, I used **Wafw00f** to check for the presence of a Web Application Firewall (WAF). The scan identified **ModSecurity (SpiderLabs)** as the WAF protecting the website.

Finally, I used **DNSRecon** to gather additional DNS information. The enumeration revealed records related to name servers, mail servers, SPF/TXT records, service records, and DNS software.

By combining the results from all six tools, I was able to collect information from several different layers of the target's public-facing infrastructure. This demonstrated how multiple reconnaissance techniques can be used together to build a more complete understanding of a target before moving into the scanning phase.

**4.2. Network Scanning with Zenmap**

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
| 7 | Multiple live hosts visible on local network | Zenmap identified three live hosts in the example network | Unknown or unauthorized devices may potentially be present on a network | 🟠 Medium |

Risk Level Key

- 🔴 **Critical**
- 🟠 **Medium**
- 🟢 **Low**

The risks listed above are based on observations made during the footprinting and network scanning exercises and should not be considered confirmed vulnerabilities.

These practical activities focused mainly on gathering information and identifying active hosts and services. No exploitation or vulnerability verification was carried out during these modules.

For this reason, findings such as exposed software versions, IP addresses, or DNS records do not necessarily indicate that a system is vulnerable. Additional authorized security testing would be required to determine whether any of these findings could be exploited.

**6. RECOMMENDATIONS**

| # | Finding                                                    | Recommendation                                                                                                                                                                          |
| - | ---------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 | Domain registration and infrastructure information exposed | Enable domain privacy where appropriate and minimize publicly available administrative information that is not required for legitimate purposes.                                        |
| 2 | Web technology information exposed                         | Keep WordPress and all installed plugins updated, remove unused components, and regularly assess exposed software for known vulnerabilities.                                            |
| 3 | Server IP address identifiable                             | Protect the origin server with appropriate network controls and, where applicable, a reverse proxy or CDN. Restrict direct access to trusted sources where operationally feasible.      |
| 4 | HTTP technical information exposed                         | Review response headers to minimize unnecessary technical disclosure and verify that the publicly accessible `/wp-json/` endpoint exposes only information required by the application. |
| 5 | WAF technology identifiable                                | Keep ModSecurity and its rulesets properly maintained, regularly review WAF configurations and logs, and validate that security controls are functioning as intended.                   |
| 6 | DNS infrastructure information exposed                     | Review DNS records regularly and remove unnecessary or obsolete entries. Avoid exposing records that unnecessarily disclose internal systems or services.                               |
| 7 | Multiple live hosts visible on local network               | Maintain an up-to-date inventory of authorized devices, investigate unidentified hosts, and apply appropriate network segmentation and access controls.                                 |

These recommendations are intended as security-hardening measures based on the information observed during the footprinting and network discovery exercises. The identified findings do not, by themselves, confirm the existence of exploitable vulnerabilities. Their security significance should be assessed in the context of the organization's architecture, configuration, and security requirements, followed by authorized validation where appropriate.

**7. Conclusion**

During **Week 2 of my Cybersecurity & Ethical Hacking internship**, I worked on two key areas of the security assessment process: **footprinting and network scanning**. The activities allowed me to practice gathering information about a public-facing domain and identifying active hosts within a local network.

For the footprinting activity, I used **WHOIS, WhatWeb, Nslookup, Curl, Wafw00f, and DNSRecon**. Each tool provided a different type of information, including domain registration details, web technologies, IP addresses, HTTP responses, WAF technology, and DNS infrastructure. Working with multiple tools helped me understand how individual findings can be combined to build a broader picture of a target's public-facing environment.

For the network scanning activity, I used **Zenmap** to examine my local network, identify active hosts, collect IP and MAC address information, and generate a network topology. This helped me understand how network discovery can be used to map devices and better understand the structure of a network.

One of the main lessons from this week was the importance of **reconnaissance and information gathering before conducting further security testing**. Information such as DNS records, software technologies, network addresses, and active hosts can provide useful context for understanding an environment and identifying areas that may require additional security review.

I also learned the importance of **accurate documentation and risk assessment**. Not every piece of exposed information represents a vulnerability, so findings need to be interpreted in context and clearly distinguished from confirmed security issues. Documenting the observation, potential impact, risk level, and recommended mitigation provides a structured way to communicate security findings.

Finally, these activities reinforced the importance of performing reconnaissance and scanning **only within an authorized scope**. All exercises documented in this report were conducted as part of the assigned educational cybersecurity lab and internship activities.

**8. Evidences Collected**

<img width="1920" height="896" alt="whois" src="https://github.com/user-attachments/assets/d1c2755c-00fe-439e-a8c0-d325ce895af3" />
<img width="1920" height="896" alt="whatweb" src="https://github.com/user-attachments/assets/ab3ea5bf-19df-47a3-a831-89f1f372b693" />
<img width="1920" height="896" alt="nslookup" src="https://github.com/user-attachments/assets/14008809-2ed4-4bfa-b9c8-5a77a3eb314d" />
<img width="1920" height="896" alt="curl" src="https://github.com/user-attachments/assets/1cbcb292-4fc5-45cf-9f94-bce92b9f1120" />
<img width="1920" height="896" alt="wafw00f" src="https://github.com/user-attachments/assets/e919c6df-26ba-4f46-b65e-15eb76d5354e" />
<img width="1920" height="896" alt="dnsrecon" src="https://github.com/user-attachments/assets/6983f64c-6e3e-4cd2-b2a0-f5c1a50e02e3" />
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
  
