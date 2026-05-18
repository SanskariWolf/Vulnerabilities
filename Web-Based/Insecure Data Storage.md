# Description
Insecure Data Storage is a vulnerability that occurs when sensitive information is stored without appropriate security controls such as encryption, access restrictions, integrity protection, lifecycle management, or secure storage practices.

Applications and systems frequently store data in:
- Databases
- Local files
- Browser storage
- Mobile application storage
- Cloud storage
- Logs and backups
- Configuration files

If stored insecurely, attackers who gain access to the storage location may retrieve, modify, or abuse sensitive information.

Sensitive data commonly affected includes:
- Credentials and secrets
- Authentication tokens
- Personal information
- Payment information
- Session identifiers
- Cryptographic keys
- Business and operational data

Common causes include:
- Plaintext storage
- Weak encryption practices
- Hardcoded secrets
- Excessive data retention
- Improper file permissions
- Insecure client-side storage
# Steps to Reproduce
### 1. Identify Data Storage Locations
Review where the application stores data.
Examples:
```text
Database
Filesystem
Local storage
Cloud storage
Backups
Logs
```
### 2. Locate Sensitive Information
Identify stored data such as:
- Passwords
- Tokens
- API keys
- User information
- Payment details
### 3. Review Storage Protection
Determine whether data is:
- Encrypted
- Access-controlled
- Signed or integrity protected
- Properly isolated
### 4. Inspect Client-Side Storage
Review:
- Browser local storage
- Session storage
- Mobile application storage
- Cached application data
### 5. Validate Data Accessibility
Determine whether unauthorized users can:
- Read stored data
- Modify stored data
- Export stored data
### 6. Verify Retention Behavior
Check whether sensitive data:
- Persists longer than required
- Remains after logout or deletion
### 7. Verify Exploitation
If sensitive information:
- Is stored insecurely
- Can be accessed or extracted without proper protection
-> vulnerability confirmed
# Impact
Insecure Data Storage can lead to:
- Exposure of sensitive information
- Credential compromise
- Unauthorized access
- Regulatory and privacy violations
- Session compromise
- Data tampering
Impact depends on data sensitivity and storage location.
# Remediation
1. Encrypt sensitive data at rest
2. Avoid storing unnecessary sensitive information
3. Use secure secret-management mechanisms
4. Restrict access using least privilege
5. Implement secure retention and deletion policies
6. Avoid storing secrets client-side where possible
7. Protect backups and exported data
8. Regularly audit stored sensitive information
# Severity
**Medium to Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:L/A:N
```
**Score:** 7.5 (High)