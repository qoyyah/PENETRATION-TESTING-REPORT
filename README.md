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

**Risk level key: ● Critical ● Medium ● Low**

The findings outlined above are based on observations made during the footprinting and network scanning exercises and should not be interpreted as verified security vulnerabilities.

The practical exercises primarily involved information gathering and host discovery. No exploitation or vulnerability validation was performed as part of these two modules.

Therefore, the presence of information such as a software version, IP address or DNS record does not by itself mean that the system is vulnerable. Further authorized security testing would be required to confirm any actual vulnerability.

# 6. Recommended Security Improvement

Based on the findings gathered during these exercises, the following security measures are recommended to strengthen the overall security posture:

1. **Monitor Publicly Available Technology Information**  
   Organizations should periodically assess the technical information exposed about their websites, content management systems (CMS) and installed plugins.

2. **Ensure Regular Software Updates**  
   CMS platforms, plugins and other web technologies should be kept up to date and checked regularly against relevant security advisories.

3. **Review HTTP Response Headers**  
   HTTP response headers should be assessed to identify and minimize the exposure of unnecessary technical details.

4. **Conduct Regular DNS Record Reviews**  
   DNS configurations should be reviewed periodically to ensure that only necessary records and services are publicly accessible.

5. **Strengthen Web Application Firewall Configuration**  
   The existing Web Application Firewall (ModSecurity) should remain enabled, properly configured, and regularly monitored to help detect and block malicious traffic.

6. **Conduct Routine Internal Network Scanning**  
   Organizations should perform periodic network discovery scans to identify active devices and maintain visibility across their internal networks.

7. **Verify Unrecognized Network Devices**  
   Any unfamiliar or unexpected devices identified during network scans should be investigated to confirm their legitimacy and authorization.

8. **Keep Network Documentation Updated**  
   Network diagrams, device inventories and configuration details should be properly documented and reviewed regularly.

9. **Ensure Proper Authorization for Security Testing**  
   All reconnaissance, network scanning, and security assessment activities must be conducted only on systems and networks for which explicit authorization has been obtained.

# 7. Conclusion

During Week 2 of my Cybersecurity and Ethical Hacking internship at Networkwalks, I completed hands-on exercises focused on domain **footprinting**, **reconnaissance** & **network scanning.**

As part of the footprinting exercise, I worked with six Kali Linux tools to gather and examine information about the target domain. I gained practical knowledge of how **WHOIS** retrieves domain registration details, **WhatWeb** identifies web technologies, **Nslookup** performs DNS resolution, **Curl** examines HTTP response headers, **Wafw00f** detects Web Application Firewalls, and **DNSRecon** gathers information about DNS infrastructure.

For the network scanning exercise, I used **Zenmap** to examine my local network configuration and identify active hosts. I also explored how to retrieve IP and MAC address information and represent discovered devices through a network topology.

These exercises reinforced my understanding of the importance of information gathering in cybersecurity. I learned that security professionals can obtain valuable insights into a system or network by analysing publicly available information and network responses, even before conducting any vulnerability assessment or exploitation.

Another important lesson was the value of proper technical documentation. Effective cybersecurity reporting requires clearly explaining the procedures performed, findings obtained, their potential security implications and appropriate recommendations for addressing identified risks.

Above all, these activities strengthened my understanding of the ethical and legal responsibilities associated with cybersecurity. **Reconnaissance** and **network scanning ** must always be conducted within an authorized scope and in compliance with applicable security guidelines. All activities documented in this report were undertaken as part of the assigned educational exercises.

Overall, Week 2 provided valuable hands-on experience and strengthened my foundational knowledge of reconnaissance, DNS enumeration and network discovery as I continue developing my practical cybersecurity skills.

# 8. Evidences Collected

*Screenshots collected as evidence during the activities (stored in the `screenshots/` folder):*

<img width="1135" height="849" alt="whois output" src="https://github.com/user-attachments/assets/a62daf4e-f857-497b-b515-adc6d344ee8b" />

<img width="1120" height="454" alt="whatweb output" src="https://github.com/user-attachments/assets/52679bb8-8f6d-4a29-a49d-db3fe9871e11" />

<img width="940" height="568" alt="nslookup output" src="https://github.com/user-attachments/assets/052d043e-782c-4aa1-98a7-9171d8ae5cfe" />

<img width="1108" height="553" alt="curl -I output" src="https://github.com/user-attachments/assets/8e709121-4870-4704-bf68-86d183296c7f" />

<img width="1122" height="712" alt="wafw00f output" src="https://github.com/user-attachments/assets/7657c101-96d8-4aae-b911-f635d703e78f" />

<img width="1147" height="484" alt="dnsrecon output" src="https://github.com/user-attachments/assets/d463c46d-974a-4acd-ae15-63da7ee5d2cb" />

<img width="1278" height="744" alt="Zenmap scan and topology" src="https://github.com/user-attachments/assets/3ed1363b-0264-4e05-b025-d0b19b0d8fdc" />

<img width="715" height="616" alt="host scan output" src="https://github.com/user-attachments/assets/904e32d9-6830-451a-acab-6be302dd78da" />

-End-

👤 Author
Rukayat Sodiq
Cybersecurity Professional B084
linkedin.com/in/alaorukayatifeoluwa

----

📌 **Project Information**
**Program Name:** Cybersecurity program at Networkwalks | Week: 02 | Repository: GitHub

