# Description
Boolean-Based SQL Injection is a type of Blind SQL Injection where attackers infer information from the database by sending queries that evaluate to TRUE or FALSE and observing differences in the application's response.

Unlike Error-Based SQL Injection, no database errors or direct outputs are shown. Instead, attackers rely on changes such as:
- Different page content
- HTTP status codes
- Response length
- Redirect behavior

This technique is a subtype of [[Blind SQL Injection]] and is often used when:
- Errors are suppressed
- No timing delays are usable
- The application still behaves differently for true/false conditions
## Steps to Reproduce
### 1. Identify Input Points
Locate parameters interacting with the database:
- URL parameters (`id=1`)
- Login forms
- Search inputs
- API endpoints
### 2. Establish Normal Behavior
Send a normal request:
```http
http://example.com/page?id=1
```
Observe:
- Page content
- Response size
- Status code
### 3. Inject Boolean TRUE Condition
```sql
' AND 1=1-- 
```
If the page behaves normally → condition is TRUE
### 4. Inject Boolean FALSE Condition
```sql
' AND 1=2-- 
```
If the page behavior changes → condition is FALSE
### 5. Compare Responses
Look for differences in:
- Content (missing data, blank page)
- Length of response
- Status code changes
If a clear difference exists → vulnerability confirmed
### 6. Extract Data (Inference-Based)
Attackers can retrieve data character-by-character:
```sql
' AND SUBSTRING(database(),1,1)='a'-- 
```
- TRUE → normal response
- FALSE → different response
### 7. Optional Automation
Use:
- sqlmap
```bash
sqlmap -u "http://example.com/page?id=1" --technique=B
```
## Impact
Boolean-Based SQL Injection can lead to:
- Extraction of sensitive database information
- Authentication bypass
- Enumeration of database structure
- Data exfiltration without visible output
- Full database compromise over time
## Remediation
1. Use **Parameterized Queries (Prepared Statements)**
2. Validate and sanitize all user inputs
3. Use ORM frameworks
4. Avoid dynamic SQL query construction
5. Implement consistent response behavior (reduce inference leaks)
6. Apply least privilege to database accounts
7. Use Web Application Firewalls (WAF)
## Severity
**High to Critical**
- Works without visible errors
- Allows complete data extraction
- Hard to detect compared to classic SQLi
## CVSS (v3.1)
```id="bb6"
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```
**Score:** 9.8 (Critical)
