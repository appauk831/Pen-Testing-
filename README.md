# Pen-Testing-
Penetrating testing results 
I performed these activities only on systems and devices for which I had secured written permission, or which I own myself. All material in this report is for education and research purposes only and must not be used to break the law. The instructor, the authors and Networkwalks are not responsible for how this knowledge is used. Every action taken is the sole responsibility of the person taking it. Misuse can lead to criminal charges, heavy fines, loss of employment and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.
 
2. Introduction
This report covers footprinting of the networkwalks.com domain using multiple Kali Linux tools (W2-PM1) and scanning of my own local network with Zenmap (W2-PM5). The first module covers the footprinting phase and the second covers the scanning phase; together they show how an attacker moves from gathering public information to mapping live hosts on a network. This is the Week 2 deliverable of my ongoing internship program at Networkwalks.
Footprinting commands were run from Kali Linux on 12 November 2026. Scanning was performed from a Windows PC with Zenmap installed. Each step below lists the exact command used, the result observed, a screenshot as evidence, and a short note on why the finding matters from an attacker's point of view.
Activities Performed
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
