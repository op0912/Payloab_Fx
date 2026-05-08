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
- Port 389 = standard LDAP.

---
- Port 636 = encrypted LDAP (LDAPS).

---
