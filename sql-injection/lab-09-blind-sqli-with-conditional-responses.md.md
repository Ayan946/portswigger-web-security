# Blind SQL injection with conditional responses

## 1. Vulnerability

**Blind SQL Injection — Conditional Responses**

The application does not return SQL query results or errors, but displays a `Welcome back` message when the query returns a row. This difference can be used as a true/false signal.

## 2. Objective

Use the application's response behavior to determine the `administrator` password and log in.

## 3. Exploitation

1. Intercept the `TrackingId` cookie using Burp Suite.
2. Confirm the boolean behavior:

`TrackingId=xyz' AND '1'='1`

The `Welcome back` message appears.

3. Change the condition to false:

`TrackingId=xyz' AND '1'='2`

The message disappears, confirming that the response can be used as a true/false signal.

4. Confirm the `users` table and `administrator` account exist using conditional queries.

5. Test different password lengths with `LENGTH(password)>N` until the response changes. The password is 20 characters long.

6. Use `SUBSTRING(password,N,1)` with Burp Intruder to test each character position against `a-z` and `0-9`.

7. Use the `Welcome back` response to identify the correct character at each position.

8. Repeat for all positions and use the recovered password to log in as `administrator`.

9. Lab solved.

## 4. Impact

Blind SQL injection can allow attackers to:

* Extract sensitive database information without seeing query results.
* Recover credentials character by character.
* Bypass authentication.
* Enumerate database contents.

## 5. Remediation

* Use **parameterized queries / prepared statements**.
* Never place untrusted input directly into SQL queries.
* Avoid response differences that reveal database query results.
* Apply least-privilege database permissions.

## 6. Key Takeaway

**Even when SQL results are hidden, small differences in application behavior can provide enough information to extract sensitive data.**

