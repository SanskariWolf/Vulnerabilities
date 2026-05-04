# Description

Insecure File Permissions is a vulnerability that occurs when files or directories on a system are assigned overly permissive access rights. This allows unauthorized users to read, modify, or execute sensitive files.

Improper permission settings can expose critical system components such as:
- Configuration files
- Application source code
- Credentials and secrets
- System binaries
This vulnerability often arises due to misconfiguration of file systems, web servers, or deployment processes.
# Steps
### 1. Identify Accessible Files/Directories
Locate sensitive files or directories such as:
- `/etc/passwd`
- `/etc/shadow`
- `.env` files
- Backup files (`.bak`, `.old`)
- Application config files
### 2. Check File Permissions (Linux)
Use:
```bash
ls -la
```
Example output:
```bash
-rwxrwxrwx 1 user user 1234 config.php
```
### 3. Analyze Permissions
- `777` → Read, write, execute for everyone (highly insecure)
- `666` → Read/write for everyone
- World-writable files → potential privilege escalation
### 4. Attempt Unauthorized Access
Try:
- Reading sensitive files
- Modifying application files
- Uploading or replacing scripts
### 5. Verify Exploitation
Examples:
- Modify a config file to inject malicious code
- Replace a script with a backdoor
- Access sensitive credentials
If successful → vulnerability confirmed
# Impact
Insecure File Permissions can lead to:
- Unauthorized access to sensitive data
- Modification of application logic
- Privilege escalation
- Remote Code Execution (in some cases)
- Full system compromise
# Remediation
1. Apply **Principle of Least Privilege**
2. Set secure permissions:
    - Files → `644`
    - Directories → `755`
3. Restrict access to sensitive files:
    - `/etc/shadow` → `600`
4. Avoid world-writable permissions (`777`)
5. Use proper user/group ownership
6. Regularly audit file permissions
7. Implement access control mechanisms
# Severity
**Medium to High** (can be Critical in certain cases)
- Medium → Read-only exposure
- High → Writable files or config access
- Critical → Leads to privilege escalation or RCE
# CVSS (v3.1)
High Severity Scenario
```text
CVSS:3.1/AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H
```
**Score:** ~7.8 (High)

 Critical Scenario (Privilege Escalation / RCE)
```text
CVSS:3.1/AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H
```
**Score:** ~7.8 (High → context-dependent Critical impact)