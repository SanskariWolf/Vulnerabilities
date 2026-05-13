# Description
Missing HttpOnly Flag is a vulnerability that occurs when cookies containing session identifiers or sensitive information are set without the `HttpOnly` attribute.

The `HttpOnly` flag instructs browsers to restrict client-side scripts from accessing cookie values through browser APIs.

Without this protection, cookies may become accessible to malicious scripts running in the browser, increasing the risk of session compromise.

Sensitive cookies commonly affected include:
- Session identifiers
- Authentication tokens
- Access tokens
- Refresh tokens
- User state information

Common causes include:
- Misconfigured session management
- Missing security headers
- Legacy application configurations
- Improper cookie generation
**Note:** Missing `HttpOnly` alone does not create script execution. It becomes significantly more dangerous when combined with vulnerabilities such as [[Cross-Site Scripting (XSS)]].
# Steps to Reproduce
### 1. Authenticate to the Application
Log in and establish a normal authenticated session.
### 2. Inspect Response Headers
Review HTTP responses.
Example:
```http
Set-Cookie: sessionid=abc123
```
Observe whether the cookie includes:
```text
HttpOnly
```
Example of secure configuration:
```http
Set-Cookie: sessionid=abc123; HttpOnly
```
### 3. Inspect Browser Storage
Open browser developer tools and review:
- Cookies
- Storage entries
- Session-related values
### 4. Verify JavaScript Accessibility
Attempt to determine whether session cookies are accessible to client-side scripts.
Example observation:
- Cookie visible through browser scripting mechanisms
### 5. Review Sensitive Cookie Usage
Identify whether cookies contain:
- Session IDs
- Authentication state
- Privileged tokens
### 6. Verify Exploitation
If sensitive cookies:
- Are accessible to client-side scripts
- Lack the `HttpOnly` attribute
-> vulnerability confirmed
# Impact
Missing HttpOnly Flag can lead to:
- Increased risk of session theft
- Exposure of authentication tokens
- Account compromise (when combined with client-side vulnerabilities)
- Session hijacking
- Unauthorized access
Impact depends on cookie sensitivity and the presence of additional vulnerabilities.
# Remediation
1. Set the `HttpOnly` attribute on all sensitive cookies
Example:
```http
Set-Cookie: sessionid=abc123; HttpOnly
```
2. Avoid storing sensitive data directly in cookies
3. Use secure server-side session management
4. Combine with `Secure` and `SameSite` cookie attributes
5. Rotate session identifiers after authentication
6. Review cookie security configurations regularly
# Severity
**Low to Medium** (can become High when chained with other issues)
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:L/I:L/A:N
```
**Score:** 4.8 (Medium)