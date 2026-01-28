# SQL Injection – WHERE Clause (Retrieval of Hidden Data)

## Vulnerability Type
SQL Injection

## Lab Objective
Exploit a SQL injection vulnerability in the WHERE clause to retrieve hidden data that is not normally visible to users.

## Root Cause
The application directly included user-controlled input in a SQL WHERE clause without proper validation or parameterized queries.

Because of this, an attacker could manipulate the query logic executed by the database.

## What Went Wrong (High-Level)
The application assumed that user input would only filter existing data.  
Instead, crafted input altered the condition of the WHERE clause, causing the database to return unintended results.

## Security Impact
An attacker could:
- Access hidden or restricted data
- Bypass intended data filtering logic
- Expose sensitive business or user information

This vulnerability can lead to unauthorized data disclosure.

## How the Issue Was Identified
By modifying input that affected the WHERE clause and observing changes in the application’s response, it became clear that the backend query logic was being altered.

This behavior confirmed the presence of a SQL injection vulnerability.

## Mitigation / How to Fix
- Use parameterized queries (prepared statements) for all database interactions
- Avoid constructing SQL queries using string concatenation
- Enforce strict server-side input validation
- Apply least-privilege permissions to database users

## Key Takeaway
Filtering data using user input is risky if proper safeguards are not in place.  
SQL injection can occur even in simple WHERE clauses when input is not handled securely.

---

*Lab Source:* PortSwigger Web Security Academy  
*Lab Name:* SQL injection vulnerability in WHERE clause allowing retrieval of hidden data  
*Level:* Apprentice
