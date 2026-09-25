# SQL injection UNION attack, finding a column containing text

## 1. Vulnerability

**SQL Injection — UNION Data Type Enumeration**

The application is vulnerable to UNION-based SQL injection, allowing an attacker to determine which returned columns can contain string data.

## 2. Objective

Identify a column that accepts text data and use it to display the lab's provided random value.

## 3. Exploitation

1. Intercept the product category request using Burp Suite.
2. Determine that the query returns three columns:

`'+UNION+SELECT+NULL,NULL,NULL--`

3. Replace each `NULL` with the random value provided by the lab, one at a time. For example:

`'+UNION+SELECT+'abcdef',NULL,NULL--`

4. If an error occurs, test the next column.
5. The column that successfully displays the value is compatible with string data.
6. Lab solved.

## 4. Impact

Identifying compatible columns allows attackers to:

* Determine where sensitive data can be extracted.
* Construct effective UNION attacks.
* Retrieve information from other database tables.

## 5. Remediation

* Use **parameterized queries / prepared statements**.
* Prevent user input from altering SQL query structure.
* Apply proper server-side input handling.

## 6. Key Takeaway

**UNION attacks require matching the number and data types of the original query's columns.**

