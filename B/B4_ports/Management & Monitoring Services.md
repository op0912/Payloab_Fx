# Management & Monitoring Services

Ports in this section are related to monitoring, managing, and collecting information from systems and network devices.

They allow:

- retrieving system and network status (CPU, memory, interfaces)
- collecting logs and events from devices
- monitoring performance and availability of systems
- detecting issues and abnormal behavior in a network

These services are commonly used in enterprise environments to maintain visibility and control over infrastructure.

---

## Port : 161 / 162 (UDP)
## Name : SNMP (Simple Network Management Protocol)

### Definition
- SNMP is a network protocol used to monitor and manage devices remotely
- It allows a system (manager) to request information from another system (agent)
- Commonly used to retrieve system data such as CPU usage, memory, network traffic, and device status
- SNMP uses OIDs (Object Identifiers) and MIBs to structure and access data

### How it communicates
- Uses UDP for lightweight and fast communication
- Port 161:
  - Used for requests and responses (GET, SET, GET NEXT)
  - Manager → Agent (request)
  - Agent → Manager (response)
- Port 162:
  - Used for traps (alerts)
  - Agent → Manager (unsolicited message)
- No persistent connection or session (no handshake)

### How it can be attacked
- Information disclosure:
  - SNMP can expose sensitive system data (network structure, device info)
- Weak authentication:
  - Community strings like "public" or "private" are often used
- Unauthorized access:
  - If write access is enabled, attacker can modify configurations
- Possible actions:
  - Change network settings
  - Disable interfaces
  - Reboot device
- Used for reconnaissance and pivoting inside a network
- Enumeration:
  - attacker can query SNMP to extract detailed system information
  - used to map the network and identify targets

### Observation
-

### Notes
- SNMP does not provide full system control (unlike SSH)
- Port 161 is active (interaction), port 162 is passive (alerts)
- Common on routers, switches, servers, and printers
- SNMPv1/v2:
  - use community strings (clear text, weak security)
- SNMPv3:
  - supports authentication and encryption

---

---

## Port : 514
## Name : SYSLOG (SYSTEM LOGGING PROTOCOL)

### Definition
- Syslog is a logging service used to send and centralize logs from multiple devices to a central server
- It is used by systems such as servers, routers, firewalls and network devices
- It allows reporting of events and activities for monitoring, troubleshooting and security analysis
- Logs are usually sent in plain text format
- Core function: sending event-based messages such as login attempts, system errors, service activity and network events

### How it communicates
- Uses mainly UDP (port 514)
- Stateless communication (no session)
- One-way communication:
  - client (device) → sends logs
  - server → receives and stores logs
- No guarantee of delivery (UDP)
- No built-in encryption or authentication
- Architecture:
  - Syslog client: device generating and sending logs (Linux server, firewall, router)
  - Syslog server: central system collecting logs for analysis

### How it can be attacked
- Log Injection:
  - attacker sends fake logs to confuse monitoring or hide malicious activity
- Sniffing:
  - logs can be captured over the network (clear text)
  - exposes usernames, IPs, services and system information
- Log Flooding (DoS):
  - attacker sends large amounts of logs to overwhelm the server
- Information Gathering:
  - attacker analyzes logs to map the network and identify targets
- Weaknesses exploited:
  - no encryption → data exposure
  - no authentication → fake log injection
  - no integrity → log tampering possible

### Observation
-

### Notes
- Syslog is a passive logging system (no interaction or control over devices)
- Client = device sending logs, NOT the human reading them
- Centralization creates a critical point (high-value target)
- If compromised, attacker can view, modify or delete logs
- Insecure by default (no encryption, authentication, integrity)
- Secure alternative: Syslog over TLS (port 6514)

---
