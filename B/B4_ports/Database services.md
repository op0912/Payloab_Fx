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

## Port : 1433/TCP

## Name : Microsoft SQL Server (MSSQL) / TDS

### Definition
- Microsoft SQL Server (MSSQL) is a relational Database Management System (DBMS) developed by Microsoft.
- It is mainly used to store, organize, manage, and process structured enterprise data.
- MSSQL is heavily associated with:
  - Windows Server environments
  - Active Directory infrastructures
  - Microsoft enterprise ecosystems
  - business and corporate infrastructures
- MSSQL mainly uses the TDS (Tabular Data Stream) protocol for database communication.
- Port 1433/TCP is commonly associated with MSSQL services.

### How it communicates
- MSSQL mainly uses a client ↔ server communication model.
- Applications, users, or backend systems send SQL queries toward the MSSQL server.
- MSSQL commonly communicates over TCP 1433.
- The TDS protocol is mainly used to transport:
  - SQL queries
  - database responses
  - authentication data
  - database communication traffic
- Client systems usually use dynamic source ports when connecting to the MSSQL server.
- MSSQL communication commonly follows this simplified flow:

```text
Client/Application
↓
TDS protocol
↓
TCP connection (1433)
↓
MSSQL Server
```

- Modern MSSQL environments may use TLS encryption to secure database communications.

### How it can be attacked
- Exposed MSSQL services may become high-value enterprise targets.
- Weak credentials may lead to unauthorized database access.
- Misconfigured MSSQL environments may expose sensitive corporate information.
- Older MSSQL systems may contain vulnerabilities or outdated configurations.
- Attackers may attempt:
  - enumeration
  - credential attacks
  - database exploitation
  - privilege escalation
- Publicly exposed database services significantly increase attack surface.

### Observation
- No direct MSSQL interaction performed yet.
- Current understanding is based on:
  - SQL/database concepts
  - Microsoft enterprise infrastructure research
  - network communication analysis
  - MSSQL client ↔ server communication logic

### Notes
- MSSQL is a relational database system developed by Microsoft.
- MSSQL and Oracle generally serve similar enterprise database purposes but use different architectures and communication protocols.
- MSSQL mainly uses the TDS (Tabular Data Stream) protocol for database communications.
- TCP 1433 is mainly associated with MSSQL services.
- MSSQL is heavily integrated into Microsoft enterprise infrastructures and Windows-based environments.
- Modern MSSQL systems may use TLS encryption to secure communications between clients and the database server.
- MSSQL remains heavily used today in enterprise and corporate environments.

---

## Port : 3306/TCP

## Name : MySQL / MySQL Protocol

### Definition
- MySQL is a relational Database Management System (DBMS).
- It is mainly used to store, organize, manage, and process structured data.
- MySQL became heavily associated with:
  - web applications
  - web hosting
  - backend infrastructures
  - CMS platforms
  - Internet services
- MySQL became extremely popular during the growth of the modern web because it was lightweight, accessible, and developer-friendly compared to heavier enterprise database systems.
- MySQL is strongly associated with the historical LAMP stack:
  - Linux
  - Apache
  - MySQL
  - PHP

### How it communicates
- MySQL mainly uses a client ↔ server communication model.
- Applications, backend systems, or users send SQL queries toward the MySQL server.
- MySQL commonly communicates over TCP 3306.
- MySQL mainly uses the MySQL protocol for database communications.
- The MySQL protocol is mainly used to transport:
  - SQL queries
  - authentication data
  - database responses
  - database communication traffic
- Client systems usually use dynamic source ports when connecting to the MySQL server.
- MySQL communication commonly follows this simplified flow:

```text
User
↓
Website / Backend
↓
SQL query
↓
MySQL protocol
↓
TCP connection (3306)
↓
MySQL Server
```

- Modern MySQL environments may use TLS encryption to secure communications.

