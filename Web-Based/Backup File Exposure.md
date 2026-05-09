# Description
Backup File Exposure is a vulnerability that occurs when backup copies of application files, databases, configurations, or archives are unintentionally accessible to unauthorized users.

Backup files are commonly created during:
- Application updates
- Server migrations
- Manual maintenance
- Development and deployment processes

If these files are stored in publicly accessible locations, attackers may download and inspect them to obtain sensitive information.

Exposed backup files may contain:
- Source code
- Database dumps
- Credentials and secrets
- Configuration files
- API keys and tokens
- User information
- Internal documentation

Common causes include:
- Leaving backup files inside the web root
- Publicly accessible storage buckets
- Temporary deployment artifacts
- Directory listing enabled
- Weak access controls
# Steps to Reproduce
### 1. Identify Potential Backup Locations
Review accessible directories such as:
```text
/
/backup/
/backups/
/old/
/archive/
/tmp/
/public/
```
### 2. Enumerate Common Backup File Names
Attempt access to commonly exposed backup files:
```text
backup.zip
website.zip
site.tar.gz
database.sql
config.bak
index.php~
app_old.zip
```
### 3. Inspect Directory Listings (If Enabled)
Browse directories and identify:
- Archived files
- Temporary files
- Historical versions
### 4. Download Accessible Backup Files
Attempt to retrieve exposed files and inspect contents.
Examples:
```text
GET /backup.zip
GET /database.sql
```
### 5. Analyze Retrieved Data
Review whether the backup contains:
- Source code
- Credentials
- Secrets
- Internal endpoints
- Sensitive records
### 6. Verify Exploitation
If backup files:
- Are publicly accessible
- Contain sensitive information
-> vulnerability confirmed
# Impact
Backup File Exposure can lead to:
- Disclosure of source code
- Exposure of credentials and secrets
- Leakage of customer or business data
- Discovery of internal architecture
- Authentication bypass    
- Full application compromise
Backup files often provide attackers with complete visibility into the environment.
# Remediation
1. Remove backup files from publicly accessible directories
2. Store backups outside the web root
3. Restrict access using authentication and authorization
4. Encrypt sensitive backups at rest
5. Disable directory listing
6. Establish backup retention and cleanup processes
7. Audit deployments for temporary or archived files
8. Monitor for unintended file exposure
# Severity
**High to Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:L/A:N
```
**Score:** 7.5 (High)