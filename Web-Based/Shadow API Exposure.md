# Description
Shadow API Exposure is a vulnerability that occurs when API endpoints exist outside the organization’s official inventory, security controls, monitoring processes, or management lifecycle.

Shadow APIs are typically created during:
- Development and testing 
- Legacy migrations
- Rapid feature deployment
- Third-party integrations
- Forgotten or deprecated services

Because these APIs are unmanaged or unknown, they often lack:
- Authentication controls
- Authorization enforcement
- Logging and monitoring
- Patch management
- Security testing

Shadow APIs significantly increase attack surface because they may expose functionality and data not intended for public access.

Common causes include:
- Missing API inventory
- Deprecated endpoints remaining accessible
- Development or staging APIs exposed to production networks
- Poor change management
- Incomplete API gateway coverage
# Steps to Reproduce
### 1. Identify Known APIs
Review documented APIs and expected endpoints.
Examples:
```text
/api/
/v1/
/v2/
```
### 2. Enumerate Additional API Endpoints
Identify APIs not listed in official documentation.
Sources may include:
- Web application traffic
- JavaScript files
- Mobile applications
- Archived endpoints
- DNS and subdomain discovery
### 3. Compare Against Official Inventory
Determine whether discovered APIs:
- Exist in API documentation
- Are registered internally
- Have assigned ownership
### 4. Inspect API Security Controls
Review whether discovered APIs enforce:
- Authentication
- Authorization
- Rate limiting
- Logging
### 5. Test Endpoint Accessibility
Determine whether endpoints expose:
- Internal functionality
- Administrative actions
- Sensitive data
- Deprecated business logic
### 6. Review Version Management
Check for:
```text
/api/v0/
/api/test/
/api/internal/
/api/legacy/
```
### 7. Verify Exploitation
If APIs:
- Exist outside official management processes
- Are publicly reachable
- Lack expected security controls
-> vulnerability confirmed
# Impact
Shadow API Exposure can lead to:
- Unauthorized access
- Sensitive data exposure
- Authentication bypass
- Discovery of hidden functionality
- Increased attack surface
- Exploitation of unpatched endpoints
Since shadow APIs are often unmanaged, they may become entry points into production environments.
# Remediation
1. Maintain a centralized API inventory
2. Continuously discover and catalog APIs
3. Decommission unused or deprecated APIs
4. Route APIs through centralized gateways
5. Apply authentication and authorization consistently
6. Monitor and log API activity
7. Include APIs in vulnerability management processes
8. Implement API lifecycle governance
# Severity
**Medium to High**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:L
```
**Score:** 6.5 (Medium)