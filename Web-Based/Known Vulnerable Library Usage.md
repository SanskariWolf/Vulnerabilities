# Description
Known Vulnerable Library Usage is a vulnerability that occurs when an application includes third-party libraries, frameworks, SDKs, or components that contain publicly disclosed security vulnerabilities.

These vulnerabilities are often documented through:
- Common Vulnerabilities and Exposures (CVEs)    
- Vendor security advisories
- Public vulnerability databases
- Security research disclosures

Applications frequently inherit security risks from external libraries, even if the application code itself is secure.

Common examples include:
- Outdated frontend libraries
- Vulnerable backend frameworks
- Legacy SDKs
- Deprecated cryptographic libraries
- Components with publicly available exploits

This issue is closely related to software supply chain security and component management.
# Steps to Reproduce
### 1. Identify Libraries in Use
Enumerate application dependencies from sources such as:
```text
package.json
requirements.txt
pom.xml
Cargo.toml
composer.lock
Gemfile.lock
```
Also inspect:
- JavaScript bundles
- Installed packages
- Container images
### 2. Determine Library Versions
Identify exact versions installed.
Examples:
```bash
npm list
```
```bash
pip freeze
```
```bash
cargo tree
```
### 3. Search for Known Vulnerabilities
Compare identified versions against vulnerability databases or scanners.
Examples of tools:
- OWASP Dependency-Check
- Snyk
- Trivy
- Dependabot
Example:
```bash
npm audit
```
### 4. Review Vulnerability Details
Validate:
- Affected versions
- Available patches
- CVE severity
- Exploit availability
### 5. Confirm Reachability
Verify whether vulnerable functionality is:
- Loaded
- Executed
- Exposed to users
### 6. Verify Exploitation
If:
- The vulnerable library version exists
- The vulnerable code path is accessible
-> vulnerability confirmed
# Impact
Known Vulnerable Library Usage can lead to:
- Remote Code Execution (RCE)
- Authentication bypass
- Data leakage
- Privilege escalation
- Supply chain compromise
- Denial of Service (DoS)
Impact depends on the vulnerable library and how it is used.
# Remediation
1. Maintain an up-to-date inventory of libraries
2. Upgrade vulnerable versions promptly
3. Remove unused libraries and dependencies
4. Continuously scan for vulnerable components
5. Subscribe to vendor security advisories
6. Automate dependency updates where appropriate
7. Pin and review dependency versions
8. Validate transitive dependencies regularly
# Severity
**Medium to Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```
**Score:** 9.8 (Critical)  