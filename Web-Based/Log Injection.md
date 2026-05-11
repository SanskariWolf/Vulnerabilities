# Description
Log Injection (also known as Log Forging) is a vulnerability that occurs when an application records untrusted user input into logs without proper sanitization or encoding.

Attackers may inject specially crafted characters or content into log entries to manipulate how logs appear, hide malicious actions, create fake records, or interfere with monitoring and incident response.

Applications commonly log:
- Usernames
- HTTP headers
- Request parameters
- Error messages
- API requests
- Search queries

If user-controlled input is written directly to logs, attackers may alter log structure or inject misleading information.

Common causes include:
- Logging raw user input
- Missing character sanitization
- Unsafe log formatting
- Concatenating log messages directly
# Steps to Reproduce
### 1. Identify Logged Inputs
Locate inputs likely to be recorded:
- Login forms
- Search fields
- HTTP headers
- Contact forms
- API parameters
### 2. Submit Crafted Input
Send input containing control characters.
Examples:
```text
admin
[INFO] Login Successful
```
Or newline-based payloads:
```text
user%0a[ERROR] Authentication bypass
```
### 3. Trigger Logging Event
Perform actions that cause the application to generate logs.
Examples:
- Login attempts
- Failed requests
- Search operations
### 4. Review Generated Logs
Inspect whether:
- New log entries were injected
- Existing entries were altered
- Formatting was broken
Example:
```text
[INFO] User Login: attacker
[ERROR] Authentication bypass
```
### 5. Verify Monitoring Impact
Check whether:
- Alerting systems are bypassed
- Log parsing fails
- Events appear legitimate
### 6. Verify Exploitation
If attacker-controlled input:
- Creates fake log records
- Alters log structure
- Hides malicious actions
-> vulnerability confirmed
# Impact
Log Injection can lead to:
- Manipulation of audit trails
- Incident response disruption
- Security monitoring bypass
- Forensic confusion
- Concealment of malicious activity
- Corruption of log analysis systems
In severe cases, downstream systems processing logs may also become vulnerable.
# Remediation
1. Sanitize and encode user input before logging
2. Remove or escape newline and control characters
3. Use structured logging formats (JSON, key-value logs)
4. Avoid string concatenation in logging statements
5. Protect log integrity and access controls
6. Validate log processing pipelines
7. Monitor abnormal log patterns
# Severity
**Medium**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:N
```
**Score:** 6.5 (Medium)
