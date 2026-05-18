# Description
Hardcoded Credentials is a vulnerability that occurs when authentication secrets are embedded directly into application code, configuration files, scripts, binaries, infrastructure definitions, or deployment artifacts instead of being securely managed at runtime.

Hardcoded credentials may include:
- Usernames and passwords
- API keys
- Database credentials
- Access tokens
- Encryption secrets
- Service account credentials
- SSH keys

Embedding credentials directly into application artifacts increases the risk of unauthorized access if those artifacts become exposed.

Common exposure locations include:
- Source code repositories
- Configuration files
- Mobile applications
- Container images
- Build pipelines
- Deployment scripts
- Frontend applications

Common causes include:
- Developer convenience
- Missing secret-management processes
- Test credentials left in production
- Credentials committed to version control
- Reuse of static credentials
## Steps to Reproduce
### 1. Identify Potential Secret Locations
Review locations where credentials may be stored:
```text
Source code
Configuration files
Containers
Build artifacts
Deployment scripts
```
### 2. Search for Embedded Credentials
Inspect application files for patterns such as:
```text
password=
username=
secret=
token=
apikey=
```
Examples of files:
```text
.env
config.yaml
application.properties
docker-compose.yml
```
### 3. Inspect Client-Side Artifacts
Review:
- JavaScript bundles
- Mobile application packages
- Public repositories
- Distributed binaries
### 4. Validate Credential Exposure
Determine whether discovered credentials:
- Are active
- Authenticate successfully
- Provide excessive permissions
### 5. Review Scope and Privileges
Check whether credentials grant:
- Administrative access
- Database access
- Production environment access
- Cross-service access
### 6. Verify Exploitation
If credentials:
- Are embedded within accessible artifacts
- Can be extracted and used
-> vulnerability confirmed
# Impact
Hardcoded Credentials can lead to:
- Unauthorized access
- Account compromise
- Data exposure
- Infrastructure compromise
- Privilege escalation
- Lateral movement across systems
Impact depends on credential sensitivity and privilege level.
# Remediation
1. Remove credentials from source code and artifacts
2. Use secure secret-management solutions
3. Store credentials in environment variables or runtime injection systems
4. Rotate exposed credentials immediately
5. Apply least privilege to service accounts
6. Prevent secrets from entering version control
7. Continuously scan repositories and artifacts for secrets
8. Separate credentials across environments
# Severity
**High to Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:L
```
**Score:** 9.1 (Critical)
