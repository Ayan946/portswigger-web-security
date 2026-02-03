# Lab 07: SQL Injection – Querying the Database Type and Version

## Lab Description
This lab demonstrates a SQL injection vulnerability that allows an attacker to determine the underlying database type and version.
Identifying the database technology is an important step for tailoring further attacks and understanding platform-specific behavior.

## Vulnerability Type
- SQL Injection
- Information Disclosure

## Affected Functionality
- Product listing page using a backend SQL query

## Root Cause
The application directly incorporates user input into SQL queries without proper parameterization.
This allows attackers to inject database-specific queries that reveal internal system information.

## Exploitation Summary (High Level)
- The application executes user-influenced SQL queries.
- By injecting database-specific functions or metadata queries, it is possible to identify the database type and version.
- The response confirms the backend database technology in use.

*(Exact payloads are omitted to keep this write-up responsible and educational.)*

## Impact
- Disclosure of database technology and version
- Enables attackers to craft database-specific exploits
- Increases the likelihood of successful follow-up attacks

## Remediation
- Use parameterized queries for all database interactions
- Restrict access to database metadata
- Validate and sanitize all user inputs
- Suppress detailed database error messages in production

## Key Takeaway
Information disclosure through SQL injection significantly lowers the barrier for attackers.
Knowing the database type and version allows attackers to optimize and scale further exploitation.

## Lab Status
✅ Completed
