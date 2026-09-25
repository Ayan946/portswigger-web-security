# SQL injection UNION attack, retrieving multiple values in a single column

## 1. Vulnerability

**SQL Injection — UNION Data Concatenation**

The application is vulnerable to UNION-based SQL injection, and only one of the returned columns is suitable for text. Multiple database values can therefore be combined into a single output column.

## 2. Objective

Retrieve usernames and passwords from the `users` table when only one column can display text.

## 3. Exploitation

1. Intercept the product category request using Burp Suite.
2. Determine that the query returns two columns and only the second accepts text:

`'+UNION+SELECT+NULL,'abc'--`

3. Concatenate the username and password into the same column:

`'+UNION+SELECT+NULL,username||'~'||password+FROM+users--`

4. The `||` operator combines the username and password into a single value separated by `~`.
5. The response reveals the credentials.
6. Use the `administrator` credentials to log in.
7. Lab solved.

## 4. Impact

This technique can allow attackers to:

* Extract multiple values through a single output column.
* Retrieve sensitive credentials.
* Bypass restrictions caused by incompatible column types.

## 5. Remediation

* Use **parameterized queries / prepared statements**.
* Prevent user input from modifying SQL syntax.
* Apply least-privilege database permissions.
* Protect sensitive credentials with secure password hashing.

## 6. Key Takeaway

**When only one column is suitable for text, multiple database values can be concatenated and extracted through that single column.**

