# Blind SQL injection with conditional errors

## 1. Vulnerability

**Blind SQL Injection — Conditional Errors**

The application returns a custom error when the SQL query fails. By deliberately triggering an error only when a condition is true, an attacker can use the error response as a boolean signal.

## 2. Objective

Use conditional SQL errors to determine the `administrator` password and log in.

## 3. Exploitation

1. Intercept the `TrackingId` cookie using Burp Suite.
2. Test a single quote and observe the error. Adding a second quote removes it, confirming that the input affects the SQL query.
3. Use:

`TrackingId=xyz'||(SELECT '' FROM dual)||'`

The `dual` table indicates that the target uses an Oracle database.

4. Confirm SQL injection by querying a non-existent table and observing an error.

5. Confirm the `users` table exists using a valid query.

6. Use a `CASE` statement with `TO_CHAR(1/0)` to generate an error only when a condition is true.

7. Test password length with `LENGTH(password)>N` until the condition becomes false. The password is 20 characters long.

8. Use `SUBSTR(password,N,1)` with Burp Intruder to test each character using `a-z` and `0-9`.

9. A `500` response indicates the tested character is correct.

10. Recover the complete password and log in as `administrator`.

11. Lab solved.

## 4. Impact

Conditional error-based SQL injection can allow attackers to:

* Infer database information.
* Extract credentials.
* Enumerate users and tables.
* Bypass authentication.

## 5. Remediation

* Use **parameterized queries / prepared statements**.
* Do not expose database errors to users.
* Use generic error responses.
* Apply least-privilege database permissions.

## 6. Key Takeaway

**Database errors can become an information channel when an attacker can control whether an error occurs.**
