# Lab 08: SQL Injection – Listing Database Contents

## Lab Description
This lab demonstrates a SQL injection vulnerability that allows enumeration of database contents.
The objective is to identify existing tables and columns within the database using SQL injection techniques.

## Vulnerability Type
- SQL Injection
- Information Disclosure
- Database Enumeration

## Affected Functionality
- Product listing page backed by a SQL database

## Root Cause
The application dynamically builds SQL queries using unsanitized user input.
This allows attackers to access database metadata and enumerate internal database structures.

## Exploitation Summary (High Level)
- The attacker leverages SQL injection to query database metadata.
- Table names and column names are identified from system catalog information.
- The application response confirms the existence of internal database structures.

*(Specific SQL payloads are intentionally omitted for ethical documentation.)*

## Impact
- Exposure of internal database structure
- Enables targeted data extraction attacks
- Increases risk of sensitive data compromise

## Remediation
- Use prepared statements and parameterized queries
- Restrict database metadata access
- Implement strict input validation
- Apply least-privilege principles to database users

## Key Takeaway
Database enumeration is a critical step in SQL injection attacks.
Once attackers understand the structure of the database, sensitive data becomes significantly easier to extract.

## Lab Status
✅ Completed
