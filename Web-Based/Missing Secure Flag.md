# Description
Missing Secure Flag is a vulnerability that occurs when cookies containing sensitive information are configured without the `Secure` attribute.

The `Secure` flag instructs browsers to send cookies **only over encrypted HTTPS connections**.

Without this protection, cookies may be transmitted over unencrypted HTTP requests, increasing the risk of interception and session compromise.

Sensitive cookies commonly affected include:
- Session identifiers
- Authentication cookies
- Access tokens
- Refresh tokens
- Persistent login cookies

If attackers can observe network traffic, exposed cookies may enable unauthorized access.

Common causes include:
- Incorrect cookie configuration
- Applications supporting both HTTP and HTTPS
- Legacy deployments
- Misconfigured reverse proxies or load balancers
# Steps to Reproduce
### 1. Authenticate to the Application
Log in and establish an authenticated session.
### 2. Inspect HTTP Response Headers
Review cookie responses.
Example:
```http
Set-Cookie: sessionid=abc123
```
Verify whether:
```text
Secure
```
is present.
Secure example:
```http
Set-Cookie: sessionid=abc123; Secure
```
### 3. Identify Sensitive Cookies
Determine whether affected cookies contain:
- Session identifiers
- Authentication state
- Persistent login data
### 4. Review Transport Behavior
Observe whether cookies are transmitted during:
- HTTP requests
- Redirect flows
- Mixed-content scenarios
### 5. Validate Session Protection
Check whether:
- HTTP access remains available
- HTTPS enforcement exists
- Sensitive cookies remain restricted
### 6. Verify Exploitation
If sensitive cookies:
- Are missing the `Secure` attribute
- Can be transmitted over HTTP
-> vulnerability confirmed
# Impact
Missing Secure Flag can lead to:
- Session hijacking
- Exposure of authentication tokens
- Unauthorized access
- Increased risk of network interception
- Compromise of authenticated sessions
Impact depends on network exposure and cookie sensitivity.
# Remediation
1. Configure sensitive cookies with the `Secure` attribute
Example:
```http
Set-Cookie: sessionid=abc123; Secure
```
2. Enforce HTTPS across the application
3. Redirect HTTP traffic to HTTPS
4. Combine with `HttpOnly` and `SameSite` attributes
5. Disable insecure transport paths
6. Regularly review session security settings
# Severity
**Medium** (can become High in exposed environments)
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:L/I:L/A:N
```
**Score:** 5.4 (Medium)