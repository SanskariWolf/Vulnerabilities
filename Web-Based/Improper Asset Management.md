# Description
Improper Asset Management is a security weakness that occurs when an organization lacks accurate visibility, ownership, inventory, classification, lifecycle control, or governance over applications, infrastructure, services, APIs, devices, repositories, and other technology assets.

Without effective asset management, systems may remain:
- Unknown or undocumented
- Unpatched or unsupported
- Misconfigured
- Publicly exposed
- Unmonitored
- Orphaned after deployment

Security teams cannot adequately protect assets they do not know exist.
Assets commonly affected include:
- Web applications
- APIs
- Cloud resources
- Databases
- Servers
- Container workloads
- Mobile applications
- Domains and subdomains
- Source code repositories

Common causes include:
- Missing asset inventory processes
- Shadow IT
- Poor ownership assignment
- Lack of decommission procedures
- Incomplete discovery processes
- Weak change management
# Steps to Reproduce
### 1. Inventory Available Assets
Enumerate known organizational assets:
- Applications
- APIs
- Domains
- Infrastructure
- Cloud environments
### 2. Discover Untracked Assets
Identify assets not present in official inventories.
Examples:
```text
Legacy application
Unused API
Forgotten subdomain
Development server
```
### 3. Compare Inventory Against Reality
Validate whether discovered assets:
- Exist in inventory records
- Have assigned owners    
- Are actively maintained
### 4. Review Lifecycle Status
Determine whether assets are:
- Supported
- Patched
- Monitored
- Retired properly    
### 5. Evaluate Exposure
Check whether unmanaged assets expose:
- Administrative interfaces
- Public services
- Sensitive data
- Development environments
### 6. Verify Exploitation
If assets:
- Exist outside management processes
- Lack ownership or maintenance
- Introduce unmanaged exposure
-> vulnerability confirmed
# Impact
Improper Asset Management can lead to:
- Exposure of forgotten systems
- Delayed vulnerability remediation
- Unauthorized access
- Data exposure
- Increased attack surface
- Security monitoring gaps
This weakness often enables exploitation of multiple downstream vulnerabilities.
# Remediation
1. Maintain a centralized asset inventory
2. Assign ownership to all assets
3. Implement asset discovery and classification processes
4. Track software and infrastructure lifecycle status
5. Remove unused or obsolete assets
6. Continuously monitor public exposure
7. Integrate asset inventory into change management
8. Conduct regular asset audits
# Severity
**Medium to High**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:L
```
**Score:** 6.5 (Medium)