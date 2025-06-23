# Scan Your Local Network for Open Ports

##  Overview

This project demonstrates a basic network scanning exercise using **Nmap** on **Kali Linux**. The goal was to identify **active hosts** within the local subnet and then perform a **comprehensive TCP port scan** on each detected host. The process involved both **host discovery** and a **full port scan** using standard Nmap flags.

---

##  Tools Used

- **Operating System**: Kali Linux  
- **Scanner**: [Nmap](https://nmap.org/) (Network Mapper)

---

##  Target Network

`192.168.27.0/24`

---

## 🔧 Steps Performed

### 

```bash

**1️⃣ Host Discovery**

To identify live hosts within the target network, the following Nmap command was used:


nmap -sn 192.168.27.0/24
The -sn flag performs a ping scan to detect which hosts are up.

**2️⃣ Full TCP Port Scan**
After detecting active hosts, a complete TCP scan was performed using:


nmap -p- -sS 192.168.27.0/24
-p- scans all 65535 TCP ports

-sS performs a TCP SYN scan (also known as a stealth scan)

📋 Identified Open Ports and Services:

🔹 192.168.27.1
Port: 7070/tcp

Service: realserver

Common Use: Used by RealNetworks streaming media server or custom apps

Risk: Known for buffer overflow and directory traversal vulnerabilities

Recommendation: Disable if not needed. Otherwise, patch and apply firewall rules

🔹 192.168.27.2

Port: 53/tcp

Service: domain (DNS over TCP)

Risks:

Vulnerable to DNS amplification DDoS

May expose zone transfers if misconfigured

Recommendation:

Limit access to internal IPs

Block external access on TCP/53

Harden DNS server configuration

🔹 192.168.27.254

Observation: All ports in ignored or filtered states

Explanation: No open ports detected; host may intentionally suppress responses

Risk: Minimal, but may suggest evasion techniques

🔹 192.168.27.128

Port: 80/tcp

Service: http

Risks:

Transmits data in plaintext, vulnerable to MITM/sniffing

Could expose outdated or unpatched web applications

Recommendation:

Enforce HTTPS (port 443)

Perform web vulnerability assessments (e.g., Nikto, OWASP ZAP)

 General Security Recommendations:
🔒 Block unused ports using UFW or iptables

🔍 Use Nmap scripts (-sC) or vulnerability scans (--script vuln) for deeper analysis

🛡️ Keep all exposed services patched

📶 Segment networks and apply access controls (limit exposure of services like DNS/HTTP)

 Conclusion
This scanning activity provided hands-on experience with host discovery and port scanning techniques using Nmap. It reinforced essential skills for network reconnaissance, which is a critical step in both ethical hacking and penetration testing workflows.



