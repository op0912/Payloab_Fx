# Legacy Network Services

Ports in this section are related to legacy local network communication and system interaction between machines.

They allow:

- resolving machine names to IP addresses within a LAN
- discovering devices on the local network
- establishing basic communication sessions between systems

These services were commonly used in older Windows environments before modern protocols like DNS and SMB over port 445 became standard.

They are mostly limited to local networks and are considered outdated, but may still appear in some internal or misconfigured systems.

---

# Port : 137  
# Name : NetBIOS Name Service (NBNS)

## Definition
- Resolves NetBIOS machine names to IP addresses on a local network  
- Legacy name resolution system used in older Windows environments  
- Used for identifying devices by name within a LAN  

## How it communicates
- Uses UDP  
- A machine sends a name query (who is X)  
- The target machine replies with its IP address  
- Can use broadcast or a WINS server  

## How it can be attacked
- Spoofing: attacker sends fake name resolution responses  
- Poisoning: attacker impersonates a legitimate machine  
- Can lead to man-in-the-middle attacks in a LAN  

## Observation
-

## Notes
- Legacy network service  
- Similar concept to DNS but for local machine names  
- Resolution methods include broadcast, WINS, and LMHOSTS  
- Node types define the order of resolution methods  
- Mostly replaced by DNS in modern environments  

---

## Port : 138  
## Name : NetBIOS Datagram Service (NBDS)

### Definition
- Service used to send messages and announcements across a local network  
- Allows machines to broadcast their presence and exchange simple information  
- Part of the NetBIOS suite used in legacy Windows environments  

### How it communicates
- Uses UDP  
- Sends broadcast messages to all devices on the network  
- Does not establish a connection (connectionless communication)  

### How it can be attacked
- Network discovery: attacker can identify active machines  
- Information leakage: machine names and presence can be exposed  
- Sniffing: attacker can monitor broadcast traffic on the network  

### Observation
-

### Notes
- Legacy network service  
- Used for broadcast and network discovery  
- Often noisy due to broadcast traffic  
- Mostly replaced by modern discovery and name resolution methods  

---

## Port : 139  
## Name : NetBIOS Session Service (NBSS)

### Definition
- Service used to establish a communication session between two machines  
- Enables data exchange such as file sharing and printer access  
- Used by older SMB implementations over NetBIOS  

### How it communicates
- Uses TCP  
- Establishes a connection between a client and a specific machine  
- Maintains a session for reliable data exchange  

### How it can be attacked
- Unauthorized access to shared resources  
- Brute force attempts on network shares  
- Interception of data if not secured  
- Exploitation of outdated SMB configurations  

### Observation
-

### Notes
- Legacy network service  
- Used with older SMB (before port 445)  
- Requires a direct connection between machines  
- Should not be exposed outside of a local network  
