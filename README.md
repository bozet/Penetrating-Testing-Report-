
# PENETRATION TESTING REPORT

### FOOTPRINTING & NETWORK SCANNING PHASES

**W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS**

| Field | Details |
|---|---|
| Pentester Name | [Your Full Name] |
| Program/Batch | Networkwalks – B084 |
| Date | 14 November 2026 |
| Modules Completed | W2-PM1 – Footprinting with Multiple Kali Tools |
| | W2-PM5 – Zenmap Network Scanning |
| Target | networkwalks.com and my own local network |
| Phases Covered | Phase 1: Reconnaissance & Footprinting |
| | Phase 2: Scanning & Network Discovery |

---

# 1. Liability Disclaimer

The activities documented in this repository were performed for educational and cybersecurity training purposes.

The footprinting activities involved collecting publicly available information about the assigned domain, while network scanning was restricted to my own local network.

All activities were conducted within the intended educational scope. These exercises did not involve exploitation, unauthorized access, or attempts to disrupt any system.

The information provided here must not be used for unauthorized activities. Anyone performing cybersecurity assessments must obtain appropriate authorization and comply with applicable laws, regulations, and service terms.

---

# 2. Introduction

This report documents the practical activities completed during Week 2 of my Cybersecurity Internship at Networkwalks.

The project focused on two major areas of cybersecurity:

- **Footprinting and Reconnaissance (W2-PM1):** Using multiple Kali Linux tools to gather publicly available information about `networkwalks.com`.
- **Network Scanning (W2-PM5):** Using Zenmap to discover active devices on my own local network, identify their IP addresses and MAC addresses, and generate a network topology.

The purpose of these exercises was to understand how information gathering and network discovery contribute to cybersecurity assessments.

The practical activities were carried out using Kali Linux, Windows Command Prompt, Nmap, and Zenmap. Screenshots and command outputs are included as supporting evidence.

---

# 3. Tools Used

The following tools were used throughout the project.

| Tool | Purpose |
|---|---|
| Kali Linux | Operating system used for footprinting and reconnaissance |
| WHOIS | Retrieve domain registration information |
| WhatWeb | Identify website technologies and web server information |
| Nslookup | Resolve domain names to IP addresses |
| cURL | Inspect HTTP response headers |
| WAFW00F | Identify the presence of a Web Application Firewall |
| DNSRecon | Collect DNS records and related information |
| Windows Command Prompt | Identify local network configuration and device information |
| Nmap | Network discovery and scanning engine |
| Zenmap | Graphical interface for Nmap and network topology visualization |

---

# 4. Activities Performed

## 4.1 Footprinting and Reconnaissance

I performed footprinting and reconnaissance on the assigned domain, `networkwalks.com`, using six tools available in Kali Linux.

Each tool provided a different type of information about the domain and its publicly exposed infrastructure.

### 4.1.1 WHOIS Lookup

**Command used:**

```bash
whois networkwalks.com
```

The WHOIS lookup provided publicly available domain registration information.

Key observations included:

- Registrar: GoDaddy.com, LLC
- Domain creation date: 6 November 2019
- Last updated: 12 November 2025
- Registry expiry date: 6 November 2027
- Registrant information protected through Domains By Proxy, LLC
- DNSSEC status: Unsigned

The lookup also returned domain name server information.

**Ethical and Legal Consideration:** The WHOIS lookup returned terms of use restricting high-volume automated access and certain forms of data collection and redistribution. The lookup was performed as a single educational query. Applicable service terms must be respected when conducting further reconnaissance.

**Evidence:** `screenshots/01-whois.png`

### 4.1.2 WhatWeb Technology Identification

**Command used:**

```bash
whatweb networkwalks.com
```

WhatWeb was used to identify technologies associated with the website.

The results identified:

- Web server: Apache
- Content Management System: WordPress 7.1.4
- WordPress Download Manager: 3.3.76
- jQuery: 3.7.1
- Website IP address: 192.232.216.135
- HTTP redirection from HTTP to HTTPS

The scan also identified other technologies and website-related information, including Google Tag Manager.

**Evidence:** `screenshots/02-whatweb.png`

### 4.1.3 DNS Lookup Using Nslookup

