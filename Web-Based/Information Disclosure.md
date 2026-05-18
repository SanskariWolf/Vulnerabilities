# Description
Information Disclosure is a vulnerability that occurs when an application, API, service, or system unintentionally exposes sensitive, internal, confidential, or unnecessary information to unauthorized users.

Information that appears harmless in isolation may significantly assist attackers in reconnaissance, exploitation, privilege escalation, or lateral movement.

Exposed information may include:
- User data
- Internal application details
- Server configuration
- Software versions
- Credentials and secrets
- Debug information
- Source code
- API responses
- Internal network information

Information disclosure does not always result in direct compromise, but it frequently enables more severe vulnerabilities.

Common causes include:
- Verbose error messages
- Directory listing enabled
- Source code exposure
- Backup file exposure
- Debug mode enabled
- Improper access controls
- Sensitive data returned in responses
- Publicly exposed metadata
# Steps to Reproduce
### 1. Identify Accessible Interfaces
Review application entry points such as:
- Web pages
- APIs
- Authentication flows
- Administrative interfaces
- Public files
### 2. Inspect Responses
Observe whether responses expose:
```text
Server details
Software versions
Stack traces
Internal IDs
Sensitive metadata
```
### 3. Trigger Edge Cases
Test scenarios such as:
- Invalid input
- Unauthorized access attempts
- Missing parameters
- Unexpected requests
Observe whether additional information is revealed.
### 4. Enumerate Public Resources
Review:
- Public directories
- API endpoints
- Static files
- Debug pages
### 5. Inspect Client-Side Artifacts
Check:
- HTML comments
- JavaScript bundles
- API responses
- Browser storage
### 6. Verify Exposure
Determine whether disclosed information:
- Was not intended for public access
- Assists understanding of internal architecture
- Increases attack capability
### 7. Verify Exploitation
If sensitive or unnecessary information
- Is exposed to unauthorized users
- Reveals internal implementation details
-> vulnerability confirmed
# Impact
Information Disclosure can lead to:
- Exposure of sensitive information
- Easier exploitation of vulnerabilities
- Credential discovery
- User privacy impact
- Increased attack surface
- Facilitation of privilege escalation
While often informational, disclosure frequently amplifies the impact of other vulnerabilities.
# Remediation
1. Minimize data returned to users
2. Disable debug information in production
3. Restrict access to internal resources
4. Sanitize application responses
5. Protect sensitive files and metadata
6. Apply least privilege principles
7. Review API responses and error handling
8. Perform regular exposure assessments
# Severity
**Low to High** (depends on exposed information)
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N
```
**Score:** 5.3 (Medium)