# Lab 02: SQL Injection Vulnerability Allowing Login Bypass

## Lab Description
This lab contains a SQL injection vulnerability in the login functionality.
The application uses user-supplied input directly in a SQL query without proper sanitization, allowing an attacker to bypass authentication.

## Vulnerability Type
- SQL Injection
- Authentication Bypass

## Affected Functionality
- Login form (username and password fields)

## Root Cause
The backend SQL query is constructed by directly concatenating user input into the query.
Because of this, crafted input can alter the logic of the SQL statement and force it to return a valid result without knowing valid credentials.

## Exploitation Summary (High Level)
- The application checks credentials using a SQL query.
- By injecting a logical condition that always evaluates to true, authentication checks are bypassed.
- This allows access without valid username or password.

(No exploit payloads are included to keep this write-up educational and responsible.)

## Impact
- Unauthorized access to user accounts
- Complete authentication bypass
- Potential exposure of sensitive user data

## Remediation
- Use parameterized queries (prepared statements)
- Avoid dynamic SQL query construction using user input
- Implement proper input validation and escaping
- Apply least-privilege principles to database users

## Key Takeaway
Authentication mechanisms are a common and high-impact attack surface.
Even simple SQL injection vulnerabilities can completely break access control if input handling is insecure.

## Lab Status
✅ Completed
