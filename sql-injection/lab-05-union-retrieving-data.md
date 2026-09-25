# SQL injection UNION attack, determining the number of columns returned by the query

## 1. Vulnerability

**SQL Injection — UNION Column Enumeration**

A UNION-based SQL injection can be used to determine how many columns are returned by the original query.

## 2. Objective

Determine the number of columns returned by the application's SQL query.

## 3. Exploitation

1. Intercept the product category request using Burp Suite.
2. Start a UNION query with one `NULL` value:

`'+UNION+SELECT+NULL--`

3. An error indicates that the number of columns does not match.
4. Add additional `NULL` values:

`'+UNION+SELECT+NULL,NULL--`

5. Continue adding columns until the error disappears and additional content is returned.
6. The number of `NULL` values that works represents the number of columns returned by the original query.
7. Lab solved.

## 4. Impact

Determining the column count helps an attacker:

* Construct UNION-based SQL injection payloads.
* Identify suitable locations for retrieving data.
* Continue database enumeration.

## 5. Remediation

* Use **parameterized queries / prepared statements**.
* Never concatenate user-controlled input into SQL queries.
* Apply proper input validation.

## 6. Key Takeaway

**Knowing the number of columns is a fundamental step when constructing a UNION-based SQL injection attack.**

