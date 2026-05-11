# Description
Lack of Audit Trail is a security weakness that occurs when an application or system fails to maintain reliable, traceable, and reviewable records of security-relevant activities.

An audit trail provides accountability by recording **who performed an action, what was changed, when it occurred, and where it originated from**.

Without sufficient auditing, organizations may be unable to:
- Detect unauthorized activity
- Investigate incidents
- Trace administrative actions
- Meet compliance requirements
- Establish accountability

Unlike [[Insufficient Logging]], which focuses on missing or incomplete event generation, Lack of Audit Trail focuses on the absence of **historical accountability and traceability** for critical actions.

Common causes include:
- Administrative actions not recorded
- Missing change history
- No user attribution
- Missing timestamp records
- Logs that cannot be correlated
- Audit records that can be modified or deleted
# Steps to Reproduce
### 1. Identify Sensitive Operations
Locate activities that should generate audit records:
- User creation or deletion
- Authentication events
- Role or permission changes
- Password resets 
- Administrative actions
- Data creation, modification, or deletion
- Configuration changes
### 2. Perform Controlled Actions
Execute test activities.
Examples:
```text
Create user
Delete record
Modify permissions
Reset password
```
### 3. Inspect Audit Records
Review:
- Audit logs
- Administrative dashboards
- SIEM records
- Change history panels
- Monitoring systems
Verify whether actions were recorded.
### 4. Validate Audit Contents
Determine whether records include:
- User identity
- Timestamp
- Action performed
- Target resource
- Source information    
- Success or failure result
### 5. Test Tamper Resistance
Verify whether:
- Audit records can be modified
- Entries can be deleted without tracking
- Historical records remain intact
### 6. Verify Exploitation
If critical activities:
- Are not recorded
- Cannot be attributed
- Leave no historical evidence
-> vulnerability confirmed
# Impact
Lack of Audit Trail can lead to:
- Loss of accountability
- Delayed incident response
- Difficulty performing forensic investigations
- Inability to detect insider threats
- Compliance violations
- Reduced visibility into malicious activity
This weakness increases operational and security risk even if no direct compromise occurs.
# Remediation
1. Implement audit logging for security-sensitive actions
2. Record user identity and timestamps
3. Protect audit logs against modification and deletion
4. Centralize audit storage
5. Retain audit history according to business requirements
6. Enable monitoring and alerting on critical events
7. Periodically review audit coverage and effectiveness
8. Ensure audit records are searchable and correlated
# Severity
**Low to Medium** (can become High in regulated or high-risk environments)
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N
```
**Score:** 5.3 (Medium)