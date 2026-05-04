# Description

SQL Injection (SQLi) is a web security vulnerability that occurs when user input is improperly validated and directly included in SQL queries. This allows attackers to manipulate database queries and interact with the backend database in unintended ways.

SQL Injection is one of the most critical vulnerabilities listed in the OWASP Top 10 by the OWASP.
# Steps

When an application dynamically constructs SQL queries using user input without proper sanitization, attackers can inject malicious SQL code.
### Example (Vulnerable Query)
```sql
SELECT * FROM users WHERE username = '$username' AND password = '$password';
```
### Malicious Input
```sql
' OR '1'='1
```

### Resulting Query
```sql
SELECT * FROM users WHERE username = '' OR '1'='1' AND password = '';
```

This condition always evaluates to TRUE → authentication bypass.

# Types of SQL Injection

SQL Injection can be broadly categorized into:
### 1. In-Band SQL Injection
- [[Error-Based SQL Injection]]
- [[Union-Based SQL Injection]]
### 2. Blind SQL Injection
- [[Boolean-Based SQL Injection]]
- [[Time-Based SQL Injection]]

# Common Attack Points
- Login forms
- Search fields
- URL parameters (`id=1`)
- API requests
- Cookies & headers
## Impact
SQL Injection can lead to:
- Authentication bypass
- Exposure of sensitive data (credentials, financial records)
- Database manipulation (INSERT, UPDATE, DELETE)
- Privilege escalation
- Remote Code Execution (in certain configurations)
- Full system compromise
## Detection Techniques (High-Level)
- Injecting special characters (`'`, `"`)
- Observing error messages
- Comparing application responses
- Using automated tools

Tool example:
- sqlmap
## Remediation
1. Use **Parameterized Queries (Prepared Statements)**
2. Use **ORM frameworks**
3. Validate and sanitize all inputs
4. Apply **least privilege principle** to database users
5. Disable detailed database error messages
6. Use Web Application Firewalls (WAF)
7. Perform regular security testing

## Severity

**Critical**

# CVSS (v3.1)
```
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```
**Score:** 9.8 (Critical)

## References / Related Notes

- [[Blind SQL Injection]]
- [[Boolean-Based SQL Injection]]
- [[Time-Based SQL Injection]]
- [[Error-Based SQL Injection]]
- [[Union-Based SQL Injection]]
