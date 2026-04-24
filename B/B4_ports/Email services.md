# Email Services

Ports in this section are related to sending, receiving, and managing emails between systems.

They allow:
- sending emails to remote mail servers
- receiving and retrieving emails from a server
- synchronizing mailboxes across multiple devices

---

  ## Port : 25/587
- 25 → SMTP (server-to-server, legacy)
- 587 → SMTP (client submission, encrypted with TLS)

## Name : SMTP (SIMPLE MAIL TRANSFER PROTOCOL)

### Description
- SMTP is used to send emails between systems
- A client sends an email to an SMTP server
- The SMTP server uses DNS (MX records) to find the destination mail server
- The message is then transferred to the recipient’s mail server
- It handles both client-to-server and server-to-server email delivery

### How it communicates
- SMTP uses a layered communication model:
- Transport layer: TCP
- Application protocol:
  - SMTP (port 25 or 587)

### How it can be attacked
- Open relay:
  Misconfigured servers may allow anyone to send emails through them
- Spam abuse:
  Attackers can use SMTP servers to send large amounts of spam
- Credential attacks:
  Weak or reused passwords can allow unauthorized access
- Email spoofing:
  Attackers can forge sender information in emails
- Unencrypted communication:
  Using port 25 without TLS can expose sensitive data

### Observation
-Tested connectivity to an SMTP server using PowerShell:
  Test-NetConnection smtp.gmail.com -Port 587  
  → TcpTestSucceeded : True  
  Test-NetConnection smtp.gmail.com -Port 25  
  → TcpTestSucceeded : False
- The SMTP server is reachable (DNS resolution and routing are working)
- Port 587 is open and allows client connections
- Port 25 is blocked for outbound connections
- Port 587 is used for client email submission (secure, authenticated)
- Port 25 is restricted by ISP to prevent spam and abuse
- SMTP communication depends on the role:
  - client → server uses port 587
  - server → server uses port 25
- Network connectivity and port accessibility are separate concepts

### Notes 
- Port 25 is mainly used for server-to-server communication
- Port 587 is used for client email submission (recommended)
- SMTP does not handle email retrieval
- SMTP relies on DNS (MX records) to locate destination mail servers

---

## Port : 110/995
- 110 → POP3 (unencrypted)
- 995 → POP3S (encrypted with TLS)

## Name : POP3 (POST OFFICE PROTOCOL VERSION 3)

### Description
- POP3 is used to retrieve emails from a mail server
- A client connects to a POP3 server to download emails locally
- Emails are typically removed from the server after being downloaded
- It is designed for single-device access and offline usage

### How it communicates
- POP3 uses a layered communication model:
- Transport layer: TCP
- Application protocol:
  - POP3 (port 110)
  - POP3S (port 995)

### How it can be attacked
- Weak credentials:
  If passwords are weak or reused, unauthorized access is possible
- Unencrypted communication:
  Using port 110 can expose credentials and email content
- Credential interception:
  Attackers can capture login information over insecure connections
- Unauthorized access:
  Compromised accounts can lead to full mailbox access

### Observation
-

### Notes 
- POP3 downloads emails to the client and often deletes them from the server
- Not suitable for multi-device synchronization
- Considered outdated compared to IMAP in modern environments
- POP3 uses a direct client-to-server communication model (no HTTP or additional protocols)

---

## Port : 143/993
- 143 → IMAP (unencrypted)
- 993 → IMAPS (encrypted with TLS)

## Name : IMAP (INTERNET MESSAGE ACCESS PROTOCOL)

### Description
- IMAP is used to retrieve and manage emails directly on a mail server
- A client connects to an IMAP server to access emails without downloading them locally
- Emails remain stored on the server and are synchronized across multiple devices
- It allows reading, organizing, and managing emails in real time

### How it communicates
- IMAP uses a layered communication model:
- Transport layer: TCP
- Application protocol:
  - IMAP (port 143)
  - IMAPS (port 993)

### How it can be attacked
- Weak credentials:
  If passwords are weak or reused, unauthorized access is possible
- Unencrypted communication:
  Using port 143 can expose credentials and email content
- Credential interception:
  Attackers can capture login information over insecure connections
- Unauthorized access:
  Compromised accounts can allow full access to synchronized mailboxes

### Observation
-

### Notes 
- IMAP keeps emails on the server and synchronizes them across devices
- Suitable for multi-device usage (phone, laptop, web)
- Considered the modern standard for email retrieval
- IMAP uses a direct client-to-server communication model (no HTTP or additional protocols) 

---
