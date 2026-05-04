# Description
Blind SQL Injection is a type of SQL Injection where the application does not return direct database errors or query results to the attacker. Instead, attackers infer information by observing application behavior such as response differences or time delays.

Unlike classic SQL Injection, data is not directly visible. Attackers rely on indirect methods to extract information from the database.

Blind SQL Injection is commonly divided into:
- [[Boolean-Based SQL Injection]]
- [[Time-Based SQL Injection]]
# Steps to Reproduce
### 1. Identify Input Points
Locate parameters interacting with the database:
- URL parameters (`id=1`)
- Login forms
- Search fields
- API requests
### 2. Test for Injection Possibility
Inject a basic payload:
```sql
'
```
Observe:
- No error → possible blind scenario
- Application still responds normally
### 3. Perform Boolean-Based Testing
```sql
' AND 1=1-- 
' AND 1=2-- 
```
Check:
- If responses differ → injection exists
### 4. Perform Time-Based Testing
```sql
' AND SLEEP(5)-- 
```
Check:
- Delayed response → injection confirmed
### 5. Confirm Vulnerability
If:
- No visible SQL errors
- But response behavior changes or delays occur
→ Blind SQL Injection is confirmed
### 6. Optional Automation
Use:
- sqlmap
```bash
sqlmap -u "http://example.com/page?id=1" --technique=B,T
```
## Impact
Blind SQL Injection can lead to:
- Extraction of sensitive data (slow but possible)
- Authentication bypass
- Enumeration of database structure
- Data exfiltration (character-by-character)
- Full database compromise over time
Even though exploitation is slower, the impact remains severe.
## Remediation
1. Use **Parameterized Queries (Prepared Statements)**
2. Validate and sanitize all user inputs
3. Use ORM frameworks
4. Implement proper error handling (avoid logic leaks)
5. Apply least privilege to database accounts
6. Use Web Application Firewalls (WAF)
7. Conduct regular security testing
## Severity

**High to Critical**
- No direct output, but still fully exploitable
- Allows complete database extraction with time
## CVSS (v3.1)
```id="cvb72x"
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```
**Score:** 9.8 (Critical)
