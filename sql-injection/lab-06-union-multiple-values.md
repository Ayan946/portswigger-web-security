# Lab 06: SQL Injection UNION Attack – Retrieving Multiple Values in a Single Column

## Lab Description
This lab demonstrates a UNION-based SQL injection vulnerability where multiple database values must be extracted through a single visible column.
The objective is to combine multiple fields into one output column to retrieve meaningful data.

## Vulnerability Type
- SQL Injection
- UNION-based Injection
- Information Disclosure

## Affected Functionality
- Product listing page backed by a SQL query

## Root Cause
The application constructs SQL queries using unsanitized user input.
Because of this, UNION queries can be injected and manipulated to merge multiple database values into a single column displayed in the response.

## Exploitation Summary (High Level)
- The original query returns only one column capable of displaying text.
- Multiple database values are concatenated into that single column.
- The combined output is rendered in the application response, confirming successful data extraction.

*(Specific payloads are intentionally omitted for ethical documentation.)*

## Impact
- Exposure of sensitive database records
- Increased risk of credential disclosure
- Enables full data extraction despite limited output channels

## Remediation
- Use parameterized queries for all database interactions
- Apply strict input validation
- Limit database permissions to only what is required
- Avoid directly reflecting database output to users

## Key Takeaway
Even when an application restricts visible output to a single column, SQL injection can still be used to extract multiple values.
Defensive coding practices must be consistent across all query logic.

## Lab Status
✅ Completed
