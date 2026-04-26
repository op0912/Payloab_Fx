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

### Observation
-

### Notes
- SNMP does not provide full system control (unlike SSH)
- Port 161 is active (interaction), port 162 is passive (alerts)
- Common on routers, switches, servers, and printers
- SNMPv1/v2 are insecure (no encryption)
- SNMPv3 adds authentication and encryption

---
