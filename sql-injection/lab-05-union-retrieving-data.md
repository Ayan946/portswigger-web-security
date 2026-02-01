# Lab 05: SQL Injection UNION Attack – Retrieving Data from Other Tables

## Lab Description
This lab demonstrates a UNION-based SQL injection vulnerability that allows retrieval of data from other database tables.
The objective is to extract sensitive information by combining the results of the original query with data from another table.

## Vulnerability Type
- SQL Injection
- UNION-based Injection
- Information Disclosure

## Affected Functionality
- Product listing page with database-driven content

## Root Cause
The application directly concatenates user input into a SQL query without parameterization.
This allows attackers to append UNION SELECT statements and retrieve data from arbitrary tables in the database.

## Exploitation Summary (High Level)
- The attacker first identifies the correct number of columns and a column capable of displaying text.
- Using a UNION query, data is selected from another table present in the database.
- The application renders this data in the response, confirming successful exploitation.

*(Specific payloads are intentionally omitted for responsible and ethical documentation.)*

## Impact
- Exposure of sensitive database information
- Unauthorized access to internal application data
- Increased risk of account compromise and data leaks

## Remediation
- Use parameterized queries (prepared statements)
- Restrict database user privileges
- Validate and sanitize all user inputs
- Avoid exposing database query results directly in application responses

## Key Takeaway
Once a UNION-based SQL injection is possible, attackers can pivot from simple reconnaissance to full data extraction.
Strong input handling and query parameterization are critical to preventing these attacks.

## Lab Status
✅ Completed