### How it can be attacked
- Exposed MySQL services may become high-value web infrastructure targets.
- Weak credentials may lead to unauthorized database access.
- Misconfigured MySQL environments may expose sensitive backend data.
- Older MySQL systems may contain vulnerabilities or outdated configurations.
- Attackers may attempt:
  - enumeration
  - credential attacks
  - SQL injection related attacks
  - database exploitation
  - privilege escalation
- Publicly exposed database services significantly increase attack surface.

### Observation
- No direct MySQL interaction performed yet.
- Current understanding is based on:
  - web infrastructure concepts
  - SQL/database concepts
  - backend communication logic
  - client ↔ server database communication analysis

### Notes
- MySQL is a relational database system strongly associated with web infrastructures and backend applications.
- MySQL mainly uses the MySQL protocol for database communications.
- TCP 3306 is mainly associated with MySQL services.
- MySQL became extremely popular during the expansion of the Internet and dynamic web applications.
- MySQL is commonly associated with:
  - PHP
  - CMS platforms
  - web hosting
  - backend web infrastructures
- Modern MySQL systems may use TLS encryption to secure database communications.
- MySQL remains one of the most widely used relational database systems today.


---

## Port :
5432/TCP

## Name :
PostgreSQL / PostgreSQL Protocol

### Definition
- PostgreSQL is a relational Database Management System (DBMS).
- It is an open-source database system mainly developed and maintained by the PostgreSQL Global Development Group.
- PostgreSQL originated from academic and university research environments.
- PostgreSQL is heavily known for:
  - stability
  - robustness
  - technical rigor
  - SQL standards compliance
  - advanced database capabilities
- PostgreSQL is heavily used in:
  - backend infrastructures
  - Linux environments
  - cloud infrastructures
  - DevOps environments
  - modern web applications
  - enterprise backend systems

### How it communicates
- PostgreSQL mainly uses a client ↔ server communication model.
- Applications, backend systems, or users send SQL queries toward the PostgreSQL server.
- PostgreSQL commonly communicates over TCP 5432.
- PostgreSQL mainly uses the PostgreSQL protocol for database communications.
- The PostgreSQL protocol is mainly used to transport:
  - SQL queries
  - authentication data
  - database responses
  - database communication traffic
- Client systems usually use dynamic source ports when connecting to the PostgreSQL server.
- PostgreSQL communication commonly follows this simplified flow:

```text
Client/Application
↓
PostgreSQL protocol
↓
TCP connection (5432)
↓
PostgreSQL Server
```

- Modern PostgreSQL environments may use TLS encryption to secure communications.

### How it can be attacked
- Exposed PostgreSQL services may become high-value backend infrastructure targets.
- Weak credentials may lead to unauthorized database access.
- Misconfigured PostgreSQL environments may expose sensitive backend data.
- Older PostgreSQL systems may contain vulnerabilities or outdated configurations.
- Attackers may attempt:
  - enumeration
  - credential attacks
  - database exploitation
  - privilege escalation
- Publicly exposed database services significantly increase attack surface.

### Observation
- No direct PostgreSQL interaction performed yet.
- Current understanding is based on:
  - SQL/database concepts
  - backend infrastructure research
  - client ↔ server communication analysis
  - PostgreSQL architecture and ecosystem concepts

### Notes
- DBMS = Database Management System.
- PostgreSQL is an open-source relational database system.
- PostgreSQL is heavily associated with:
  - Linux infrastructures
  - cloud environments
  - DevOps ecosystems
  - backend modern web infrastructures
- PostgreSQL originated from university and academic research environments.
- PostgreSQL is widely recognized for technical rigor, robustness, and standards compliance.
- PostgreSQL mainly uses the PostgreSQL protocol for database communications.
- TCP 5432 is mainly associated with PostgreSQL services.
- Modern PostgreSQL systems may use TLS encryption to secure database communications.
- PostgreSQL remains one of the most respected and widely used relational database systems today.

---
