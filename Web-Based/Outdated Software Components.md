# Description

Outdated Software Components is a vulnerability that occurs when an application, server, framework, operating system, plugin, container image, or supporting software runs unsupported, deprecated, or outdated versions that contain known security weaknesses.

Software vendors continuously release updates to:
- Fix security vulnerabilities
- Improve stability    
- Patch known exploits
- Add security controls

Failure to apply updates may expose the environment to publicly known attacks and exploitation techniques.

Affected components may include:
- Web server
- Application frameworks
- Operating systems
- Libraries and dependencies
- Container images
- Databases
- Runtime environments
- Plugins and extensions

Common causes include:
- Missing patch management processes
- Unsupported software versions
- Operational delays in upgrades
- Poor asset inventory management
# Steps to Reproduce
### 1. Identify Technology Stack
Enumerate software components used by the application or infrastructure.
Examples:
- Web server
- Framework
- Database
- Runtime
- Container platform
### 2. Determine Version Information
Identify running versions.
Examples:
```bash
nmap -sV example.com
```
```bash
curl -I https://example.com
```
Inspect:
- Response headers
- Application banners
- Package manifests
### 3. Enumerate Installed Components
Examples:
```bash
dpkg -l
```
```bash
rpm -qa
```
```bash
docker images
```
### 4. Compare Against Security Advisories
Review:
- Vendor advisories
- Public CVEs
- End-of-life (EOL) status
- Patch availability

Use tools such as:
- Trivy
- OWASP Dependency-Check
- Snyk
### 5. Validate Exposure
Confirm:
- Vulnerable functionality is reachable
- Software is actively used
- Public exploits exist (if applicable)
### 6. Verify Exploitation
If:
- Software version is outdated    
- Known vulnerabilities affect that version
-> vulnerability confirmed
# Impact
Outdated Software Components can lead to:
- Remote Code Execution (RCE)
- Authentication bypass
- Sensitive data exposure
- Privilege escalation
- Supply chain compromise
- Denial of Service (DoS)
Impact depends on the component’s role and associated vulnerabilities.
# Remediation
1. Establish a formal patch management process
2. Maintain an inventory of software assets
3. Upgrade unsupported and end-of-life software
4. Continuously monitor vendor advisories and CVEs
5. Remove unused software and plugins
6. Automate update and dependency management where possible
7. Regularly scan infrastructure and applications
8. Test updates in staging environments before production deployment
# Severity
**Medium to Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```
**Score:** 9.8 (Critical)  