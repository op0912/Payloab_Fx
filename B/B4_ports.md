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

---

## File Transfer

Ports in this section are related to file transfer and file sharing between systems.

They allow:
- uploading and downloading files
- sharing directories over the network
- accessing remote file systems

---

## Port : 20/21  
## Name : FTP (FILE TRANSFER PROTOCOL)

### Definition
- FTP (File Transfer Protocol) is used to transfer files between a client and a server.
- It allows uploading (sending files) and downloading (receiving files).
- The protocol is split into two channels:
  - Port 21 is used for control (login, commands, session management)
  - Port 20 is used for data transfer
- Session management means maintaining the connection while multiple commands and transfers are executed.

### How it communicates
- Uses TCP for both 20/21
- Establishes a control connection on port 21
- Uses a separate connection for data transfer (port 20 or dynamic ports in passive mode)

### How it can be attacked
- Brute force: attacker tries many username/password combinations until one works
- Anonymous login: attacker logs in without credentials if the server allows it
- Credential sniffing: attacker captures username and password because FTP is not encrypted
- Unauthorized file upload: attacker uploads malicious files to the server
- Misconfigured permissions: attacker accesses or modifies files they should not have access to

### Observation
- No FTP service detected on port 21 using netstat
- Only local connections observed (127.0.0.1)
- Test-NetConnection failed when using an invalid IP
- No FTP response when attempting to connect (ftp command)
- No FTP observed locally

### Notes
- Port 21 is the main entry point for FTP
- FTP requires a running service to respond
- No service on port 21 means FTP is not available
- FTP is not secure (credentials are sent in clear text)
- FTPS (secure) control connection can use port 21 (explicit mode) or 990 (implicit mode)
- Data connections are often dynamic (especially in passive mode), not always using port 20
---

## Port : 69  
## Name : TFTP (TRIVIAL FILE TRANSFER PROTOCOL)

### Definition
- Used to transfer files over a network
- Simpler version of FTP with no authentication


### How it communicates
- Uses UDP (port 69)
- No connection setup (connectionless)
- No login or authentication

### How it can be attacked
- No authentication: anyone can access files if the service is exposed
- File download: attacker can retrieve sensitive files
- File upload: attacker can upload malicious files

### Observation
- 

### Notes
- 

---

## Port : 2049  
## Name : NFS (NETWORK FILE SYSTEM)

### Definition
- Used to access and work on files stored on a remote system
- Allows files to be used as if they were local
- Used mainly on Linux systems

### How it communicates
- Uses TCP (port 2049)
- Client sends requests to access files on the server
- Server responds with file data
- Allows reading and writing files over the network

### How it can be attacked
- Unauthorized access: attacker can read files if access is not properly restricted
- File modification: attacker can modify existing files on the server
- File upload: attacker can add malicious files to the system
- Trust abuse: NFS is often used in trusted networks, making it easier to exploit if access is gained

### Observation
- 

### Notes
- Modifying or adding files through NFS affects the remote server, not the local machine
- However, if a file is executed, it runs on the local system and can affect it


---

## Port : 445
## Name : SMB (SERVER MESSAGE BLOCK) 

### Definition
- Protocol used to share files and network resources between systems
- Allows accessing and modifying files on a remote system 

### How it communicates
- Uses TCP (port 445)
- Client connects to a remote system to access shared resources
- Server responds and allows access based on permissions
- Allows reading and writing files over the network 

### How it can be attacked
- Credential attacks: attacker can try to guess or reuse login credentials
- Unauthorized access: attacker can access shared folders if permissions are weak
- File access: attacker can read or copy sensitive files
- File modification: attacker can modify or delete files
- Malware execution: malicious files can be placed and executed on a system

### Observation
-

### Notes
- Mainly used in Windows environments
- Widely used in most networks, making it a common target
- Requires authentication (username and password)
- Equivalent to NFS in Linux systems

---

## Remote Access

Ports in this section are used to remotely access and control systems.

They allow:
- remote command execution
- system administration
- remote desktop access


---

## Port : 22
## Name : SSH (SECURE SHELL)

### Definition
- Protocol used to remotely access and control a system securely
- Allows command execution on a remote machine

### How it communicates
- Uses TCP (port 22)
- Establishes a secure connection between client and server
- Requires authentication (password or SSH key)
- Allows sending commands and receiving output in real time

### How it can be attacked
- Brute force: attacker tries many passwords to gain access
- Credential reuse: attacker uses leaked credentials from other services
- Misconfiguration: weak settings can allow unauthorized access
- Key compromise: stolen SSH keys can grant direct access
- Exposure: open SSH service can be targeted continuously

### Observation
-

### Notes
- Provides encrypted remote access (unlike Telnet)
- Mainly used on servers and Linux systems
- Not commonly used by regular users
- Requires a running service to accept connections

---

 ## Port : 23
## Name : TELNET

### Definition
- Protocol used to remotely access and control a system
- Does not provide encryption, making it insecure

### How it communicates
- Uses TCP (port 23)
- Establishes a direct connection between client and server
- Sends all data in plain text (no encryption)

### How it can be attacked
- Credential sniffing: attacker can capture usernames and passwords in plain text
- Man-in-the-middle: attacker can intercept and modify communication
- Unauthorized access: weak or exposed services can be accessed directly

### Observation
-

### Notes
- Predecessor to SSH
- Not secure due to lack of encryption
- Uses authentication but transmits credentials in plain text
- Rarely used in modern environments
- Replaced by SSH in most cases


---

## Port : 3389
## Name : RDP (REMOTE DESKTOP PROTOCOL)

### Definition
- Protocol used to remotely access and control a system with a graphical interface
- Allows full interaction with a remote desktop (mouse, keyboard, applications)

### How it communicates
- Uses TCP (port 3389)
- Client connects to a remote system running RDP service
- Server sends graphical display data to the client
- Client sends input (keyboard and mouse) back to the server

### How it can be attacked
- Brute force: attacker tries multiple credentials to gain access
- Credential reuse: attacker uses leaked login credentials
- Unauthorized access: weak passwords or exposed services can be exploited
- Misconfiguration: improper settings can expose the system

### Observation
-

### Notes
- Mainly used in Windows environments
- Provides full desktop access (not just terminal)
- Execution happens on the remote machine
- Requires authentication (username and password)
- More resource-intensive than SSH due to graphical interface
- Creates a new, independent session on the remote system
- Multiple users can have separate sessions on the same machine
- The local user does not see the remote session activity


---


## Port : 5985/5986
## Name : WinRM (WINDOWS REMOTE MANAGEMENT)

### Definition
- 

### How it communicates
- 

### How it can be attacked
- 

### Observation
-

---

## Port : 5900
## Name : VNC (VIRTUAL NETWORK COMPUTING)

### Definition
- Protocol used to remotely access and control a system with a graphical interface
- Allows sharing and interacting with the current user’s desktop

### How it communicates
- Uses TCP (port 5900)
- Client connects to a system running a VNC server
- Server sends the current screen to the client
- Client sends mouse and keyboard input back to the server

### How it can be attacked
- Weak authentication: attacker can access the system if credentials are weak
- Unauthorized access: exposed VNC services can be directly targeted
- Session hijacking: attacker can take control of an active session
- Lack of encryption: some VNC implementations do not encrypt traffic

### Observation
-

### Notes
- Shares the existing user session (not a new one)
- User activity is visible to both parties in real time
- Less secure by default compared to RDP
- Commonly used for support and screen sharing
- Unlike RDP, VNC does not create a separate session but mirrors the current user’s screen