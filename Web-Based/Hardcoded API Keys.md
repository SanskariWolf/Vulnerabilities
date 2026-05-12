# Description
Hardcoded API Keys is a vulnerability that occurs when API credentials are embedded directly into application source code, configuration files, scripts, binaries, mobile applications, or frontend assets instead of being securely managed at runtime.

API keys are intended to authenticate communication between systems and services. Embedding them directly into application artifacts increases the risk of unauthorized disclosure and misuse.

Hardcoded API keys may appear in:
- Source code repositories
- Mobile applications
- Frontend JavaScript files
- Configuration files
- Build artifacts
- Container images
- CI/CD pipelines

If exposed, attackers may use these credentials to access protected services, consume resources, retrieve sensitive information, or perform unauthorized actions.

Common causes include:
- Convenience during development
- Lack of secret-management practices
- Secrets committed to version control
- Improper deployment configuration
- Reusing credentials across environments
# Steps to Reproduce
### 1. Identify Application Artifacts
Review locations where secrets may be embedded:
```text
Source code
Configuration files
Mobile APK/IPA
Frontend bundles
Docker images
```
### 2. Search for Hardcoded Secrets
Inspect files for credential patterns.
Examples:
```text
api_key=
apikey=
secret=
token=
Authorization=
```
Examples of locations:
```text
.env
config.js
application.yml
settings.json
```
### 3. Inspect Client-Side Assets
Review:
- JavaScript files
- Mobile binaries
- Public repositories
- Build outputs
Look for embedded keys.
### 4. Validate Key Exposure
Determine whether discovered keys:
- Are active
- Can authenticate requests
- Have excessive permissions
### 5. Review Scope and Privileges
Check whether the key grants:
- Read access
- Write access
- Administrative capabilities
- Production environment access
### 6. Verify Exploitation
If API keys:
- Are embedded in application artifacts
- Can be extracted and reused
-> vulnerability confirmed
# Impact
Hardcoded API Keys can lead to:
- Unauthorized API access
- Data leakage
- Abuse of paid services
- Privilege escalation
- Infrastructure compromise
- Supply chain exposure
Impact depends on key privileges and environment.
# Remediation
1. Remove secrets from source code and binaries
2. Store credentials in secure secret-management systems
3. Use environment variables or runtime injection
4. Rotate exposed keys immediately
5. Apply least privilege to API permissions
6. Prevent secrets from entering version control
7. Scan repositories and build artifacts for embedded credentials
8. Separate credentials across environments (dev/test/prod)
# Severity
**High to Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:L
```
**Score:** 9.1 (Critical)
