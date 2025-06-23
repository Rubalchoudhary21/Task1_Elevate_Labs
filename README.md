Scan Your Local Network for Open Ports

Overview:

This project demonstrates a basic network scanning task performed using Nmap on Kali Linux. The objective was to identify active hosts within a specific target network and then perform a full TCP port scan on those hosts. The process included host discovery and a comprehensive scan of all TCP ports using appropriate Nmap flags.

Tools Used:

Kali Linux (Operating System) Nmap (Network Mapper) 

Target Network: 192.168.27.0/24

Steps Performed:

Host Discovery
To identify live hosts within the target network, the following Nmap command was used:

nmap -sn 192.168.27.0/24 -sn flag performs a "ping scan" to detect which hosts are up.

Once the active hosts were identified, a full TCP scan was performed on all ports using the following command:

nmap -p- -sS 192.168.27.0/24

-p- flag scans all 65535 TCP ports.

-sS performs a SYN scan (stealth scan)

Identified Open Ports and Services:

1. 192.168.27.1
Port: 7070/tcp

Service: realserver
Common Use: This port is often used by RealNetworks streaming media server or sometimes custom applications.

Risk: If not patched, RealServer services have known buffer overflow vulnerabilities and directory traversal flaws.

Recommendation: If RealServer is unnecessary, disable it. Otherwise, ensure it’s updated and protected with firewall rules.

2. 192.168.27.2
Port: 53/tcp

Service: domain (DNS over TCP)

Risk: Open DNS ports can be abused for:

DNS amplification DDoS attacks

Zone transfer leaks if misconfigured

Recommendation:

Limit DNS services to internal network

Block TCP/53 externally if not required

Harden BIND or DNS server configuration

3. 192.168.27.254
All ports are in ignored states

Explanation: No open ports detected, or all were filtered (no response). Not a direct security concern, but may hide detection intentionally.

4. 192.168.27.128
Port: 80/tcp

Service: http

Risk:

Plaintext communication (susceptible to sniffing or MITM attacks)

May expose outdated web servers (e.g., Apache, Nginx, IIS) or vulnerable web applications (e.g., CMS like WordPress)

Recommendation:

Migrate to HTTPS (port 443)

Perform web vulnerability scanning (e.g., with Nikto or OWASP ZAP)

General Security Recommendations:
Block unused ports with a firewall (UFW/iptables).

Use Nmap scripts (-sC) or vuln scans to further analyze exposed services.

Apply patches and monitor logs for signs of exploitation.

Limit access using network segmentation and access controls (e.g., only allow internal IPs to reach DNS or HTTP if needed).

Conclusion

The scanning exercise provided insights into discovering live hosts in a network and identifying open ports using different Nmap scanning techniques. This is a foundational step in network reconnaissance and penetration testing.
