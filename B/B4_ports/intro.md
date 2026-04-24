# B4 — Ports (Exposure & Entry Points)

## Core Idea

At this level, the focus is on **understanding which services are exposed on a system**.

Ports are not just numbers.  
Each port is an entry point to a service, and every exposed service is a potential attack surface.

The goal is not memorization, but understanding:
- what the service does  
- how it communicates  
- how it can be attacked  

In this section, **about 40 key ports will be analyzed in depth** to build a clear and practical understanding.

---

# Fundamentals — Port / Service / Protocol / Function

---

## Core Concept

A port exposes a service  
A service uses a protocol  
A protocol fulfills a function

---

## Definitions

### Port
A port is a network entry point on a machine.

Role:
- Directs incoming traffic to the correct service
- Identifies a specific application

Key idea:
Port = network entry point

Examples:
- 21 → FTP  
- 443 → HTTPS  
- 445 → SMB  

---

### Service
A service is a program running on a machine that listens on a port.

Role:
- Handles incoming connections
- Provides a specific functionality (web, file sharing, etc.)

Key idea:
Service = program listening on a port

Examples:
- FTP server  
- Web server (Apache, Nginx)  
- SMB service  

---

### Protocol
A protocol is a set of rules that define how machines communicate.

Role:
- Standardizes communication
- Ensures systems understand each other

Key idea:
Protocol = communication rules / language

Examples:
- FTP → file transfer  
- HTTP/HTTPS → web communication  
- DNS → name resolution  

---

### Function
The function is the actual purpose of the protocol.

Role:
- Solves a specific need

Key idea:
Function = what it is used for

Examples:
- FTP → send/receive files  
- DNS → resolve domain names to IP  
- SMB → share files  

---

## Full Chain Example

Port 21 open  
→ FTP service running  
→ FTP protocol used  
→ Function = file transfer  

---

## Why These Services Were Created

### Historical Context

Originally:
- closed networks  
- trusted users  
- little to no attacks  

Priority = functionality  
NOT = security  

---

### Purpose of Common Services

- FTP → transfer files between machines  
- TFTP → simple and fast file transfer (internal use)  
- NFS → share files across Linux systems  
- SMB → share files across Windows networks  

---

## Why They Became Vulnerable

### Core Problem

These protocols were not designed with modern security in mind

---

### Main Reasons

1. No Encryption  
- FTP → credentials in clear text  
- Telnet → data visible  

2. Trusted Network Assumption  
- NFS / SMB assume internal trusted environments  

3. Over-Simplicity  
- TFTP → no authentication  

4. Environment Changed  

Before:
closed network  

Today:
open and hostile Internet  

---

## Key Security Concept

Open port → exposed service → potential attack surface  

---

## Final Summary

Port = entry point  
Service = running program  
Protocol = communication rules  
Function = purpose  

Created to solve a need  
Can become exploitable if not secured  

---

## Mental Model

More open ports  
→ more exposed services  
→ larger attack surface

---

## Selected Ports

This section will cover about 40 key ports.

These ports were selected based on:
- frequency in real-world environments
- relevance for Network+ certification
- importance in offensive security and red team scenarios

The goal is to focus on ports that provide the most practical value, rather than trying to cover everything.

---

### Core Ports

20/21 → FTP  
22 → SSH  
23 → Telnet  
25 → SMTP (incl. 587 TLS)  
53 → DNS  
67/68 → DHCP  
69 → TFTP  
80 → HTTP  
110 → POP3 (incl. 995 TLS)  
123 → NTP  
137 → NetBIOS Name  
138 → NetBIOS Datagram  
139 → NetBIOS Session  
143 → IMAP (incl. 993 TLS)  
161/162 → SNMP  
389 → LDAP (incl. 636 TLS)  
443 → HTTPS  
445 → SMB  
3389 → RDP  

---

### Enterprise / Red Team

88 → Kerberos  
135 → RPC  
500 → ISAKMP (IPSec VPN)  
1433 → MSSQL  
1521 → Oracle DB  
2049 → NFS  
3306 → MySQL  
5432 → PostgreSQL  
5900 → VNC  
5985/5986 → WinRM  
8080 → HTTP alt  

---

### Optional / Contextual

5060/5061 → SIP (VoIP)  
1720 → H.323  
514 → Syslog  



---

## Working Template (Temporary)

This template is used to document each port during the learning phase.

It ensures consistency and helps build a structured understanding of:
- the service behind the port
- how it communicates
- how it can be attacked
- real observations

This section will be removed once all ports are documented.

---

## Port : 
## Name : 

### Definition
- 

### How it communicates
- 

### How it can be attacked
- 

### Observation
-

### Notes
-

---
