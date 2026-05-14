# Database Services

Ports in this section are related to database communication between applications, clients, and database servers.

They allow:
- storing and managing structured data
- handling queries and database transactions
- centralizing application and enterprise data
- allowing applications to communicate with backend databases
- managing authentication, records, permissions, and data processing

Database services are heavily used in:
- enterprise infrastructures
- web applications
- cloud environments
- business management systems
- financial systems
- authentication platforms
- backend application infrastructures

This section focuses on:
- relational database services
- SQL-based communication
- database exposure and attack surface
- client ↔ database server interaction
- enterprise and web infrastructure databases

---

# SQL — Structured Query Language

## Description

SQL (Structured Query Language) is a language mainly used to communicate with relational databases.

SQL allows:
- reading data
- inserting data
- modifying data
- deleting data
- organizing database structures

Relational databases organize information into tables that can be linked together through relationships.

Example:
- users
- orders
- employees
- payments

SQL queries are sent from:
- applications
- users
- backend systems
- database clients

toward a DBMS (Database Management System).

Common DBMS examples:
- Oracle
- MSSQL
- MySQL
- PostgreSQL

Example SQL query:

```sql
SELECT * FROM users;
```
- Common SQL syntax is generally similar across most relational database systems.

Common SQL commands:
```sql
SELECT * FROM users;
```
- Reads and retrieves data from a table.

```sql
INSERT INTO users VALUES (...);
```
- Inserts new data into a table.

```sql
UPDATE users SET name='John';
```
- Modifies existing data inside a table.

```sql
DELETE FROM users;
```
- Deletes data from a table.

- SQL syntax may slightly vary depending on the DBMS used.
- Most relational database systems share common SQL concepts, but vendors often implement their own features, functions, and syntax variations.
- Different database systems evolved separately over time and developed their own enterprise-specific implementations.
This query requests all data from the users table.

SQL is heavily used in:
- enterprise infrastructures
- web applications
- cloud environments
- financial systems
- authentication systems
- backend services

---

## Port : 1521/TCP

## Name : Oracle Database / Oracle TNS Listener

### Definition
- Oracle is a relational Database Management System (DBMS) developed by Oracle Corporation.
- It is mainly used to store, organize, manage, and process structured enterprise data.
- Oracle databases are heavily used in:
  - enterprise infrastructures
  - banks
  - governments
  - financial systems
  - large corporate environments
- Port 1521/TCP is commonly associated with the Oracle TNS Listener service.

### How it communicates
- Oracle mainly uses a client ↔ server communication model.
- Applications, users, or backend systems send SQL queries toward the Oracle database server.
- Oracle commonly communicates over TCP 1521.
- The Oracle TNS Listener listens for incoming Oracle client connections and redirects them toward the correct database instance.
- Client systems usually use dynamic source ports when connecting to the Oracle server.
- Oracle communication commonly follows this simplified flow:

```text
Client/Application
↓
TCP connection
↓
Oracle TNS Listener (1521)
↓
Oracle Database
```

- SQL queries and database responses are transmitted through the established TCP connection.

### How it can be attacked
- Exposed Oracle databases may become high-value enterprise targets.
- Weak credentials may lead to unauthorized database access.
- Older Oracle systems may contain vulnerabilities or outdated configurations.
- Misconfigured databases may expose sensitive enterprise information.
- Attackers may attempt:
  - enumeration
  - credential attacks
  - database exploitation
  - privilege escalation
- Publicly exposed database services increase attack surface significantly.

### Observation
- No direct Oracle database interaction performed yet.
- Current understanding is based on:
  - network communication analysis
  - SQL/database concepts
  - enterprise infrastructure research
  - Oracle client ↔ server communication logic

### Notes
- DBMS = Database Management System.
- Oracle is a relational database system heavily associated with enterprise infrastructures.
- Oracle still remains widely used today in:
  - banks
  - governments
  - large corporations
  - critical infrastructures
- Oracle is often associated with older enterprise environments, but modern Oracle systems are still actively maintained and secured.
- TCP 1521 mainly represents the Oracle TNS Listener service.
- The TNS Listener listens for incoming Oracle client connections and redirects them toward the database service.
- Oracle communication relies on TCP sessions between client systems and the Oracle server.

---