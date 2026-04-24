# Core Network Services

Ports in this section are related to the fundamental services that allow a network to function properly.

They allow:

- resolving domain names to IP addresses
- automatically assigning network configuration to devices
- synchronizing time across systems

---

## Port : 53
- 53 → DNS (UDP/TCP)

## Name : DNS (DOMAIN NAME SYSTEM)

### Description
- DNS is used to resolve domain names into IP addresses
- A client sends a request to a DNS server to find the IP address of a domain
- The DNS server responds with the corresponding IP address
- It allows users to access services using human-readable names instead of IP addresses

### How it communicates
- DNS uses a layered communication model:
- Transport layer:
  - UDP (port 53) for most queries (fast)
  - TCP (port 53) for large responses and zone transfers
- Application protocol:
  - DNS

### How it can be attacked
- DNS spoofing:
  Attackers can provide false IP addresses to redirect traffic
- Cache poisoning:
  Malicious responses can be stored in DNS cache
- Amplification attacks:
  DNS can be abused for DDoS using UDP
- Misconfiguration:
  Incorrect DNS setup can expose internal infrastructure

### Observation
-

### Notes 
- DNS is required before most network communications (HTTP, SMTP, etc.)
- Resolves domain names to IP addresses (name → IP)
- Does not transmit application data, only resolution information
- Uses UDP for speed and TCP for reliability when needed
- Without DNS, users would need to remember IP addresses instead of domain names

---

## Port : 67/68
- 67 → DHCP (server)
- 68 → DHCP (client)

## Name : DHCP (DYNAMIC HOST CONFIGURATION PROTOCOL)

### Description
- DHCP is used to automatically assign network configuration to devices
- A client requests an IP address and network settings from a DHCP server
- The server provides configuration such as IP address, subnet mask, gateway, and DNS
- It eliminates the need for manual network configuration

### How it communicates
- DHCP uses a layered communication model:
- Transport layer: UDP
- Application protocol:
  - DHCP (ports 67/68)

- Communication follows the DORA process:
  - Discover → client (68) → server (67)
  - Offer → server (67) → client (68)
  - Request → client (68) → server (67)
  - Acknowledge → server (67) → client (68)

### How it can be attacked
- Rogue DHCP:
  A malicious server provides false network configuration
- DHCP starvation:
  Attackers exhaust the IP address pool to disrupt the network
- Man-in-the-Middle:
  Malicious configuration (gateway/DNS) can redirect traffic
- Misconfiguration:
  Incorrect settings can expose or disrupt network communication

### Observation
-

### Notes 
- DHCP is required before most network communication (IP must be assigned first)
- Uses UDP because the client does not yet have an IP address
- Based on trust, which makes it vulnerable to attacks
- Replaced BOOTP with dynamic and scalable configuration

---

## Port : 123
- 123 → NTP (UDP)

## Name : NTP (NETWORK TIME PROTOCOL)

### Description
- NTP is used to synchronize the time across systems on a network
- A client requests the current time from an NTP server
- The server responds with a reference time which the client uses to adjust its clock
- It ensures consistent time across all devices

### How it communicates
- NTP uses a layered communication model:
- Transport layer: UDP
- Application protocol:
  - NTP (port 123)

- Communication process:
  - client sends a time request to the server
  - server responds with its current time
  - client calculates network delay (latency)
  - client adjusts its clock accordingly (slewing)

- NTP uses a hierarchical structure:
  - Stratum 0 → reference clocks (atomic clocks, GPS)
  - Stratum 1 → servers directly connected to Stratum 0
  - Stratum 2+ → servers synchronized from other NTP servers

### How it can be attacked
- NTP amplification:
  Attackers use NTP servers to generate large amounts of traffic (DDoS)
- Time manipulation:
  Malicious servers can provide incorrect time
- Misconfiguration:
  Incorrect time sources can lead to system desynchronization
- Man-in-the-Middle:
  Attackers can alter time responses in transit

### Observation
-

### Notes 
- NTP is critical for authentication, logging, and certificate validation
- Uses UDP for fast communication with minimal overhead
- Time synchronization is required before many secure operations
- Works in a distributed hierarchy to ensure scalability and reliability

---
