# Description
Missing SameSite Attribute is a vulnerability that occurs when cookies are issued without the `SameSite` attribute, allowing browsers to send those cookies during cross-site requests.

The `SameSite` attribute controls whether cookies are included in requests originating from another website.

Available values:
- `Strict` → Cookies are sent only for same-site requests
- `Lax` → Cookies are sent for limited cross-site navigation scenarios
- `None` → Cookies are sent in cross-site requests (requires `Secure`)

If sensitive cookies are missing this protection, attackers may exploit browser behavior to trigger authenticated requests on behalf of users.

Sensitive cookies commonly affected include:
- Session identifiers
- Authentication cookies
- CSRF-related tokens
- Persistent login cookies

Common causes include:
- Legacy session configurations
- Missing secure cookie policies
- Framework defaults not explicitly configured
- Incomplete session hardening

**Note:** Missing `SameSite` does not directly create a vulnerability but increases exposure to attacks such as [[Cross-Site Request Forgery (CSRF)]].
## Steps to Reproduce
### 1. Authenticate to the Application
Log in and establish an authenticated session.
### 2. Inspect Cookie Response Headers
Review HTTP responses.
Example:
```http
Set-Cookie: sessionid=abc123
```
Check whether the response includes:
```text
SameSite=
```
Secure examples:
```http
Set-Cookie: sessionid=abc123; SameSite=Lax
```
or
```http
Set-Cookie: sessionid=abc123; SameSite=Strict
```
### 3. Identify Sensitive Cookies
Determine whether affected cookies contain:
- Session identifiers
- Authentication state
- Persistent login data
### 4. Verify Cross-Site Cookie Behavior
Observe whether cookies are included during:
- Cross-origin navigation
- Third-party requests
- Embedded content requests
### 5. Evaluate Request Protection
Determine whether additional protections exist:
- CSRF tokens
- Origin validation    
- Referer validation
### 6. Verify Exploitation
If sensitive cookies:
- Lack the `SameSite` attribute
- Are transmitted in cross-site contexts
-> vulnerability confirmed
# Impact
Missing SameSite Attribute can lead to:
- Increased exposure to Cross-Site Request Forgery (CSRF)
- Unauthorized state-changing actions
- Session misuse
- Account modification without user intent
Impact depends on available protections and cookie sensitivity.
# Remediation
1. Configure `SameSite` for sensitive cookies
Recommended:
```http
Set-Cookie: sessionid=abc123; SameSite=Lax
```
For stronger protection:
```http
Set-Cookie: sessionid=abc123; SameSite=Strict
```
2. Use `SameSite=None; Secure` only when cross-site access is required
3. Implement CSRF protection mechanisms
4. Validate request origin and referer headers
5. Regularly review session and cookie configurations
6. Combine with `Secure` and `HttpOnly` attributes
# Severity
**Low to Medium** (can become High when combined with CSRF exposure)
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:L/I:L/A:N
```
**Score:** 4.8 (Medium)