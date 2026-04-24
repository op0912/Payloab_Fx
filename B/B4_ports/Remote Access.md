# Remote Access

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
- 5985 → HTTP (unencrypted)
- 5986 → HTTPS (encrypted with TLS)

## Name : WinRM (WINDOWS REMOTE MANAGEMENT)

### Description
- WinRM is based on the WS-Management protocol over HTTP/HTTPS
- A client sends HTTP/HTTPS requests containing PowerShell commands to the target machine.
- The remote system executes the commands and returns the result through the same protocol.
- It allows executing PowerShell commands on a remote machine without using a graphical interface.

### How it communicates
- WinRM uses a layered communication model:
- Transport layer: TCP
- Application protocol:
  - HTTP (port 5985)
  - HTTPS (port 5986)

### How it can be attacked
- Weak credentials:
  If passwords are weak or reused, unauthorized access is possible
- Exposed service:
  If WinRM is accessible from the internet, it increases risk
- Unencrypted communication:
  Using HTTP (port 5985) can expose sensitive data
- Misconfiguration:
  Poor access control can allow unintended access
- High privilege access:
  If an admin account is compromised, full control of the system is possible

### Observation
-

### Notes 
- WinRM does not use a custom protocol like SSH.
- Instead, it uses HTTP/HTTPS as a transport mechanism to carry management commands.

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

---
