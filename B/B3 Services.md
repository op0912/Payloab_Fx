#  B3 — Services (Application Layer)

##  Core Idea

At this level, network communication is no longer just about machines, IPs, or ports.

It is about **applications requesting services and receiving responses**.

A website is not “just loaded” magically.

It is requested through a chain of actions:

DNS resolves the name  
TCP establishes the connection  
TLS secures it (if HTTPS)  
HTTP requests the content  
the server responds  
the browser loads and renders the page

---

##  High-Level Web Flow

When accessing a website:

1. DNS resolves domain → IP  
2. Connection is established (TCP or QUIC)  
3. TLS secures the connection (HTTPS)  
4. Browser sends HTTP request  
5. Server responds with HTML  
6. Browser loads CSS / JS / images  
7. JavaScript may trigger API requests  
8. Page renders  

---

##  DNS Resolution Process

DNS follows a hierarchical process:

PC cache → Router cache → DNS resolver → Root → TLD → Authoritative → Response

---

### Step by step

1. The PC checks its local DNS cache  
2. If not found, it queries the router (gateway)  
3. The router may answer from its cache  
4. If not found, the request is sent to a DNS resolver (ISP or public like Google DNS)  
5. The resolver queries:
   - Root servers (.)
   - TLD servers (.com, .org, .mn, etc.)
   - Authoritative server (final answer)

---

### Key Points

- DNS is hierarchical  
- Each level redirects the query  
- The authoritative server provides the final IP  
- Results are cached  
- Multiple IPs can be returned (load balancing)

---

##  TCP Connection (Transport Layer Link/B2 continuity)

Before any HTTP request, a connection must be established.

### TCP Handshake (B2)

- SYN → client initiates connection  
- SYN-ACK → server responds  
- ACK → connection established  

### Key Idea (B2)

TCP creates a reliable communication channel before data is exchanged.

---

##  HTTP vs HTTPS

### HTTP

- Unencrypted  
- Data readable and modifiable  
- No authentication  

---

### HTTPS

- HTTP over TLS  
- Encrypted  
- Authenticated via certificate  
- Integrity protected  

---

### Modern Behavior

- HTTP is still supported but rarely used directly  
- Most sites force HTTPS (redirect / HSTS)  

---

##  TLS Handshake

### Goal

- Secure communication  
- Exchange keys  
- Verify server identity  

---

### Simplified Flow

1. Client Hello  
2. Server Hello  
3. Certificate sent  
4. Key exchange  
5. Secure channel established  
6. HTTP begins over TLS  

---

### Key Concepts

- Certificate proves identity  
- Issued by trusted CA  
- Public / Private / Session keys used  

---

### Key Insight

TLS provides:
- confidentiality  
- integrity  
- authentication  

---

##  HTTP Request Example

Example of a basic request:

GET / HTTP/1.1  
Host: example.com  

---

##  HTTP Versions

- HTTP/1.1 → legacy (TCP)  
- HTTP/2 → multiplexing (TCP)  
- HTTP/3 → QUIC (UDP)  

### Key Points

- HTTPS = HTTP + TLS  
- HTTP/3 uses QUIC (UDP instead of TCP)  
- QUIC replaces TCP in HTTP/3  
- Browser selects best protocol automatically  
- Multiple versions can coexist  

---

##  DHCP (Real Behavior)

### Role

Automatically assigns network configuration

---

### DORA Process

1. DISCOVER → broadcast request for IP  
2. OFFER → server proposes IP + config  
3. REQUEST → client accepts  
4. ACK → server confirms  

---

### Key Points

- Happens automatically on network connection  
- DHCP server often = router  
- Provides:
  - IP  
  - subnet mask  
  - gateway  
  - DNS  

---

#  Observations — B3 (Real Network Behavior)

## LAB 1 — Local Network Configuration

### Command
ipconfig /all

### Observations
- IPv4 address identified (private LAN address)
- Default gateway identified (router)
- DHCP server = same as gateway
- DNS servers:
  - local gateway (DNS forwarder)
  - external resolver

### Understanding
The machine:
- receives its configuration via DHCP
- uses the router as network exit (gateway)
- uses DNS servers to resolve domain names

---

## LAB 2 — DNS vs Ping Behavior

### Commands
ping google.com  
nslookup google.com  

### Observations
- IP addresses from ping and nslookup were different
- Multiple nslookup executions returned different IPs
- Observed IP range: 64.233.178.X

### Understanding
- DNS is dynamic
- A domain does not map to a single IP
- Google = multiple servers
- DNS returns multiple possible IPs
- The client selects one IP for actual communication

---

## LAB 3 — Direct IP Testing

### Command
ping 64.233.178.113

### Observations
- 4/4 packets received
- ~20 ms latency

### Interpretation
- The IP is reachable
- Belongs to Google's infrastructure

---

## LAB 4 — Reverse DNS

### Command
nslookup 64.233.178.113

### Result
ol-in-f113.1e100.net

### Understanding
- Reverse DNS does not return "google.com"
- It returns internal infrastructure naming
- 1e100 = googol → origin of "Google"

---

## LAB 5 — Unknown Domain Resolution

### Command
nslookup montsame.mn

### Result
103.17.109.76

### Understanding
- DNS works globally
- No prior visit required

---

## LAB 6 — Reverse DNS Failure

### Command
nslookup 103.17.109.76

### Result
Server failed

### Understanding
- Reverse DNS is optional
- Not always configured

---

## LAB 7 — Ping Failure

### Commands
ping montsame.mn  
ping 103.17.109.76  

### Observations
- 100% packet loss
- No ICMP response

### Understanding
- ICMP likely blocked
- Ping failure ≠ server unavailable

---

## LAB 8 — Tracert Analysis

### Command
tracert montsame.mn

### Observations
- Path visible across multiple networks
- Backbone identified (twelve99)
- European nodes observed (London, Paris, Frankfurt)
- Destination region reached (Mongolia)
- Final hops hidden (* * *)

### Understanding
- Traffic reaches destination region
- Final network blocks ICMP
- Tracert shows partial path only

---

## LAB 9 — Extended Hop Testing

### Commands
tracert -h 50  
tracert -h 100  

### Observations
- No additional visibility
- Continued timeouts

### Understanding
- Not a routing loop
- No ICMP response from final network

---

## LAB 10 — HTTP vs HTTPS

### Observations

- HTTP automatically redirected to HTTPS  
- HTTP rarely usable directly  

---

### TLS Certificate

- CN: *.facebook.com  
- Organization: Meta  
- Issuer: DigiCert  

---

### Protocol Observation

Observed:

- HTTP/1.1  
- HTTP/2 (h2)  
- HTTP/3 (h3)  

---

### Critical Insight

- A single page uses multiple HTTP versions  
- Different resources use different protocols  
- Browser selects best protocol automatically  

---

### Insecure Site

- Invalid certificate (ERR_CERT_DATE_INVALID)  
- Browser blocks access  
- Manual bypass possible (unsafe)  
- Mixed protocols observed  

---

##  Final Observations

- DNS works independently of connectivity  
- Domains map to multiple IPs  
- Reverse DNS is optional  
- Ping is not reliable alone  
- Tracert shows partial paths  
- HTTP is deprecated in practice  
- HTTPS is enforced  
- Multiple protocols coexist  
- Internet is distributed and dynamic  

---

##  Final Understanding

Modern web communication:

DNS → TCP/UDP → TLS → HTTP → multiple requests → rendering  

Security is enforced by default.
