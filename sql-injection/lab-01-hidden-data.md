# SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

## 1. Vulnerability

**SQL Injection in WHERE Clause**

The product category parameter is incorporated into a SQL query without proper sanitization. This allows an attacker to modify the query's logic and retrieve products that are normally hidden.

## 2. Objective

Use SQL injection to display one or more unreleased products.

## 3. Exploitation

1. Intercept the product category request using Burp Suite.
2. Modify the `category` parameter with:

`'+OR+1=1--`

3. The payload makes the `WHERE` condition always true and comments out the remaining query.
4. Send the request and verify that unreleased products are now displayed.
5. Lab solved.

## 4. Impact

SQL injection can allow attackers to:

* Retrieve unauthorized data.
* Bypass application logic.
* Modify or delete database information.
* Potentially compromise backend functionality.

## 5. Remediation

* Use **parameterized queries / prepared statements**.
* Never concatenate user input directly into SQL queries.
* Apply appropriate input validation.
* Use least-privileged database accounts.

## 6. Key Takeaway

**SQL injection allows attacker-controlled input to alter the logic of a database query.**