**Command used:**

```bash
nslookup networkwalks.com
```

Nslookup was used to resolve the domain name and identify its associated IP address.

The result returned:

- Domain: networkwalks.com
- IP address: 192.232.216.135
- DNS server used: 10.0.0.1

The resolved IP address matched the address identified by WhatWeb.

**Evidence:** `screenshots/03-nslookup.png`

### 4.1.4 HTTP Header Inspection Using cURL

**Command used:**

```bash
curl -I https://networkwalks.com
```

The cURL command was used to retrieve the HTTP response headers without downloading the complete webpage.

The response returned:

- HTTP status: 200 OK
- Web server: Apache
- Content type: text/html
- WordPress REST API endpoint information
- Cookie security attributes, including Secure and HttpOnly
- Additional HTTP response and caching headers

This activity demonstrated how HTTP response headers can reveal technical information about a web application.

**Evidence:** `screenshots/04-curl.png`

### 4.1.5 Web Application Firewall Detection

**Command used:**

```bash
wafw00f https://networkwalks.com
```

WAFW00F was used to identify whether a Web Application Firewall was present.

The result identified:

- Web Application Firewall: ModSecurity
- Provider/Identification: SpiderLabs
- Number of requests: 2

This demonstrated how WAF detection tools can identify security technologies used by a website.

**Evidence:** `screenshots/05-wafw00f.png`

### 4.1.6 DNS Enumeration Using DNSRecon

**Command used:**

```bash
dnsrecon -d networkwalks.com
```

DNSRecon was used to collect DNS-related information about the domain.

The results included:

- A records
- NS records
- SOA record
- MX record
- TXT records
- SPF information
- SRV records
- DNS server software information

The scan also returned an unsigned DNSSEC indication, consistent with the WHOIS result.

The SPF record included a soft-fail policy (`~all`).

DNSRecon identified eight SRV records associated with the domain's autodiscovery service.

These findings provided a broader view of the domain's publicly available DNS infrastructure.

**Evidence:** `screenshots/06-dnsrecon.png`

---

## 4.2 Network Scanning with Zenmap

The second practical activity involved network discovery using Zenmap on my own local network.

The objective was to identify the local subnet, discover active devices, identify their IP and MAC addresses, and generate a network topology.

### 4.2.1 Identifying the Local IP Address

I used the Windows Command Prompt to identify the computer's network configuration.

**Command used:**

```cmd
ipconfig
```

The results showed:

- Local IPv4 address: 192.168.1.167
- Subnet mask: 255.255.255.0
- Default gateway: 192.168.1.1
- Network subnet: 192.168.1.0/24

### 4.2.2 Discovering Live Hosts

I launched Zenmap and selected the Ping Scan option.

The local subnet was entered as the target:

```text
192.168.1.0/24
```

The scan identified three active hosts:

| Device | IP Address |
|---|---|
| Router/Gateway | 192.168.1.1 |
| iPhone | 192.168.1.128 |
| Windows PC | 192.168.1.167 |

The scan completed after approximately 7.06 seconds.

**Total live hosts discovered: 3**

### 4.2.3 Identifying MAC Addresses

I used Windows network information and the ARP table to identify the MAC addresses associated with the discovered devices.

The commands used included:

```cmd
ipconfig /all
```

```cmd
arp -a
```

The results helped identify the physical network addresses of the local devices.

For privacy and security reasons, the complete MAC addresses are not reproduced in this public report.

### 4.2.4 Network Topology Generation

After completing the network discovery activity, I opened the Topology tab in Zenmap.

I reviewed the discovered devices, enabled the topology legend, and exported the network topology as a PDF file.

The exported topology provides a visual representation of the three discovered devices and their network relationships.

**Evidence:** `07-network-topology.pdf`

---

# 5. Risk Analysis / Impact

Based on the information collected during the footprinting and network discovery activities, the following potential security observations were identified.

