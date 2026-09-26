# SQL Injection Filter Bypass via XML Encoding

## Vulnerability

**SQL Injection via XML-encoded input**

The application filters SQL injection characters and keywords in the `storeId` parameter. However, the input is later XML-decoded before being processed by the backend, allowing the filter to be bypassed using **HTML/XML hex entities**.

## Objective

Bypass the SQL injection filter and retrieve the administrator's password from the database.

## Exploitation

1. Send the **Check stock** request to **Burp Repeater** and identify the `storeId` XML tag.

2. Use the following SQL injection query to retrieve the administrator's password:

```sql
UNION SELECT password FROM users WHERE username='administrator'
```

3. Encode the SQL query using **hexadecimal XML entities** with an encoding tool such as CyberChef.

4. Replace the value inside the `<storeId>` tag with the encoded payload:

```xml
<storeId>[XML-encoded SQL payload]</storeId>
```

5. Send the modified request. The application decodes the XML entities before processing the query, allowing the SQL injection to reach the database while bypassing the input filter.

6. The response reveals the **administrator's password**, completing the lab.

## Impact

Improper input filtering combined with XML entity decoding can allow attackers to bypass SQL injection protections and extract sensitive database information.

## Remediation

* Use **parameterized queries / prepared statements** instead of filtering SQL keywords.
* Decode and normalize input **before security validation**.
* Apply validation consistently after all relevant encoding/decoding transformations.
* Use least-privileged database accounts.

## Key Takeaway

**Encoding is not a security control.** Input filters can often be bypassed when an application validates encoded data before decoding it. Always normalize input before validation and, most importantly, use parameterized queries to prevent SQL injection.
