# Description
Insufficient Logging is a vulnerability that occurs when an application, system, or infrastructure fails to generate, retain, monitor, or protect security-relevant logs required to detect, investigate, and respond to malicious or unauthorized activity.

Logging is essential for:
- Security monitoring
- Incident detection
- Threat hunting
- Forensics and investigation
- Compliance and auditing

When logging is missing or inadequate, security incidents may go unnoticed and attackers may operate without detection.

Common issues include:
- Missing authentication logs
- No failed login tracking
- Lack of audit trails
- Incomplete API activity records
- Missing administrative action logs
- Short log retention periods
- Sensitive events not being monitored
This issue aligns closely with logging and monitoring weaknesses described by OWASP.
# Steps to Reproduce
### 1. Identify Security-Relevant Actions
Locate actions that should generate logs:
- User authentication
- Password resets
- Privilege changes
- Administrative actions
- API requests
- File uploads
- Sensitive data access
### 2. Perform Test Actions
Execute controlled activities such as:
```text
Failed login attempt
Successful login
Role modification
Invalid API request
```
### 3. Inspect Logging Mechanisms
Review:
- Application logs
- Audit logs
- SIEM dashboards
- Monitoring platforms
- Event records
Check whether the activity was recorded.
### 4. Validate Log Quality
Determine whether logs contain:
- Timestamp
- User identity
- Source information
- Event type
- Result (success/failure)
### 5. Review Retention and Monitoring
Verify:
- Log retention policies
- Alerting mechanisms
- Real-time monitoring
- Centralized collection
### 6. Verify Exploitation
If security-relevant actions:
- Are not logged
- Cannot be monitored
- Leave insufficient forensic evidence
->  vulnerability confirmed
# Impact
Insufficient Logging can lead to:
- Delayed incident detection
- Reduced forensic visibility
- Difficulty identifying attackers
- Increased dwell time for malicious activity
- Compliance failures
- Inability to investigate security incidents
Although it may not directly enable compromise, it significantly increases organizational risk.
# Remediation
1. Log all security-sensitive actions
2. Centralize logging infrastructure    
3. Implement monitoring and alerting mechanisms
4. Retain logs according to business and compliance requirements
5. Protect logs from unauthorized modification
6. Include sufficient context in events
7. Monitor failed authentication and privileged activity
8. Periodically test detection and response capabilities
# Severity
**Low to Medium** (can become High in regulated or critical environments)
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N
```
**Score:** 5.3 (Medium)