# B1 — Network Basics

## Core Idea
A network = machines exchanging packets through multiple intermediaries (routers).

## IP Addressing

- Private IP (ex: 192.168.x.x)
  - used inside LAN
  - not routable on Internet

- Public IP
  - used on Internet
  - assigned by ISP

## NAT (Network Address Translation)

- translates private IP → public IP
- allows multiple devices to share one public IP

## PAT (Port Address Translation)

- assigns unique ports to each connection
- allows multiple simultaneous connections using one public IP


# Router (Default Gateway)

- example: 192.168.2.1
- role:
  - receives packets from local network
  - performs NAT / PAT
  - forwards traffic to Internet

Important:
- router is NOT the final destination
- it is an intermediary

---

## Packet Flow (Real)

PC → Router → ISP → Internet → Server → return path

Important:
- packets travel hop by hop
- never go directly to destination
- path is dynamic (not fixed)

---

# DNS (Domain Name System)

- translates domain → IP
- ex: google.com → 142.x.x.x

### Process:
1. PC asks configured DNS (usually router)
2. router checks cache
3. if not found → asks ISP DNS
4. response returns to PC

### Key Points:

- multiple DNS = redundancy
- DNS cache = faster responses
- without DNS:
  - domain names ❌
  - direct IP ✔️



# Netmask

- defines network boundary
- determines if destination is local or remote

Example:
IP:      192.168.2.10  
Mask:    255.255.255.0  

→ network = 192.168.2.X

## Binary Explanation (Important)

- each part of an IP = 1 octet (8 bits)

- an octet can go from:
  00000000 → 11111111  
  (0 → 255)
  binary values:

128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 = 255

## Netmask Meaning

255 = 11111111 → network part  
0   = 00000000 → host part  

### Example:

255.255.255.0

→ binary: 11111111.11111111.11111111.00000000

### Interpretation:

- first 3 octets = network  
- last octet = host  

→ network = 192.168.2.X

## Behavior

- same network → direct communication  
- different network → goes through router  

Examples:

- 192.168.2.10 → 192.168.2.200 → DIRECT  
- 192.168.2.10 → 192.168.3.5   → ROUTER  
- 192.168.2.10 → 8.8.8.8       → ROUTER 


# Tools

## ipconfig

Shows:
- IP address
- gateway
- DNS
- DHCP server
## DHCP vs Gateway

- DHCP server assigns:
  - IP
  - netmask
  - gateway
  - DNS

- Gateway = router (Internet exit)

Important:
- often same device at home
- can be different in enterprise networks

### Public IP & DNS (Real Debugging)

### Step 1 — Checking local network

I used:

ipconfig

---

### What I saw:

- IPv4: 192.168.2.10 → private IP
- Gateway: 192.168.2.1 → router

---

### Problem

- I could NOT see my public IP
- I understood that:
  → private IP is not visible on Internet

---

### Step 2 — Finding public IP

I used:

curl ifconfig.me

---

### Result:

- returned HTML page (not useful)

---

### Fix:

curl ifconfig.me/ip

---

### Result:

65.92.82.167 → my public IP

---

### What I understood:

- websites see my public IP, not 192.168.x.x
- NAT translates my private IP → public IP

---

## DNS Discovery

### Problem

- I did not see DNS clearly in ipconfig

---

### Solution

I used:

ipconfig /all

---

### Result:

- DNS servers:
  - 192.168.2.1 (router)
  - ISP DNS

---

### What I understood:

- router acts as DNS relay
- DNS is not always obvious in basic ipconfig
- /all gives full network details

### tracert

Command (Windows / PowerShell):

tracert site.com

Example:
tracert google.com



- shows path to destination (hops)
- each hop = router
- used for network troubleshooting

---

## How tracert works

- sends 3 packets per hop
- displays 3 latency values (ms ms ms)

Example:
1     3 ms     4 ms     3 ms

---

## Important Observations

- 1st hop = almost always the router (default gateway)
  ex: 192.168.2.1

- each hop = step in network path

- can estimate location using:
  - latency jumps
  - hostnames (ex: hkg = Hong Kong, dub = Dublin)

---

## Latency & Distance

- 1–30 ms → local / same region
- 50–120 ms → continent
- 200+ ms → long distance (ex: Asia)

Important:
- latency ≈ distance
- number of hops ≠ distance

Example:
- 20 hops → can be local
- 10 hops → can cross the world

---

## Packet Loss (*)

- `*` = packet lost or ICMP blocked
- `* * *` ≠ network failure
- packets can still reach destination

---

## Real Observations

I tested tracert to multiple locations:

- google.com (North America)
- google.com.au (Australia)
- zing.vn (Vietnam)
- www.southafrica.net (Africa)

---

### What I observed:

- latency increases with distance
- routes change depending on destination
- backbone providers change

Examples:

- Google → about 20 ms
- Vietnam / Hong Kong → ~ about 250 ms

---

### Identified locations:

- Hong Kong (hkg)
- Dublin (dub)

---

## Cloud / Backbone Insight

- large providers (ex: Microsoft Azure) have their own network backbone
- once inside:
  - traffic stays internal
  - multiple hops are within same provider

---

## Key Insights

- Internet = network of routers
- packets travel hop by hop
- routing is dynamic
- tracert shows ICMP responses, not exact traffic flow
- latency helps estimate distance
- hops ≠ distance
- private IP ≠ public IP
- public IP is obtained through Internet request
- NAT hides internal network
- DNS is critical for domain resolution
- troubleshooting requires multiple commands
