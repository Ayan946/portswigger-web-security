# Blind SQL injection with time delays and information retrieval

## 1. Vulnerability

**Blind SQL Injection — Time-Based**

The application does not reveal query results or errors, but the database processes queries synchronously. This allows an attacker to use conditional time delays as a side channel.

## 2. Objective

Use time-based blind SQL injection to determine the `administrator` password and log in.

## 3. Exploitation

1. Intercept the `TrackingId` cookie using Burp Suite.

2. Test a true condition that causes a 10-second delay:

`TrackingId=x'%3BSELECT+CASE+WHEN+(1=1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END--`

3. Change the condition to false:

`TrackingId=x'%3BSELECT+CASE+WHEN+(1=2)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END--`

The response is immediate, confirming that response time can be used as a boolean signal.

4. Confirm the `administrator` user exists using a conditional `pg_sleep()`.

5. Test password length using `LENGTH(password)>N`. The password is 20 characters long.

6. Use `SUBSTRING(password,N,1)` with Burp Intruder to test each character against `a-z` and `0-9`.

7. A response of approximately 10 seconds indicates the tested character is correct.

8. Repeat for each character position until the entire password is recovered.

9. Use the recovered password to log in as `administrator`.

10. Lab solved.

## 4. Impact

Time-based blind SQL injection can allow attackers to:

* Extract data when no useful response is returned.
* Recover credentials character by character.
* Infer database information through timing differences.
* Bypass authentication.

## 5. Remediation

* Use **parameterized queries / prepared statements**.
* Do not allow user input to influence SQL query structure.
* Apply least-privilege database permissions.
* Monitor unusual database query patterns and repeated delayed requests.

## 6. Key Takeaway

**Even when an application reveals no useful data or errors, database response time can become a side channel for extracting sensitive information.**
