# PENETRATION-TESTING-REPORT-FOOTPRINTING-NETWORK-SCANNING-PHASES
| Pentester Name (Cybersecurity Professional) | Dominic Joshua |
|---|---|
| **Program/Batch** | B083-Networkwalks |
| **Date** | 16 september 2026 |
| **Modules completed** | W2-PM1 (Multiple Kali Tools)<br>W2-PM5 (Zenmap Scanning) |
| **Client/Target** | 1. Networkwalks (secured written permission already)<br>2. My own local LAN Network |
| **Permission secured from client?** | Yes |
| **Phases covered** | Phase 1: Reconnaissance & Footprinting<br>Phase 2: Scanning & Network Discovery<br>Phase 3-5: In Progress |

## 1. Liability Disclaimer
I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.

## 2. Introduction
This report covers footprinting the networkwalks.com domain using multiple Kali Linux tools (W2-PM1) and scanning my own local network with Zenmap (W2-PM5). One module covers the footprinting phase and the other covers the scanning phase, so together they show how an attacker moves from gathering public information to mapping live hosts on a network. It is the Week 2 part of my ongoing internship program at Networkwalks.
All commands were run in Kali Linux (footprinting) and on a Windows PC with Zenmap installed (scanning). Every step below includes the exact command used, the result I observed, a screenshot as evidence, and a short note on why the finding matters from an attacker's point of view.

## 3. Tools Used


The table below lists each tool used in this report and its purpose.

| Tool | Purpose |
|---|---|
| Kali Linux & Windows | Operating systems used for reconnaissance activities |
| WHOIS | Find domain registration details (owner, dates, name servers) |
| whatweb | Fingerprint web technologies (server, CMS, plugins, IP) |
| nslookup | Resolve the domain name to its IP address using DNS |
| curl -l | Read the HTTP response headers of the website |
| wafw00f | Detect whether a Web Application Firewall protects the site |
| dnsrecon | Enumerate all DNS records (NS, MX, SPF, TXT, SRV) |
| Zenmap (Nmap GUI) | Scan the local subnet to find live hosts, IPs and MAC addresses |
| Windows CMD | Local IP and MAC address identification |


# 4. Activities Performed
## 4.1 Footprinting & Reconnaissance

I performed reconnaissance against the networkwalks.com domain using six Kali Linux tools: WHOIS, WhatWeb, Nslookup, Curl, Wafw00f and DNSRecon. Each tool was used to collect a different type of information about the target.
First, I used WHOIS to obtain publicly available domain registration information and identify the domain’s name servers. The results provided information about the domain registration and hosting infrastructure.
I then used WhatWeb to identify technologies used by the website. The results identified WordPress 7.0.4 and WP Download Manager 3.3.58, along with other information exposed by the website.
Using Nslookup, I resolved the domain name to its IP address. The provided result identified 192.232.216.135.
4.2 Network Scanning with Zenmap
For the second activity, I used Zenmap to perform network discovery on my local network. The practical required me to identify my local IP address and subnet, discover live hosts, identify their IP and MAC addresses, and generate a network topology.
I first used the Windows ipconfig command to identify my local IP address and LAN subnet. I then entered the subnet into Zenmap and selected Ping Scan to identify active hosts.
The example results provided in the practical identified one live hosts:
192.168.2.1
The example results also included four MAC addresses.
After completing the scan, I opened the Topology section in Zenmap, enabled the legend and saved the network topology in PDF format as required by the practical task.
<h2>5. Risk Analysis / Impact</h2>

<p>Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks.</p>

<table style="width: 100%; border-collapse: collapse; background-color: #e8e0d5;">
<tr style="background-color: #a89968; color: white;">
<th style="border: 1px solid #999; padding: 12px; text-align: left; font-weight: bold;">#</th>
<th style="border: 1px solid #999; padding: 12px; text-align: left; font-weight: bold;">Risk / Finding</th>
<th style="border: 1px solid #999; padding: 12px; text-align: left; font-weight: bold;">Evidence / Observation</th>
<th style="border: 1px solid #999; padding: 12px; text-align: left; font-weight: bold;">Potential Impact</th>
<th style="border: 1px solid #999; padding: 12px; text-align: left; font-weight: bold;">Risk Level</th>
</tr>

