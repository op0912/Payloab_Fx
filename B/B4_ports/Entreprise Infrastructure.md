# Enterprise Infrastructure & Active Directory

## Description

Core enterprise network services commonly found in Windows domain environments and large corporate infrastructures.

This section focuses on:
- authentication
- directory services
- remote service communication
- enterprise system interaction

Services covered here are heavily related to:
- Active Directory
- domain environments
- centralized management
- enterprise administration
- internal infrastructure communication

---

## Port : 389 / 636
## Name : LDAP / LDAPS (Lightweight Directory Access Protocol)

### Definition
- LDAP is a protocol used to query directory information.
- It is commonly used with Active Directory in enterprise environments.
- LDAP allows systems and applications to retrieve information about users, groups, computers, and access-related data.

### How it communicates
- LDAP uses a client → server communication model.
- A client sends a query to the directory server.
- The server responds with matching information.
- LDAP runs over TCP.
- Port 389 = standard LDAP.
- Port 636 = encrypted LDAP (LDAPS).

### How it can be attacked
- LDAP can expose information about users, groups, and enterprise structure.
- Misconfigured LDAP permissions may reveal excessive directory information.
- Unencrypted LDAP traffic may expose sensitive information on the network.

### Observation
- No real LDAP observation performed yet.
- Current understanding is based on conceptual analysis of Active Directory and enterprise authentication workflows.

### Notes
- LDAP mainly works with an attribute=value logic.
- Example:
  - cn=admin*
- LDAP is mainly used to retrieve information from a directory.
- Active Directory stores the information.
- LDAP is used to access and query that information.
- *Port 389 = standard LDAP.*
- *Port 636 = encrypted LDAP (LDAPS).*

---

## Port :
88

## Name :
Kerberos

### Definition
- Kerberos is a network authentication protocol mainly used in Active Directory environments.
- It is designed to authenticate users and services securely within a domain.
- Kerberos uses tickets distributed by the KDC (Key Distribution Center) instead of constantly sending passwords across the network.
- It is one of the main authentication systems used in modern Windows enterprise infrastructures.

### How it communicates
- Kerberos mainly uses a client → KDC → service communication model.
- A user first authenticates to the KDC.
- The KDC verifies the identity and distributes authentication tickets.
- The user then uses these tickets to access authorized services without repeatedly re-entering credentials.
- Kerberos mainly runs over TCP/UDP 88.
- In Active Directory environments, the KDC is commonly integrated into the Domain Controller.

### How it can be attacked
- Kerberos tickets may become valuable targets if stolen by attackers.
- Misconfigured permissions and excessive privileges may increase security risks in enterprise environments.
- Compromised accounts may allow attackers to access additional services inside a domain.

### Observation
- No direct Kerberos observation performed yet.
- Current understanding is based on conceptual analysis of Active Directory authentication workflows and enterprise infrastructure behavior.

### Notes
- Kerberos is heavily related to Active Directory enterprise authentication workflows.
- Kerberos works closely with:
  - Active Directory
  - LDAP
  - Domain Controllers
  - Single Sign-On (SSO)
- Kerberos mainly handles authentication, while permissions and access control are generally managed through groups, ACLs, and Active Directory policies.
- The KDC (Key Distribution Center) verifies identities and distributes tickets.
- Kerberos tickets allow users to access services without constantly resending passwords.
- Authentication = verifying identity.
- Authorization = determining what the authenticated user is allowed to access.
- A Domain Controller commonly hosts:
  - Active Directory
  - Kerberos KDC
  - LDAP
  - DNS services

---
