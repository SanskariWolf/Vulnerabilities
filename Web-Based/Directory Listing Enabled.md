# Description

Directory Listing Enabled is a vulnerability that occurs when a web server is configured to display the contents of directories instead of returning a default page or denying access.

When directory browsing is enabled, users may access and enumerate files and folders that were not intended to be publicly exposed.

Exposed content may include:
- Source code
- Configuration files
- Backup files
- Uploaded files
- Logs
- Internal documents
- Temporary files

This issue typically results from insecure web server configuration or missing index files.

Common causes include:
- Directory indexing enabled on the web server
- Missing `index.html` / `index.php`
- Misconfigured access controls
- Exposed upload or backup directories
# Steps to Reproduce
### 1. Identify Accessible Directories
Browse common directories such as:
```text
/
/uploads/
/images/
/backup/
/admin/
/logs/
/assets/
```
### 2. Observe Server Response
Access directories directly:
```http
GET /uploads/
```
Check whether the server:
- Displays file listings
- Allows directory navigation
- Reveals hidden resources
### 3. Enumerate Directory Contents
Review exposed information such as:
- File names
- Folder structure
- Timestamps
- File sizes
### 4. Attempt Access to Sensitive Files
Check whether exposed files are accessible.
Examples:
```text
backup.zip
config.php.bak
.env
database.sql
```
### 5. Use Automated Enumeration (Optional)
Examples:
```bash
dirsearch -u https://example.com
```
```bash
gobuster dir -u https://example.com -w wordlist.txt
```
### 6. Verify Exploitation
If the application:
- Displays directory contents
- Allows browsing of internal files
- Exposes sensitive resources
-> vulnerability confirmed
# Impact
Directory Listing Enabled can lead to:
- Information disclosure
- Exposure of source code or configuration files
- Discovery of hidden application functionality
- Credential leakage
- Enumeration for further attacks
- Increased attack surface
While often informational by itself, it may enable more severe vulnerabilities.
# Remediation
1. Disable directory listing on the web server
2. Configure default index pages:
    - `index.html`
    - `index.php`
3. Restrict access using proper authorization controls
4. Move sensitive files outside the web root
5. Remove backup and temporary files from public directories
6. Apply least privilege to file access
7. Regularly audit publicly accessible paths
# Severity
**Low to Medium** (can become High depending on exposed content)
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N
```
**Score:** 5.3 (Medium)
