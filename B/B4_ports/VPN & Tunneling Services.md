# VPN & Tunneling Services

## Description

Services in this section are related to secure remote communications and encrypted network tunneling.

This section focuses on:
- VPN communication
- encrypted tunnels
- remote secure access
- VPN negotiation protocols
- secure communication across public networks

Services covered here are heavily related to:
- IPSec VPN
- remote enterprise access
- site-to-site VPNs
- secure tunneling
- encrypted network communication

---

## Port :
500/UDP

## Name :
ISAKMP / IKE (IPSec VPN)

### Definition
- ISAKMP and IKE are protocols mainly used to negotiate and establish IPSec VPN tunnels.
- They are responsible for exchanging keys, negotiating encryption settings, and preparing secure VPN communications.
- These protocols are heavily used in enterprise VPN infrastructures and remote secure access environments.

### How it communicates
- ISAKMP/IKE mainly use a client ↔ server communication model.
- Before a VPN tunnel is established, both sides negotiate:
  - encryption methods
  - authentication
  - security parameters
  - cryptographic keys
- ISAKMP/IKE mainly run over UDP 500.
- Once negotiation is completed, IPSec can begin securing the traffic through the VPN tunnel.

### How it can be attacked
- Misconfigured VPN services may expose enterprise infrastructure to attackers.
- Weak authentication methods may increase security risks.
- Exposed VPN services may become targets for enumeration and unauthorized access attempts.

### Observation
- No direct ISAKMP/IKE observation performed yet.
- Current understanding is based on conceptual analysis of VPN communication and enterprise remote access infrastructure.

### Notes
- VPN = Virtual Private Network.
- VPNs are used to create secure encrypted tunnels across public networks such as the Internet.
- IPSec mainly secures and encrypts the VPN traffic.
- IKE mainly handles key exchange and security negotiation.
- ISAKMP mainly provides the framework and structure used during VPN security negotiation.
- Port 500 does not represent the VPN tunnel itself.
- Port 500 is mainly related to the negotiation and establishment phase of IPSec VPN communications.
- VPNs were historically used to securely connect remote employees and distant offices without requiring expensive dedicated physical lines.
- Modern enterprises still heavily use VPN technologies for:
  - remote work
  - secure internal access
  - site-to-site communication
  - enterprise infrastructure connectivity

---

