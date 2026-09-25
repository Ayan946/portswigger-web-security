# SQL injection UNION attack, retrieving data from other tables

## 1. Vulnerability

**SQL Injection — UNION Data Extraction**

The product category parameter allows an attacker to use a UNION query to retrieve data from tables that are not part of the application's intended query.

## 2. Objective

Retrieve usernames and passwords from the `users` table and use them to log in as `administrator`.

## 3. Exploitation

1. Intercept the product category request using Burp Suite.
2. Determine that the query returns two text-compatible columns:

`'+UNION+SELECT+'abc','def'--`

3. Query the `users` table:

`'+UNION+SELECT+username,+password+FROM+users--`

4. The response reveals the usernames and passwords.
5. Use the `administrator` credentials to log in.
6. Lab solved.

## 4. Impact

UNION-based SQL injection can allow attackers to:

* Retrieve data from other database tables.
* Expose usernames and passwords.
* Access privileged accounts.
* Extract sensitive application data.

## 5. Remediation

* Use **parameterized queries / prepared statements**.
* Apply least-privilege database permissions.
* Store passwords securely using strong password hashing.
* Never expose database contents through application responses.

## 6. Key Takeaway

**A UNION SQL injection can turn a restricted query into a mechanism for extracting data from other database tables.**

