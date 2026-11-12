# PENETRATION-TESTING-REPORT
FOOTPRINTING &amp; NETWORK SCANNING PHASES

**W2-PM1 and W2-PM5-FINAL  |  CYBERSECURITY  |  NETWORKWALKS**

| Field | Detail |
|---|---|
| **Pentester Name (Cybersecurity Professional)** | **Rukayat Sodiq** |
| **Program/Batch** | B084-Networkwalks |
| **Date** | 12 November 2026 |
| **Modules completed** | W2-PM1 (Multiple Kali Tools)<br>W2-PM5 (Zenmap Scanning) |
| **Client/Target** | 1. Networkwalks (secured written permission already)<br>2. My own local LAN Network |
| **Permission secured from client?** | Yes |
| **Phases covered** | **Phase 1:** Reconnaissance & Footprinting<br>**Phase 2:** Scanning & Network Discovery<br>**Phase 3-5:** In Progress |

# 1. Liability Disclaimer

All practical activities documented in this project were conducted exclusively on systems and devices that I personally own or for which I obtained explicit written authorization to perform security testing.

The information, tools, techniques and materials presented are intended strictly for educational, training and research purposes. They must not be used for unlawful activities, unauthorized access, or any form of malicious exploitation.

The instructor, content authors and Networkwalks shall not be held responsible for any misuse of the knowledge or techniques shared throughout this training. Every individual is solely responsible for their actions and how they apply the information acquired.

Unauthorized access to computer systems is a criminal offence in many jurisdictions, regardless of whether damage occurs. Violations may result in criminal prosecution, substantial financial penalties, loss of employment and a permanent criminal record.

Always prioritize ethical conduct, obtain proper authorization and comply with applicable cybersecurity laws and regulations before conducting any security assessment.

# 2. Introduction

This report documents two practical cybersecurity exercises completed during Week 2 of my ongoing internship programme at Networkwalks. The first exercise (W2-PM1) focuses on performing domain footprinting on networkwalks.com using various Kali Linux tools, while the second exercise (W2-PM5) involves scanning my own local network using Zenmap.

These exercises cover two important stages of the cybersecurity assessment process: footprinting and network scanning. Together, they demonstrate how information gathering can progress from collecting publicly available details about a domain to identifying and mapping active hosts within a network.

This project forms part of my continued hands-on learning and practical development throughout the Networkwalks internship programme.

# 3. Tools Used

The table below lists each tool used in this report and its purpose.

| Tool | Purpose |
|---|---|
| Kali Linux & Windows | Operating systems utilized for conducting reconnaissance and information-gathering activities.             |
| WHOIS                | Retrieves domain ownership and registration information..   |
| whatweb              | Identifies web technologies, IP, servers, CMS platforms and plugins.         |
| NSLookup             | Retrieves a domain's IP address through DNS queries.             |
| curl -I              | Read the HTTP response headers of the website.                   |
| WAFW00F              | Identifies whether a website is protected by a Web Application Firewall.     |
| DNSRecon             | Discovers and analyses DNS records, including NS, MX, SPF, TXT, and SRV.               |
| Zenmap (Nmap GUI)    | Scan the local subnet to find live hosts, IPs and MAC addresses. |
| Windows CMD          | Local IP and MAC address identification                          |

# 4. Practical Exercises Performed

## 4.1 Footprinting & Reconnaissance

I conducted domain reconnaissance on **networkwalks.com** using six Kali Linux tools: **WHOIS**, **WhatWeb**, **Nslookup**, **Curl**, **Wafw00f**, and **DNSRecon**. Each tool helped gather specific information about the target domain from a different perspective.

I began by using **WHOIS** to retrieve publicly accessible domain registration details, including the domain's name servers. This provided useful insights into its registration records and hosting infrastructure.

I proceeded with **WhatWeb** to examine the website's technology stack. The scan revealed WordPress 7.1.4 and WP Download Manager 3.3.76, alongside other publicly accessible technical details.

Next, I used **Nslookup** to perform a **DNS query** and retrieve the domain's corresponding IP address, which resolved to **192.232.216.135**.

I used **Curl** with the **-I** **flag** to examine the website's HTTP response headers. This revealed additional technical details about the web application, including the publicly accessible WordPress REST API endpoint **/wp-json/**.

I then ran **Wafw00f** to check for the presence of a Web Application Firewall **(WAF)**. The scan detected **ModSecurity (SpiderLabs)** as the security technology protecting the website.

Finally, I performed **DNS enumeration** using **DNSRecon** to gather details about the domain's DNS infrastructure. The results revealed information about its name servers, mail servers, SPF/TXT records, 8 service records were found and DNS software.

## 4.2 Network Scanning with Zenmap

For the second exercise, I used **Zenmap** to conduct network discovery on my local network. The objective was to determine my local IP address and subnet, identify active hosts, retrieve their corresponding IP and MAC addresses and generate a visual representation of the network topology.

I began by running the Windows **ip addr** command to obtain my local IP address and **LAN subnet** information . 

I subsequently ran **ip route** to confirm the network routing information and default gateway. After identifying the **subnet**, I entered it into **Zenmap** and selected the Ping Scan option to detect active devices connected to the network.

The practical's example scan results revealed two active hosts with the following IP addresses:

10.0.0.1

10.0.0.2

Additionally, the scan results displayed two corresponding MAC addresses, providing further information about the devices identified on the network.

# 5. Risk Analysis / Impact

Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks.

| **\#** | **Risk / Finding**                           | **Evidence / Observation**                                  | **Potential Impact**                                                                                            | **Risk Level** |
|--------|----------------------------------------------|-------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|----------------|
| 1      | Exposure of Web Technology Details           | WhatWeb detected WordPress and WP Download Manager.      | Could help attackers identify software components that may require further security assessment. | **● Medium**   |
| 2      | Publicly Identifiable Server IP               | NSLookup resolved the domain to `192.232.216.135`           | Provides information about the network location of the web service                                              | **● Low**      |
| 3      | HTTP technical information exposed           | Curl returned HTTP response headers and exposed `/wp-json/` | May assist technology fingerprinting and further enumeration                                                    | **● Low**      |
| 4      | WAF technology identifiable                  | Wafw00f identified ModSecurity (SpiderLabs)                 | Reveals information about the web application’s security architecture                                           | **● Low**      |
| 5      | DNS infrastructure information exposed       | DNSRecon identified DNS, mail and service-related records   | DNS information can help build a broader infrastructure profile                                                 | **● Medium**   |
| 6      | Multiple live hosts visible on local network | Zenmap identified four live hosts in the example network    | Unknown or unauthorized devices may potentially be present on a network                                         | **● Medium**   |

**Risk level key:** ● Critical ● Medium ● Low
