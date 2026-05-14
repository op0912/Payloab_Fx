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

This query requests all data from the users table.

SQL is heavily used in:
- enterprise infrastructures
- web applications
- cloud environments
- financial systems
- authentication systems
- backend services

---