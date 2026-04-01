
# B2 — Transport Layer

## Core Idea

The transport layer manages communication between applications using ports and protocols (TCP / UDP).

It allows multiple applications to communicate simultaneously over the network.

---

## Ports

- ports identify applications (not machines)
- allow multiple connections on the same device

---

### Types of Ports

- Source port:
  - chosen by the client
  - temporary (ephemeral)
  - identifies local application

- Destination port:
  - identifies the service on the server
  - examples:
    - 80 → HTTP
    - 443 → HTTPS
    - 53 → DNS

---

### Example

192.168.2.10:52341 → 142.x.x.x:443

- 52341 = client port
- 443 = server (HTTPS)

---

### Key Insight

- IP = machine
- Port = application
- Connection = IP + Port

---

## Multiple Connections

- one application can open multiple connections at the same time
- each connection uses a different source port

---

### Example (Web Page Load — Real Visualization)

When I type:

google.com

---

## What actually happens (simplified view)

The browser loads multiple resources:

---

### 1. HTML → page structure (skeleton)

- HTML = initial request (first thing loaded)

Example:

<html>
  <head>
    <title>Google</title>
  </head>
  <body>
    <input type="text" placeholder="Search Google">
    <button>Search</button>
  </body>
</html>

---

### 2. CSS → style (colors, layout)

Example:

body {
  background-color: white;
  text-align: center;
}

input {
  border: 1px solid gray;
  width: 300px;
}

---

### 3. JavaScript → logic / behavior

Example:

button.onclick = function() {
  let query = input.value;
  fetch("/api/search?q=" + query);
};

---

### 4. Images → visual elements

Examples:

- logo.png
- search_icon.svg

Browser requests:

GET /logo.png  
GET /search_icon.svg  

---

### 5. API Requests → dynamic data

- API can be triggered:
  - by user interaction (search)
  - automatically when page loads

Example:

GET /api/search?q=weather

Server responds (JSON):

{
  "results": [
    "Weather today: 18°C cloudy"
  ]
}

---

## API (Important Concept)

- API = a way to request data from a server
- returns data (often JSON), not HTML

---

### Key Insight

- JSON = data (transport)
- HTML = display (visual)

---

### Flow

1. client requests data (API)
2. server returns JSON
3. JavaScript processes it
4. page updates dynamically

---

## Important Insight

When loading a website:

- HTML = initial structure
- CSS / JS / images = additional resources
- API = dynamic data (on load or interaction)

---

## Connection Impact (Transport Layer)

Each of these can create separate connections:

- HTML request → 1 connection
- CSS request → 1 connection
- JS request → 1 connection
- images → multiple connections
- API calls → multiple connections

- all these resources (HTML, CSS, JS, images, API) are transferred using transport layer protocols, mainly TCP over HTTPS (port 443)
→ explains why netstat shows many connections

---

## Final Understanding

Typing "google.com" does NOT load one thing.

It loads:

- structure (HTML)
- style (CSS)
- behavior (JavaScript)
- visuals (images)
- data (API)

→ all through multiple TCP connections

---

### Key Insight

- JSON = data (transport)
- HTML = display (visual)

---

### Flow

1. client requests data (API)
2. server returns JSON
3. JavaScript processes it
4. page updates dynamically

---

## TCP vs UDP

### TCP (Transmission Control Protocol)

- connection-oriented
- reliable
- ordered
- retransmits lost packets

---

### TCP Features

- handshake (SYN → SYN-ACK → ACK)
- session tracking
- retransmission
- guaranteed delivery order

---

### UDP (User Datagram Protocol)

- connectionless
- no guarantee
- no retransmission
- faster (low latency)

---

### Use Cases

TCP:
- web (HTTP/HTTPS)
- downloads
- email

UDP:
- gaming
- VoIP
- real-time communication

---

## Important Clarification

- many streaming services (ex: Netflix) use TCP (HTTPS)
- newer protocols (QUIC / HTTP3) use UDP

---

## TCP Handshake

1. SYN → client initiates  
2. SYN-ACK → server responds  
3. ACK → connection established  

---

## TCP States

### LISTENING
- program waiting for incoming connections

---

### ESTABLISHED
- active connection
- data is flowing

---

### CLOSE_WAIT
- remote side closed connection
- local application still open

---

