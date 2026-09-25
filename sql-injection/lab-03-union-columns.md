
# SQL injection attack, querying the database type and version on MySQL and Microsoft

## 1. Vulnerability

**SQL Injection — UNION Attack**

The product category parameter is vulnerable to SQL injection, allowing additional queries to be combined with the original query using `UNION`.

## 2. Objective

Determine the database type and retrieve its version string.

## 3. Exploitation

1. Intercept the product category request using Burp Suite.
2. Determine the number of columns and identify columns that support text. In this lab, there are two text-compatible columns.
3. Confirm this with:

`'+UNION+SELECT+'abc','def'#`

4. Retrieve the database version using:

`'+UNION+SELECT+@@version,+NULL#`

5. The response reveals the database version.
6. Lab solved.

## 4. Impact

SQL injection can allow attackers to:

* Identify database technologies and versions.
* Retrieve sensitive information.
* Enumerate the database structure.
* Build further targeted attacks.

## 5. Remediation

* Use **parameterized queries / prepared statements**.
* Never concatenate user input into SQL queries.
* Restrict database permissions.
* Avoid exposing unnecessary database information.

## 6. Key Takeaway

**Database version information can help an attacker understand the target and select appropriate follow-up techniques.**
