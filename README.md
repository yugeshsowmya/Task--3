# Task--3
Basic Vulnerability Scan on Your PC
Task 3 — Vulnerability Scan Using Nmap

This task involves performing a basic vulnerability scan on my personal laptop using Nmap, documenting the findings, and providing remediation suggestions.
Since I was unable to install Nessus Essentials and OpenVAS, I used Nmap vulnerability scripts as an alternative, which is acceptable for the internship assignment.
**1. System Details**
- **Local IP Address:** 192.168.31.118  
- **Operating System:** Windows  
- **Scanner Used:** Nmap 7.98  
- **Scan Types:**  
  - Ping Scan  
  - Top Ports Scan  
  - Full TCP Port Scan  
  - Vulnerability Scan using NSE scripts
**2. Commands Used**
Find IP Address
         ipconfig
Host Discovery
         nmap -sn 192.168.31.118
Quick Top‑Ports Scan
         nmap -sS -sV --top-ports 100 -T4 -oN quickscan.txt 192.168.31.118
Full TCP Port Scan (All Ports)
         nmap -p- -sS -sV -O -T4 -oA fullscan 192.168.31.118
Vulnerability Scan (NSE vuln scripts)
         nmap -sV --script vuln -oN vulnscan.txt 192.168.31.118
**3.Screenshots**
All screenshots are included in this repository:
  IP Discovery
  Host Discovery
  Quick Scan
  Full TCP Scan
  Vulnerability Scan
**4.Analysis and Findings**
Open Ports Identified:
    Port	        Service	        Description
135/tcp	        msrpc	          Windows RPC service
137/tcp	        netbios-ns	    NetBIOS name service
139/tcp	        netbios-ssn	    NetBIOS session service
445/tcp	        microsoft-ds	  SMB file sharing
2869/tcp	      http	          SSDP/UPnP HTTP API
5040/tcp	      unknown	        Windows internal service
7070/tcp	      ssl/realserver?	Possible UPnP/media service
7680/tcp	      pando-pub?	    Windows Delivery Optimization
49664–49669/tcp	msrpc	          Windows RPC dynamic ports
**Vulnerability Scan Results:**
  Based on the Nmap NSE vuln scripts:
    ❌ No XSS vulnerabilities found
    ❌ No CSRF vulnerabilities
    ❌ No DOM‑based XSS
    ❌ No stored XSS
    ❌ No SMB vulnerabilities confirmed (connection blocked by firewall)
    ✔ System appears not vulnerable to the tested CVEs
    ✔ Windows firewall blocked unsafe SMB attempts — this is good
**Potential Risks (Even if not exploitable):**
 Service                  Potential Risk                                  
 SMB (445)           Target for malware if outdated (e.g., WannaCry) 
 NetBIOS (137/139)   Reveals device information on LAN               
 UPnP (2869)         May allow device discovery by other LAN users   
 RPC ports           Must remain patched to avoid RCE exploits       
 Unknown services    Could expose internal components if outdated
**Remediation Suggestions:**
 Issue / Port                       Recommendation                                                       
 SMB (445)                          Keep Windows fully updated; disable SMBv1; restrict to local network 
 NetBIOS (137/139)                  Disable NetBIOS over TCP/IP if not needed                            
 UPnP (2869)                        Disable UPnP in Windows if unused                                    
 RPC dynamic ports                  Apply all Windows security updates regularly                         
 Unknown ports (5040, 7070, 7680)   Verify service purpose; disable if unnecessary                       

