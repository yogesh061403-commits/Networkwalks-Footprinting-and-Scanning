
# Week 2 – Footprinting & Reconnaissance Report

**Networkwalks Cybersecurity Internship**
**Project:** Footprinting and Reconnaissance Using Multiple Kali Linux Tools & Network Scanning

---

## 1. Project Overview

This report documents my Week 2 practical activities as part of the Networkwalks Cybersecurity Internship.

The project focused on footprinting, reconnaissance, OSINT and network discovery using different cybersecurity tools.

I performed domain information gathering on networkwalks.com using Kali Linux tools and explored OSINT with theHarvester and Maltego. I also used Zenmap to discover active hosts on my local VirtualBox network.

The practical work helped me understand how information is collected and analysed before moving into further penetration testing activities.

## 2. Objectives

- Understand the footprinting and reconnaissance process.
- Collect domain registration information using WHOIS.
- Identify website technologies using WhatWeb.
- Perform DNS resolution and enumeration.
- Analyse HTTP response headers.
- Identify Web Application Firewall (WAF) technologies.
- Explore OSINT using theHarvester and Maltego.
- Discover active hosts using Zenmap.
- Understand the importance of reconnaissance in VAPT.

## 3. Tools Used

| Tool | Purpose |
|------|---------|
| Kali Linux | Reconnaissance environment |
| WHOIS | Domain registration information |
| WhatWeb | Website technology identification |
| Nslookup | DNS lookup |
| cURL | HTTP response header analysis |
| Wafw00f | WAF detection |
| DNSRecon | DNS enumeration |
| theHarvester | OSINT information gathering |
| Maltego | Visual OSINT and relationship mapping |
| Zenmap | Network discovery and scanning |

## 4. Scope of Testing

| Category | Details |
|----------|---------|
| Program | Networkwalks Cybersecurity Internship |
| Project | Week 2 |
| Domain | networkwalks.com |
| Local network | 192.168.56.0/24 |
| Footprinting environment | Kali Linux |
| Network scanning tool | Zenmap |
| Network scanning environment | Windows / VirtualBox lab |

The domain footprinting activities were performed as part of the assigned internship exercise. The Zenmap scan was performed on my local lab network.

## 5. Practical Activities & Findings

### 5.1 WHOIS – Domain Information Gathering

```bash
whois networkwalks.com 
```

WHOIS was used to gather publicly available registration information about the target domain.

**Information identified:**
- Domain registrar: GoDaddy.com, LLC
- Domain creation date
- Domain update date
- Domain registration status
- Name servers
- DNSSEC status

**Observation:** WHOIS provided useful information about the domain registration and its associated name servers.

### 5.2 WhatWeb – Website Technology Identification

```bash
whatweb networkwalks.com 
```

**Technologies identified:**
- Apache web server
- WordPress
- Bootstrap
- jQuery
- WordPress-related components

**Observation:** The scan helped identify the website's technology stack and provided an initial understanding of its web environment.

### 5.3 Nslookup – DNS Resolution

```bash
nslookup networkwalks.com 
```

**Result:**
```
DNS Server: 8.8.8.8
Name: networkwalks.com
Address: 192.232.216.135
```

**Observation:** The domain was successfully resolved using Google's public DNS server.

### 5.4 cURL – HTTP Response Header Analysis

```bash
curl -I https://networkwalks.com 
```

The `-I` option retrieves HTTP response headers without downloading the complete webpage.

| Header | Result |
|--------|--------|
| HTTP Status | HTTP/2 200 |
| Server | Apache |
| Content-Type | text/html; charset=UTF-8 |
| Set-Cookie | WordPress client cookie |
| X-Nginx-Cache | 0 |
| Link | WordPress REST API endpoint |

**Observation:** The headers provided information about the web server, content type, cookies and application-related endpoints. This showed how HTTP headers can reveal useful technical information during web reconnaissance.

### 5.5 Wafw00f – Web Application Firewall Detection

```bash
wafw00f networkwalks.com 
```

**Result:** The site https://networkwalks.com is behind ModSecurity (SpiderLabs) WAF.

**Observation:** This activity helped me understand the role of WAF detection during the reconnaissance phase.

### 5.6 DNSRecon – DNS Enumeration

```bash
dnsrecon -d networkwalks.com
```

**Records observed:** NS, A, MX, TXT, SPF information, SRV

**Observation:** DNSRecon reported 8 records and provided additional information about the domain's DNS infrastructure, mail services and service records.

### 5.7 theHarvester – OSINT Information Gathering

**Command 1:**
```bash
theHarvester -d microsoft.com -l 1000 -b baidu
```

