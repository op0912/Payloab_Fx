# Core Communication Services

Ports and mechanisms in this section are related to internal system communication between services and programs.

They allow:
- communication between processes on the same machine or across the network
- execution of functions on remote systems
- interaction between core system components
- they are not traditional network services (like HTTP or SMB)
- they act as communication layers used by other services
- they do not always rely on a single fixed port
- they often use a discovery port (e.g. 135) and dynamic ports for communication
- they are essential for system operations, remote administration, and service interaction
- examples include RPC, used by components such as WMI, DCOM, and other Windows services

---

## Port:
- 135 (Endpoint Mapper)
- Dynamic Ports (RPC Communication)

## Name:
- RPC (Remote Procedure Call)

### Definition
- RPC is a communication mechanism that allows a program or service to execute functions on another system (or process) as if they were local
- It is widely used in Windows for system communication and remote administration

### How it communicates
- Uses port 135 (RPC Endpoint Mapper) to locate the target service
- After discovery, communication continues on dynamic ports (e.g. 49152+)
- Can use multiple transports depending on context:
  - TCP
  - SMB
  - HTTP / HTTPS
- Core components:
  - RpcEptMapper → returns the port of the requested service
  - RpcSs → handles the RPC communication
- Common usage:
  - WMI (Winmgmt)
  - DCOM (DcomLaunch)
  - SMB-related services (LanmanServer / LanmanWorkstation)

### How it can be attacked
- Used for remote code execution
- Enables lateral movement between systems
- Allows remote service manipulation
- Can be abused through WMI / DCOM
- Often leveraged through SMB-based tools and techniques
- If exposed, it can allow interaction with system-level services

### Observation
- RPC runs as background Windows services:
  - RpcSs
  - RpcEptMapper
- Hosted inside svchost.exe
- Port 135 is in LISTENING state:
  - netstat -ano | findstr ":135"
- Services can be mapped using:
  - tasklist /svc /fi "PID eq XXXX"
- Typical behavior:
  - connection to port 135
  - server responds with a dynamic port
  - communication continues on that port

### Notes
- RPC is not a single protocol but a communication framework
- It acts as a bridge between services and systems
- Many Windows components depend on RPC
- Common pattern:
  - connect to 135
  - receive target port
  - communicate on dynamic port
- Understanding RPC helps explain:
  - Active Directory behavior
  - remote administration
  - lateral movement techniques

---
