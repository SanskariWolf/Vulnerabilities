# Description

Source Code Disclosure is a vulnerability that occurs when an application unintentionally exposes its source code to unauthorized users.

Source code may become accessible through misconfigurations, deployment mistakes, backup exposures, improper access controls, or server processing failures.

Exposed source code can reveal sensitive information such as:
- Hardcoded credentials
- API keys and tokens
- Database connection strings
- Internal endpoints
- Business logic
- Security controls
- Hidden functionality

This vulnerability significantly increases the likelihood of discovering and exploiting additional weaknesses.

Common causes include:
- Exposed repository files
- Misconfigured web servers
- Public backup files
- Directory listing enabled
- Improper file permissions
- Debug or development artifacts left in production
# Steps to Reproduce
### 1. Identify Potential Exposure Points
Check for locations such as:
```text
/
/backup/
/src/
/config/
/git/
/old/
/debug/
```
### 2. Attempt Direct Access to Files
Look for common source or backup files:
```text
index.php
config.php
app.js
.env
.git/config
backup.zip
source.tar.gz
```
Observe whether source code is returned instead of processed output.
### 3. Inspect Application Responses
Check:
- HTML comments
- JavaScript bundles
- API responses
- Static asset references

Look for:
- Internal paths
- Sensitive comments
- Embedded secrets
### 4. Enumerate Repository Exposure
Attempt to access exposed version control artifacts:
```text
.git/
.svn/
.hg/
```
### 5. Review Downloadable Files
Inspect publicly available archives:
```text
site_backup.zip
database.sql
project.tar.gz
```
### 6. Verify Exploitation
If the application:
- Exposes source files
- Reveals internal application logic
- Leaks credentials or configuration
-> vulnerability confirmed
# Impact
Source Code Disclosure can lead to:
- Exposure of secrets and credentials
- Discovery of hidden endpoints
- Authentication bypass
- Easier exploitation of application vulnerabilities
- Privilege escalation
- Full application compromise
Source code exposure frequently acts as a force multiplier for other attacks.
# Remediation
1. Remove source and backup files from public directories
2. Disable access to development artifacts
3. Configure servers to process source files instead of serving them directly
4. Restrict access to repository metadata
5. Store secrets outside source code
6. Implement proper file permissions
7. Disable directory listing
8. Perform regular deployment and exposure audits
# Severity
**High to Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:L/A:N
```
**Score:** 7.5 (High)