**Result:** No IP addresses, email addresses, people or hosts found.

**Observation:** The selected source did not return any results for this search.

**Command 2:**
```bash
theHarvester -d microsoft.com -l 50 -b all
```

**Observation:** Some sources could not complete their searches because the required API keys were missing or invalid. This showed that certain OSINT sources need API credentials.

### 5.8 Maltego – Visual OSINT

**Target domain:** networkwalks.com

**Activity performed:**
1. Created a Domain entity.
2. Added the target domain to the graph.
3. Executed the To Emails transformation.
4. Examined the returned email entity.

**Result:**
```
networkwalks.com
       |
info@networkwalks.com
```

**Observation:** Maltego showed how OSINT information can be collected and represented visually through connected entities.

### 5.9 Zenmap – Network Discovery

**Target network:** 192.168.56.0/24

```bash
nmap -sn 192.168.56.0/24
```

I selected the Ping Scan profile in Zenmap to discover active hosts on my local network.

**Result:**
```
Nmap scan report for 192.168.56.1
Host is up.

Nmap done: 256 IP addresses scanned, 1 host up
```

**Observation:** The scan identified one active host (192.168.56.1) in the scanned subnet.

### 5.10 Zenmap – Network Topology

After the discovery scan, I opened the Topology tab in Zenmap.

**Activity performed:**
- Opened the Topology view.
- Examined the discovered host.
- Viewed the relationship between localhost and the discovered network host.

**Observation:** The topology view displayed host 192.168.56.1 connected to localhost, giving a visual representation of the discovery results.

## 6. Summary of Findings

| Tool | Key Finding |
|------|-------------|
| WHOIS | Domain registration and name server information |
| WhatWeb | Apache, WordPress and other web technologies |
| Nslookup | Resolved IP: 192.232.216.135 |
| cURL | HTTP/2 200 and response headers |
| Wafw00f | ModSecurity (SpiderLabs) detected |
| DNSRecon | 8 DNS records reported |
| theHarvester | Baidu returned no results; multiple sources had API-key limitations |
| Maltego | Domain-to-email relationship identified |
| Zenmap | 1 active host discovered |
| Zenmap Topology | Visual network topology generated |

## 7. Conclusion

During Week 2 of the Networkwalks Cybersecurity Internship, I gained practical experience in footprinting, reconnaissance, OSINT and network discovery.

I worked with multiple Kali Linux tools, including WHOIS, WhatWeb, Nslookup, cURL, Wafw00f and DNSRecon. I also explored theHarvester and Maltego to understand different approaches to collecting and analysing publicly available information.

Using Zenmap, I performed a Ping Scan on my local network and identified an active host, then explored the topology view to see how discovered hosts are represented visually.

Overall, this project strengthened my understanding of the reconnaissance phase and how information gathering supports the initial stages of Vulnerability Assessment and Penetration Testing (VAPT).

## 8. Evidence Collected

### 8.1 WHOIS – Domain Information
![WHOIS Result](screenshots/01-whois.png)

### 8.2 WhatWeb – Technology Identification
![WhatWeb Result](screenshots/02-whatweb.png)

### 8.3 Nslookup – DNS Resolution
![Nslookup Result](screenshots/03-nslookup.png)

### 8.4 cURL – HTTP Response Headers
![HTTP Headers Result](screenshots/04-curl.png)

### 8.5 Wafw00f – WAF Detection
![Wafw00f Result](screenshots/05-wafw00f.png)

### 8.6 DNSRecon – DNS Enumeration
![DNSRecon Result](screenshots/06-dnsrecon.png)

### 8.7 theHarvester – Multiple Sources
![theHarvester Multiple Sources](screenshots/07-theharvester-all.png)

### 8.8 theHarvester – Baidu Search
![theHarvester Baidu Result](screenshots/08-theharvester-baidu.png)

### 8.9 Maltego – Domain and Email Relationship
![Maltego Graph](screenshots/09-maltego.png)

### 8.10 Zenmap – Network Scan Result
![Zenmap Scan Result](screenshots/10-zenmap-scan.png)

### 8.11 Zenmap – Network Topology
![Zenmap Topology](screenshots/11-zenmap-topology.png)

## 9. Disclaimer

This project was performed as part of cybersecurity learning and internship activities.

All scanning and testing should be conducted only on systems and networks for which proper authorization has been obtained. The findings documented here are for educational purposes.

**Project:** Week 2 – Footprinting and Reconnaissance
**Program:** Networkwalks Cybersecurity Internship
**Focus Area:** Vulnerability Assessment and Penetration Testing (VAPT)
EOF
