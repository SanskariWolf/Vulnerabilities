# Description
API Key Exposure is a vulnerability that occurs when application programming interface (API) keys are unintentionally exposed to unauthorized users through source code, client-side applications, logs, repositories, configuration files, backups, or network traffic.

API keys are commonly used to authenticate and authorize communication between applications and external services.

Exposed API keys may allow attackers to:
- Access protected APIs
- Consume paid resources
- Enumerate internal functionality
- Access sensitive data
- Perform unauthorized operations    

Common exposure locations include:
- Frontend JavaScript files
- Mobile applications
- Public repositories
- Environment files (`.env`)
- Configuration files
- Error messages
- Logs and backups

Common causes include:
- Hardcoded secrets
- Improper secret management
- Missing key rotation policies
- Excessive API permissions
- Debug information exposure
# Steps to Reproduce
### 1. Identify Potential Exposure Locations
Review:
- Client-side source code
- JavaScript bundles
- Mobile application packages
- Configuration files
- Logs
- Backup archives
Examples:
```text
.env
config.json
settings.js
```
### 2. Inspect Network Requests
Observe application traffic using:
- Browser Developer Tools
- Burp Suite
Check whether API keys are transmitted or exposed.
### 3. Search for Embedded Secrets
Review accessible files and responses for patterns such as:
```text
api_key=
apikey=
Authorization:
Bearer
```
### 4. Validate Key Exposure
Determine whether the discovered key:
- Is active
- Grants access to protected functionality
- Has excessive permissions
### 5. Review Access Scope
Inspect whether the exposed key permits:
- Read operations
- Write operations
- Administrative access
- Billing-related actions
### 6. Verify Exploitation
If an API key:
- Is accessible to unauthorized users
- Allows interaction with protected services
-> vulnerability confirmed
# Impact
API Key Exposure can lead to:
- Unauthorized API access
- Data exposure
- Abuse of third-party services
- Financial loss from resource consumption
- Privilege escalation
- Account or infrastructure compromise
Impact depends on the exposed key’s permissions and environment.
# Remediation
1. Store API keys in secure secret-management systems
2. Remove secrets from source code and client-side applications
3. Rotate exposed keys immediately
4. Apply least privilege to API permissions
5. Use environment variables for secret storage
6. Monitor usage anomalies and unauthorized requests
7. Restrict keys by origin, IP, or service where possible
8. Regularly scan repositories and deployments for secrets
# Severity
**Medium to Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:L
```
**Score:** 9.1 (Critical)
