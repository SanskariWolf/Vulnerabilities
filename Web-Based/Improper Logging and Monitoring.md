# Description
Improper Logging and Monitoring is a vulnerability that occurs when an application or infrastructure fails to adequately record, retain, analyze, monitor, or respond to security-relevant events.

Logging provides visibility into system activity, while monitoring enables detection and response to suspicious behavior. Weaknesses in either area may allow attackers to operate undetected for extended periods.

Security-relevant events that should typically be logged and monitored include:
- Authentication attempts
- Privilege changes
- Administrative actions
- API access
- Data exports
- File uploads
- Configuration changes
- Security control failures

Common issues include:
- Missing audit logs
- Insufficient event details
- Lack of centralized monitoring
- No alerting for suspicious activity
- Short retention periods
- Unprotected or mutable logs
- Failure to investigate alerts
This category aligns closely with monitoring and detection weaknesses identified by OWASP.
## Steps to Reproduce
### 1. Identify Security-Critical Operations
Locate activities that should generate logs and alerts:
- Login attempts
- Failed authentication
- Password resets
- Role changes
- Administrative access
- Sensitive data access
### 2. Perform Controlled Test Actions
Execute activities such as:
```text
Multiple failed logins
Privilege modification
Invalid API request
Unexpected file upload
```
### 3. Review Logging Behavior
Inspect:
- Application logs
- Audit logs
- Monitoring dashboards
- Alert systems
- SIEM platforms
Determine whether events are recorded.
### 4. Validate Monitoring Coverage
Check whether the system:
- Generates alerts
- Detects abnormal behavior
- Correlates related events
- Escalates security incidents
### 5. Review Retention and Integrity
Verify:
- Log retention policies
- Centralized collection
- Access controls for logs
- Tamper resistance
### 6. Verify Exploitation
If security-relevant activity:
- Is not logged
- Is not monitored
- Does not trigger alerts
-> vulnerability confirmed
# Impact
Improper Logging and Monitoring can lead to:
- Delayed attack detectio
- Longer attacker dwell time
- Reduced forensic capability
- Failure to identify breaches
- Compliance violations
- Increased incident response costs
This weakness usually amplifies the impact of other vulnerabilities.
# Remediation
1. Log all security-relevant events
2. Implement centralized logging and monitoring
3. Configure alerting for suspicious activity
4. Protect logs against unauthorized modification
5. Retain logs according to business and compliance requirements
6. Monitor authentication and administrative actions
7. Establish incident response workflows
8. Periodically validate monitoring effectiveness    
# Severity
**Medium**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N
```
**Score:** 5.3 (Medium)
