# Description
Token Leakage is a vulnerability that occurs when authentication, authorization, session, or access tokens are exposed to unauthorized parties through insecure storage, transmission, logging, URLs, client-side code, or application responses.

Tokens are commonly used to represent authenticated identity and access permissions. If exposed, attackers may reuse them to impersonate legitimate users or gain unauthorized access.

Commonly exposed token types include:
- Session tokens
- Access tokens
- Refresh tokens
- API bearer tokens
- OAuth authorization tokens
- JWTs

Common leakage sources include:
- URL query parameters
- Browser storage
- Client-side JavaScript
- Source code exposure
- Logs and monitoring systems
- Error messages
- Browser history
- Referer headers

Common causes include:
- Storing tokens insecurely
- Returning tokens in URLs
- Logging authentication information
- Improper secret handling
- Weak session management
# Steps to Reproduce

### 1. Authenticate to the Application
Log in using a valid account and establish an authenticated session.
### 2. Inspect Authentication Mechanisms
Review whether tokens appear in:
- Response bodies
- Cookies
- URLs
- Local storage
- Session storage
- Headers
Examples:
```http
Authorization: Bearer eyJ...
```
or
```text
https://example.com/callback?token=abc123
```
### 3. Inspect Browser and Application Storage
Review:
- Developer tools storage
- Local storage
- Session storage
- Cookies
- Cached responses
### 4. Inspect Logs and Responses
Check whether tokens appear in:
- Server logs
- Error messages
- Monitoring systems
- Debug output
### 5. Test Token Reusability
Determine whether an exposed token:
- Remains valid
- Grants authenticated access
- Works across devices or sessions
### 6. Verify Token Scope
Check whether the token provides:
- Read access
- Administrative access
- Long-lived authentication
- Refresh capability
### 7. Verify Exploitation
If tokens:
- Are exposed to unauthorized users
- Can be reused for authenticated access
-> vulnerability confirmed
# Impact
Token Leakage can lead to:
- Account takeover
- Session hijacking
- Authentication bypass
- Unauthorized API access
- Privilege escalation
- Long-term unauthorized access
Impact depends heavily on token permissions and expiration behavior.
# Remediation
1. Never expose tokens in URLs
2. Store tokens securely using appropriate storage mechanisms
3. Avoid logging sensitive authentication data
4. Apply short token expiration periods
5. Rotate and revoke exposed tokens immediately
6. Use secure transport (HTTPS only)
7. Protect tokens with secure cookie attributes where appropriate
8. Monitor for abnormal token usage
# Severity
**High to Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:L
```
**Score:** 9.1 (Critical)