| No. | Risk / Finding | Evidence / Observation | Potential Impact | Risk Level |
|---|---|---|---|---|
| 1 | Website technology information exposed | WhatWeb identified WordPress and associated technologies | May assist technology fingerprinting | Medium |
| 2 | Domain IP address identifiable | Nslookup resolved the domain to an IP address | Provides information about the website's hosting infrastructure | Low |
| 3 | HTTP technical information exposed | cURL returned HTTP response headers and WordPress endpoint information | May provide additional information for reconnaissance | Low |
| 4 | WAF technology identifiable | WAFW00F identified ModSecurity | Reveals information about the website's security architecture | Low |
| 5 | DNS infrastructure information exposed | DNSRecon identified DNS, mail, TXT and SRV records | May help build a broader infrastructure profile | Medium |
| 6 | Multiple active devices discovered | Zenmap identified three live hosts on the local network | Unexpected devices should be verified and monitored | Medium |

**Risk level key:**
- Low: Limited information exposure or potential impact.
- Medium: Information that may require further security review.
- High: Significant potential impact requiring prompt investigation.

The observations above are not confirmed vulnerabilities. The activities focused on information gathering and network discovery. No exploitation or vulnerability validation was performed.

The presence of publicly available technical information does not automatically mean that a system is vulnerable.

---

# 6. Recommendations

Based on the observations made during the exercises, the following recommendations are proposed:

1. **Review publicly exposed technologies:** Organizations should periodically review information exposed about their web servers, CMS platforms, and plugins.

2. **Keep software updated:** Website platforms, plugins, and supporting technologies should be maintained with appropriate security updates.

3. **Review HTTP response headers:** Organizations should assess whether their HTTP headers disclose unnecessary technical information.

4. **Monitor DNS records:** DNS records should be reviewed regularly to ensure that only required information and services are publicly exposed.

5. **Maintain WAF protection:** Web Application Firewall configurations should be reviewed and monitored regularly.

6. **Perform regular network discovery:** Organizations should periodically identify active devices connected to their networks.

7. **Investigate unknown devices:** Any unexpected device discovered during network discovery should be verified.

8. **Maintain network documentation:** Network diagrams and device inventories should be kept up to date.

9. **Respect authorized testing boundaries:** Reconnaissance and network scanning should only be conducted within an approved scope.

---

# 7. Conclusion

During Week 2 of my Cybersecurity Internship at Networkwalks, I completed practical exercises covering footprinting, reconnaissance, and network scanning.

For the footprinting activity, I used six Kali Linux tools: WHOIS, WhatWeb, Nslookup, cURL, WAFW00F, and DNSRecon. These tools helped me understand how publicly available domain registration information, web technologies, DNS records, HTTP headers, and WAF information can be collected and analyzed.

For the network scanning activity, I used Zenmap to identify my local network configuration and discover active devices. I identified three live hosts, examined their IP and MAC address information, and generated a network topology.

These activities improved my understanding of the reconnaissance and network discovery stages of cybersecurity assessments. I also gained practical experience using command-line tools, interpreting their output, documenting findings, and presenting evidence.

Most importantly, the exercises reinforced the importance of conducting cybersecurity activities within an authorized scope and documenting findings responsibly.

---

# 8. Evidences Collected

The following evidence files are included in this repository.

### Footprinting and Reconnaissance

| No. | Evidence | Description |
|---|---|---|
| 1 | `01-whois.png` | WHOIS domain registration lookup |
| 2 | `02-whatweb.png` | Website technology identification |
| 3 | `03-nslookup.png` | DNS lookup results |
| 4 | `04-curl.png` | HTTP response headers |
| 5 | `05-wafw00f.png` | WAF detection results |
| 6 | `06-dnsrecon.png` | DNS enumeration results |

### Network Scanning

| No. | Evidence | Description |
|---|---|---|
| 7 | `07-zenmap-topology.png` | Zenmap network topology screenshot |
| 8 | `07-network-topology.pdf` | Exported network topology |

### Command Output Files

The `outputs/` folder contains the text files generated during the footprinting activities:

- `01-whois.txt`
- `02-whatweb.txt`
- `03-nslookup.txt`
- `04-curl.txt`
- `05-wafw00f.txt`
- `06-dnsrecon.txt`

---

**End of Report**

**Project Information**

- Program: Cybersecurity Internship – Networkwalks
- Batch: B084
- Project: Week 2 – Footprinting and Network Scanning
- Modules: W2-PM1 and W2-PM5
