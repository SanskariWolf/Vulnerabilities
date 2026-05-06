# Description
Insecure Third-Party Integration is a vulnerability that occurs when an application integrates external services, APIs, libraries, plugins, or platforms without implementing proper security controls.
Modern applications commonly rely on third-party services for:
- Authentication
- Payment processing
- Analytics
- Cloud storage
- Communication services
- CI/CD pipelines
If these integrations are insecure, attackers may exploit trust relationships between systems to gain unauthorized access, steal sensitive data, or compromise application functionality.

Common causes include:
- Excessive trust in third-party responses
- Weak API authentication
- Insecure webhook handling
- Vulnerable third-party libraries
- Overly permissive OAuth scopes
- Lack of input validation for external data
# Steps to Reproduce
### 1. Identify Third-Party Integrations
Enumerate:
- External APIs
- OAuth providers
- Payment gateways
- Analytics services
- Webhooks
- Embedded scripts/plugins
### 2. Inspect Requests and Responses
Use:
- Browser Developer Tools
- Burp Suite

Check for:
- API keys
- Tokens
- Sensitive headers
- Trust assumptions
### 3. Test Authentication and Authorization
Verify whether:
- API requests require proper authentication
- Tokens are validated securely    
- Scopes are restricted properly
### 4. Modify Third-Party Responses
Attempt to tamper with:
- API responses
- Webhook payloads
- Callback parameters
Observe whether the application trusts manipulated data.
### 5. Check Dependency Security
Identify outdated or vulnerable libraries using:
- Dependency scanners
- Software Composition Analysis (SCA) tools
### 6. Test Integration Failure Handling
Check how the application behaves when:
- Third-party services fail
- Invalid responses are received
- TLS validation errors occur
### 7. Verify Exploitation
If the application:
- Trusts manipulated third-party data
- Uses insecure libraries
- Exposes sensitive credentials
- Fails to validate integration responses
-> vulnerability confirmed
# Impact
Insecure Third-Party Integration can lead to:
- Account takeover
- Unauthorized access
- Data leakage
- Supply chain compromise
- Remote Code Execution (through vulnerable dependencies)
- Business logic abuse
The impact depends on the level of trust granted to the third-party service.
# Remediation
1. Validate and sanitize all third-party data
2. Use strong authentication and authorization mechanisms
3. Restrict OAuth/API scopes to minimum required permissions
4. Regularly update third-party libraries and dependencies
5. Monitor third-party services for security advisories
6. Implement secure webhook and callback validation
7. Avoid storing sensitive API keys in client-side code
8. Conduct regular security assessments of integrations
# Severity
**Medium to Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H
```
**Score:** 10.0 (Critical)