<tr style="background-color: #f5f1e8;">
<td style="border: 1px solid #999; padding: 12px;">1</td>
<td style="border: 1px solid #999; padding: 12px;">Web technology information exposed</td>
<td style="border: 1px solid #999; padding: 12px;">WhatWeb identified WordPress and WP Download Manager</td>
<td style="border: 1px solid #999; padding: 12px;">Attackers may use exposed technology/version information to identify software requiring further security review</td>
<td style="border: 1px solid #999; padding: 12px; text-align: center;">🟠 <strong>Medium</strong></td>
</tr>

<tr style="background-color: #f5f1e8;">
<td style="border: 1px solid #999; padding: 12px;">2</td>
<td style="border: 1px solid #999; padding: 12px;">Server IP address identifiable</td>
<td style="border: 1px solid #999; padding: 12px;">Nslookup resolved the domain to 192.232.216.135</td>
<td style="border: 1px solid #999; padding: 12px;">Provides information about the network location of the web service</td>
<td style="border: 1px solid #999; padding: 12px; text-align: center;">🟡 <strong>Low</strong></td>
</tr>

<tr style="background-color: #f5f1e8;">
<td style="border: 1px solid #999; padding: 12px;">3</td>
<td style="border: 1px solid #999; padding: 12px;">HTTP technical information exposed</td>
<td style="border: 1px solid #999; padding: 12px;">Curl returned HTTP response headers and exposed /wp-json/</td>
<td style="border: 1px solid #999; padding: 12px;">May assist technology fingerprinting and further enumeration</td>
<td style="border: 1px solid #999; padding: 12px; text-align: center;">🟡 <strong>Low</strong></td>
</tr>

<tr style="background-color: #f5f1e8;">
<td style="border: 1px solid #999; padding: 12px;">4</td>
<td style="border: 1px solid #999; padding: 12px;">WAF technology identifiable</td>
<td style="border: 1px solid #999; padding: 12px;">Wafw00f identified ModSecurity (SpiderLabs)</td>
<td style="border: 1px solid #999; padding: 12px;">Reveals information about the web application's security architecture</td>
<td style="border: 1px solid #999; padding: 12px; text-align: center;">🟡 <strong>Low</strong></td>
</tr>

<tr style="background-color: #f5f1e8;">
<td style="border: 1px solid #999; padding: 12px;">5</td>
<td style="border: 1px solid #999; padding: 12px;">DNS infrastructure information exposed</td>
<td style="border: 1px solid #999; padding: 12px;">DNSRecon identified DNS, mail and service-related records</td>
<td style="border: 1px solid #999; padding: 12px;">DNS information can help build a broader infrastructure profile</td>
<td style="border: 1px solid #999; padding: 12px; text-align: center;">🟠 <strong>Medium</strong></td>
</tr>

<tr style="background-color: #f5f1e8;">
<td style="border: 1px solid #999; padding: 12px;">6</td>
<td style="border: 1px solid #999; padding: 12px;">two live hosts visible on local network</td>
<td style="border: 1px solid #999; padding: 12px;">Zenmap identified two live hosts in the example network</td>
<td style="border: 1px solid #999; padding: 12px;">Unknown or unauthorized devices may potentially be present on a network</td>
<td style="border: 1px solid #999; padding: 12px; text-align: center;">🟡 <strong>Low</strong></td>
</tr>
</table>

<p style="margin-top: 15px;"><strong>Risk level key:</strong> 🔴 Critical • 🟠 Medium • 🟡 Low</p>

<p>The risks above are observations from the footprinting and scanning exercises, not confirmed vulnerabilities.</p>

<p>The practical exercises primarily involved information gathering and host discovery. No exploitation or vulnerability validation was performed as part of these two modules.</p>

