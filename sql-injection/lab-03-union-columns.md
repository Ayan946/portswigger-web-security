# Lab 03: SQL Injection UNION Attack – Determining the Number of Columns

## Lab Description
This lab demonstrates a SQL injection vulnerability that allows the use of a UNION-based attack.
The objective is to determine the number of columns returned by the original SQL query in order to prepare further UNION attacks.

## Vulnerability Type
- SQL Injection
- UNION-based Injection

## Affected Functionality
- Product listing page using a database-backed query

## Root Cause
The application directly incorporates user input into a SQL query without proper sanitization or parameterization.
This allows attackers to manipulate the query structure using SQL keywords such as UNION.

## Exploitation Summary (High Level)
- The original SQL query returns a fixed number of columns.
- By injecting UNION SELECT statements and adjusting the number of selected columns, it is possible to infer how many columns the query returns.
- Once the correct column count is identified, UNION-based SQL injection becomes possible.

(Specific payloads are intentionally omitted for responsible disclosure.)

## Impact
- Enables further data extraction attacks
- Acts as a stepping stone for full database compromise
- Can lead to exposure of sensitive application data

## Remediation
- Use parameterized queries (prepared statements)
- Avoid building SQL queries through string concatenation
- Implement strict server-side input validation
- Disable verbose database error messages in production

## Key Takeaway
Determining the number of columns is a critical reconnaissance step in UNION-based SQL injection attacks.
Small input validation flaws can enable attackers to fully control database queries.

## Lab Status
✅ Completed
