# Pen-Testing-
Penetrating testing results 
Liability Disclaimer
I performed these activities only on systems and devices for which I had secured written permission, or which I own myself. All material in this report is for education and research purposes only and must not be used to break the law. The instructor, the authors and Networkwalks are not responsible for how this knowledge is used. Every action taken is the sole responsibility of the person taking it. Misuse can lead to criminal charges, heavy fines, loss of employment and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.
 
2. Introduction
This report covers footprinting of the networkwalks.com domain using multiple Kali Linux tools (W2-PM1) and scanning of my own local network with Zenmap (W2-PM5). The first module covers the footprinting phase and the second covers the scanning phase; together they show how an attacker moves from gathering public information to mapping live hosts on a network. This is the Week 2 deliverable of my ongoing internship program at Networkwalks.
Footprinting commands were run from Kali Linux on 12 November 2026. Scanning was performed from a Windows PC with Zenmap installed. Each step below lists the exact command used, the result observed, a screenshot as evidence, and a short note on why the finding matters from an attacker's point of view.
3. Tools Used
Tool	Purpose
Kali Linux / Windows	Operating systems used for the reconnaissance activities
whois	Domain registration details (registrar, dates, name servers, privacy)
whatweb	Fingerprint web technologies (server, CMS, plugins, IP)
nslookup	Resolve the domain name to its IP address using DNS
curl -I	Read the HTTP response headers of the website
wafw00f (v2.3.1)	Detect whether a Web Application Firewall protects the site
dnsrecon	Enumerate DNS records (SOA, NS, MX, A, SPF/TXT, SRV)
Zenmap (Nmap GUI)	Scan the local subnet for live hosts, IPs and MAC addresses
Windows CMD (ipconfig)	Identify local IP address and subnet
 
4. Activities Performed
4.1 Footprinting & Reconnaissance
Reconnaissance was performed against networkwalks.com using six Kali Linux tools. Each tool collects a different type of public information about the target. All activity was passive or limited to normal client requests (a handful of DNS lookups and a few HTTP requests) and stayed within the permitted scope.
4.1.1 WHOIS - Domain Registration
Command
 $ whois networkwalks.com
Result observed
•	Registrar: GoDaddy.com, LLC (IANA ID 146); registry domain ID 2452319255_DOMAIN_COM-VRSN.
•	Created 6 Nov 2019; registry expiry date 6 Nov 2027; record last updated 12 Nov 2025.
•	Domain status: clientDeleteProhibited, clientRenewProhibited, clientTransferProhibited and clientUpdateProhibited (registrar locks in place).
•	Name servers: NS6135.HOSTGATOR.COM, NS6136.HOSTGATOR.COM, plus NS29/NS30.DOMAINCONTROL.COM in the registrar's own WHOIS record.
•	DNSSEC: unsigned.
•	Registrant, admin and tech contacts are masked by a privacy service (Domains By Proxy, LLC, Tempe, Arizona); contact is via a GoDaddy web form.
Why it matters
WHOIS shows who hosts and registers the domain and where DNS is managed, which tells an attacker which providers' portals and support channels are worth targeting (for example for social engineering). The privacy proxy and registrar locks are good practice and limit exposure. Unsigned DNSSEC means DNS answers cannot be cryptographically validated.
 
Figure 1: WHOIS output - registrar, dates, status codes and name servers
 
Figure 2: WHOIS output (continued) - privacy-protected contacts and name servers
4.1.2 WhatWeb - Web Technology Fingerprinting
Command
 $ whatweb networkwalks.com
Result observed
•	HTTP request redirects (301) to HTTPS; HTTPS responds 200 OK.
•	Web server: Apache; server IP 192.232.216.135.
•	CMS: WordPress 7.1.4 (via MetaGenerator tag), with WordPress Download Manager 3.3.76.
•	Front-end: jQuery 3.7.1, HTML5, Open Graph protocol, Google Tag Manager; page title "Networkwalks Academy".
•	Cookie __wpdm_client is set with the HttpOnly flag.
•	Public contact email exposed: info@networkwalks.com.
•	Uncommon headers disclosed include x-nginx-cache, x-endurance-cache-level, permissions-policy and x-redirect-by.
Why it matters
Exact CMS and plugin versions let an attacker look up known vulnerabilities for those releases. A version number alone is not a vulnerability, and the versions seen here are newer than those recorded in my earlier run (WordPress 7.0.4 and WP Download Manager 3.3.58), which suggests the site is being kept up to date. Disclosure of the version is still avoidable information leakage.
