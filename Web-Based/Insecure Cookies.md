# Description
Insecure Cookies is a vulnerability that occurs when cookies used by an application are configured or handled in a way that exposes sensitive information or weakens session security.

Cookies commonly store or reference:
- Session identifiers
- Authentication state
- User preferences
- Access tokens
- Tracking information

Improperly secured cookies may allow attackers to intercept, manipulate, reuse, or abuse session-related data.

Common insecure cookie configurations include:
- Missing `Secure` attribute
- Missing `HttpOnly` attribute
- Missing `SameSite` attribute
- Storing sensitive information directly in cookies
- Predictable cookie values
- Excessively long cookie lifetime
- Weak session handling

Sensitive cookies affected may include:
- Session cookies
- Authentication cookies
- Persistent login cookies
- Token-bearing cookies
# Steps to Reproduce
### 1. Authenticate to the Application
Log in and establish a normal session.
### 2. Inspect HTTP Responses
Review cookie-related headers.
Example:
```http
Set-Cookie: sessionid=abc123
```
Inspect for missing security attributes.
### 3. Review Cookie Properties
Check whether cookies include:
```text
Secure
HttpOnly
SameSite
```
Example secure configuration:
```http
Set-Cookie: sessionid=abc123; Secure; HttpOnly; SameSite=Lax
```
### 4. Analyze Cookie Contents
Determine whether cookies contain:
- Plaintext credentials
- User identifiers
- Sensitive application data
- Authentication tokens
### 5. Validate Session Security
Check whether cookies:
- Persist longer than necessary
- Can be reused after logout
- Are transmitted over insecure transport
### 6. Verify Exploitation
If sensitive cookies:
- Lack security attributes
- Store sensitive data insecurely
- Are improperly managed
-> vulnerability confirmed
# Impact
Insecure Cookies can lead to:
- Session hijacking
- Authentication bypass
- Exposure of sensitive data
- Unauthorized account access
- Cross-site attack exposure
- Increased risk of credential compromise
Impact depends on cookie usage and application architecture.
# Remediation
1. Apply the `Secure` attribute to sensitive cookies
2. Apply the `HttpOnly` attribute
3. Configure `SameSite` appropriately (`Lax` or `Strict`)
4. Avoid storing sensitive information directly in cookies
5. Use short-lived session cookies
6. Rotate session identifiers periodically
7. Encrypt or sign sensitive cookie data where appropriate
8. Review cookie policies during security testing
# Severity
**Medium**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:L/I:L/A:N
```
**Score:** 5.4 (Medium)