### TIME_WAIT
- connection closed
- OS cleanup phase
- PID often = 0 (handled by OS)

---

## 0.0.0.0 Meaning

- 0.0.0.0 = all interfaces
- service accepts connections from:
  - local machine
  - local network
  - potentially external sources

---

## Security Insight

- LISTENING = open port (service running)
- NOT automatically dangerous

Risk depends on:
- exposure (who can connect)
- vulnerability (service weakness)
- firewall rules

---

# NETSTAT ANALYSIS (REAL LAB — DETAILED)

## Command Used

netstat -ano

---

## What netstat shows

Each line contains:

- protocol (TCP / UDP)
- local address (IP:port)
- remote address (IP:port)
- state (connection status)
- PID (process ID)

---

## Example Breakdown

TCP 192.168.2.10:5215 → 172.x.x.x:443 ESTABLISHED 5020

Meaning:

- TCP = protocol used
- 192.168.2.10:5215 = my machine + source port
- 172.x.x.x:443 = remote server (HTTPS)
- ESTABLISHED = active connection
- 5020 = process using the connection

---

## Step 1 — HTTPS Analysis

Command:

netstat -ano | findstr 443

---

### Observation

- multiple connections to port 443
- many different source ports
- many ESTABLISHED connections

---

### Example

192.168.2.10:5215 → 172.x.x.x:443 ESTABLISHED  
192.168.2.10:5222 → 172.x.x.x:443 ESTABLISHED  

---

### Insight

- one application (browser) opens multiple connections
- each connection uses a unique source port
- destination port remains constant (443)

---

### Additional States Observed

- CLOSE_WAIT → remote closed, local app still processing
- TIME_WAIT → connection closed, OS cleanup

---

## Step 2 — HTTP Analysis (Security Check)

Command:

netstat -ano | findstr 80

---

### Goal

- verify if HTTP (port 80) is actively used
- detect potential exposed services

---

### Observation

- some connections to port 80
- mostly:
  - TIME_WAIT
  - CLOSE_WAIT

---

### Interpretation

- no persistent HTTP service running
- no active LISTENING on port 80
- therefore:
  → no obvious HTTP exposure

---

## Step 3 — LISTENING Ports Analysis

Example:

TCP 0.0.0.0:5040 LISTENING 8980  
TCP 0.0.0.0:7680 LISTENING 10076  
TCP 0.0.0.0:49664 LISTENING 804  

---

### Meaning

- service is waiting for incoming connections
- 0.0.0.0 = accepts connections on all interfaces

---

### Important Insight

- LISTENING = open service
- BUT:
  - not necessarily exposed to Internet
  - depends on firewall and NAT

---

## Step 4 — Process Mapping

Command:

tasklist | findstr <PID>

---

### Example Results

8980 → svchost.exe  
10076 → svchost.exe  
804 → lsass.exe  
12044 → msedge.exe  

---

### Interpretation

- msedge.exe → browser traffic
- svchost.exe → Windows services
- lsass.exe → authentication system

---

## Step 5 — Service Identification

Command:

tasklist /svc | findstr <PID>

---

### Results

svchost.exe → CDPSvc  
svchost.exe → DoSvc  
lsass.exe → KeyIso, SamSs, VaultSvc  

---

### Meaning

- CDPSvc → device communication
- DoSvc → Windows updates
- KeyIso / SamSs / VaultSvc → authentication (LSASS)

---

## Step 6 — Critical Service Analysis

### LSASS (lsass.exe)

- handles authentication
- stores credentials
- validates users

---

### Security Importance

- high-value target for attackers
- used by tools like credential dumpers

---

## Step 7 — Security Action Performed

Identified risk:

- LSASS contains sensitive credentials
- needs protection

---

### Action

Modified registry:

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa

Set:

RunAsPPL = 1

---

### Result

- LSASS runs as Protected Process Light (PPL)
- prevents credential extraction
- increases system security

---

## Key Security Insight

- open port ≠ vulnerability
- must analyze:
  - process
  - service
  - exposure
  - behavior

---

## Final Understanding

- netstat provides visibility into real connections
- ports map to applications
- processes control network activity
- system services generate legitimate traffic
- security = understanding + verification + action

---

## Mindset

- do not assume risk
- investigate before concluding
- always correlate:
  network → process → service → function