<p>Therefore, the presence of information such as a software version, IP address or DNS record does not by itself mean that the system is vulnerable. Further authorized security testing would be required to confirm any actual vulnerability.</p>

## 6. Recommendations

Based on the observations from these activities, I recommend the following security improvements:

1. Review publicly exposed technology information
   Organizations should regularly review what information about their web technologies, CMS and plugins is publicly visible.

2. Keep software updated
   CMS platforms, plugins and other web technologies should be regularly updated and reviewed against current security advisories.

3. Review HTTP headers
   HTTP response headers should be reviewed to determine whether unnecessary technical information is being exposed.

4. Review DNS records regularly
   DNS records should be checked periodically to ensure that only required information and services are publicly exposed.

5. Properly configure and monitor the WAF
   Keep the WAF (ModSecurity) enabled and tuned, since it already blocks naive attacks.

6. Perform regular internal network discovery
   Organizations should periodically scan their own networks to identify active devices.

7. Investigate unknown devices
   Any unexpected device discovered during network scanning should be investigated and verified.

8. Maintain network documentation
   Network topology and device information should be documented and updated regularly.

9. Perform security testing with authorization
   Reconnaissance and scanning should only be performed against systems and networks where appropriate authorization has been provided.

## 7. Conclusion

During Week 2 of my Cybersecurity & Ethical Hacking internship, I completed practical activities covering footprinting, reconnaissance and network scanning.

In the footprinting activity, I used six Kali Linux tools to collect information about the target domain. I learned how WHOIS can provide domain information, WhatWeb can identify web technologies, Nslookup can resolve domain names, Curl can inspect HTTP headers, Wafw00f can identify a WAF, and DNSRecon can provide additional DNS information.

In the network scanning activity, I used Zenmap to identify my local network configuration and discover active hosts. I also collected IP and MAC address information and created a network topology.

The exercises showed me that information gathering is an important part of cybersecurity. Even before attempting to exploit a system, a security professional can learn a significant amount about an environment by carefully analyzing publicly available information and network responses.

I also learned that technical findings should be documented clearly. A good cybersecurity report should explain what was performed, what was discovered, what the observation means, what risk it may create, and what can be done to reduce that risk.

Finally, I learned that reconnaissance and scanning must always be performed within an authorized scope. These activities were completed as part of the assigned educational cybersecurity lab.

## 8. Evidences Collected
<img width="1346" height="1364" alt="Screenshot 2026-09-16 092238" src="https://github.com/user-attachments/assets/53b96b1c-9031-44eb-a236-1adb317343db" />
<img width="1346" height="1364" alt="Screenshot 2026-09-16 094850" src="https://github.com/user-attachments/assets/2c789002-3633-441b-bdcb-ef71047cf012" />
<img width="1346" height="1364" alt="Screenshot 2026-09-16 100527" src="https://github.com/user-attachments/assets/2f0d33a0-3711-4f35-bd13-dd9d9cb01c66" />
<img width="1346" height="1364" alt="Screenshot 2026-09-16 103452" src="https://github.com/user-attachments/assets/12070f45-834d-40dc-a7c5-cd88a9a5dce0" />
<img width="1346" height="1364" alt="Screenshot 2026-09-16 101156" src="https://github.com/user-attachments/assets/e6acf39f-862c-42ad-bb32-47da3745bd06" />
<img width="1346" height="1364" alt="Screenshot 2026-09-16 103655" src="https://github.com/user-attachments/assets/e1ba5601-447d-4c1a-aa37-6cbae5092777" />
<img width="2538" height="1429" alt="Screenshot 2026-09-16 225329" src="https://github.com/user-attachments/assets/9e855df4-a78a-4ced-a6b0-8c6990091383" />

Author: Dominic Joshua
Cybersecurity professional BO83
linkedin: www.linkedin.com/in/dominic-joshua-bb69473a
📌 Project Information
Program Name: Cybersecurity program at Networkwalks




