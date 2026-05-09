# Description
Default Credentials Usage is a vulnerability that occurs when an application, service, device, or administrative interface continues to use vendor-provided or commonly known default usernames and passwords.

Default credentials are often intended only for initial setup and deployment. If they remain unchanged, attackers may gain unauthorized access using publicly known credential combinations.

Affected systems may include:
- Administrative dashboards
- Web applications
- Network appliances
- Databases
- Cloud services
- Development and testing environments
- IoT and embedded devices

Common examples include:
- `admin/admin`
- `admin/password`
- `root/root`
- Vendor default accounts

Common causes include:
- Failure to rotate initial credentials
- Weak deployment procedures
- Incomplete hardening processes
- Forgotten administrative accounts
# Steps to Reproduce
### 1. Identify Authentication Interfaces
Locate login points such as:
- Administrative panels
- Web application login pages
- API authentication endpoints
- Database consoles
- Device management portals
### 2. Enumerate Default Accounts
Review:
- Vendor documentation
- Installation guides
- Standard account naming conventions
Examples:
```text
admin
administrator
root
test
guest
```
### 3. Attempt Authentication Using Default Credentials
Test commonly known default combinations.
Example:
```text
Username: admin
Password: admin
```
Observe whether access is granted.
### 4. Verify Privilege Level
After authentication, determine:
- User permissions
- Administrative capabilities
- Accessible resources
### 5. Confirm Account Persistence
Check whether:
- Password reset is enforced
- Initial credentials remain active
- Multiple default accounts exist
### 6. Verify Exploitation
If authentication succeeds using vendor-provided or known default credentials:
-> vulnerability confirmed
# Impact
Default Credentials Usage can lead to:
- Unauthorized access
- Administrative account compromise
- Data exposure
- Configuration manipulation
- Privilege escalation
- Full system compromise
Attackers frequently target default credentials during automated scanning and opportunistic attacks.
# Remediation
1. Change all default credentials during deployment
2. Disable unused default accounts
3. Enforce password rotation policies
4. Require strong password complexity rules
5. Implement account lockout and rate limiting
6. Use unique credentials per environment
7. Enable Multi-Factor Authentication (MFA) for administrative access
8. Perform regular credential audits
# Severity
**High to Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```
**Score:** 9.8 (Critical)