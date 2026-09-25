# SQL injection vulnerability allowing login bypass

## 1. Vulnerability

**SQL Injection in Login Function**

The login function directly incorporates the username into a SQL query, allowing an attacker to manipulate the query and bypass password verification.

## 2. Objective

Use SQL injection to log in as the `administrator` user without knowing the password.

## 3. Exploitation

1. Intercept the login request using Burp Suite.
2. Modify the `username` parameter to:

`administrator'--`

3. The `'` closes the username string and `--` comments out the rest of the SQL query, including the password check.
4. Send the request and the application logs in as `administrator`.
5. Lab solved.

## 4. Impact

SQL injection in authentication functionality can allow attackers to:

* Bypass login controls.
* Access other users' accounts.
* Potentially gain administrative access.
* Retrieve or modify sensitive data.

## 5. Remediation

* Use **parameterized queries / prepared statements**.
* Never build authentication queries using string concatenation.
* Implement proper server-side authentication and authorization.
* Use least-privileged database accounts.

## 6. Key Takeaway

**A SQL injection vulnerability in a login function can completely bypass authentication if user input is directly incorporated into the query.**

