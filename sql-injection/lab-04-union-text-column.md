# Lab 04: SQL Injection UNION Attack – Finding a Column Containing Text

## Lab Description
This lab demonstrates a UNION-based SQL injection vulnerability where the attacker must identify which column in the query can display text-based data.
This step is necessary to extract meaningful information using UNION attacks.

## Vulnerability Type
- SQL Injection
- UNION-based Injection

## Affected Functionality
- Product listing page with database-backed filtering

## Root Cause
The application embeds user-controlled input directly into a SQL query without proper parameterization.
As a result, attackers can manipulate the query using UNION statements and observe the application’s response.

## Exploitation Summary (High Level)
- The SQL query returns multiple columns.
- Not all columns can display string data.
- By testing each column with textual input, it is possible to determine which column reflects text in the application response.
- This enables further UNION-based data extraction.

*(Specific payloads are omitted to keep the write-up educational and responsible.)*

## Impact
- Enables retrieval of sensitive database information
- Facilitates further SQL injection exploitation
- Increases risk of full database compromise

## Remediation
- Use prepared statements with parameterized queries
- Enforce strict input validation
- Avoid displaying raw database query results directly to users
- Implement proper error handling

## Key Takeaway
Finding a column that can display text is a critical step in UNION-based SQL injection attacks.
Seemingly minor input handling flaws can lead to serious data exposure risks.

## Lab Status
✅ Completed
