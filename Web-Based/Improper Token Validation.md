# Description

Improper Token Validation is a vulnerability that occurs when an application fails to properly verify the authenticity, integrity, expiration, or ownership of authentication or session tokens.

Tokens are commonly used for:
- Authentication
- Session management
- Password reset flows
- API authorization

If validation is weak or missing, attackers may be able to:
- Forge tokens    
- Reuse expired tokens
- Bypass authentication
- Access unauthorized accounts or resources

This issue is commonly associated with:
- JSON Web Tokens (JWT)
- Session tokens
- OAuth tokens
- API bearer tokens
# Steps to Reproduce

### 1. Authenticate to the Application
Log in with a valid account and capture the issued token using:
- Browser Developer Tools
- Burp Suite
- API clients

Example:
```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR...
```
### 2. Analyze the Token

Inspect:
- Payload contents
- Expiration time (`exp`)
- User identifiers
- Signing algorithm

For JWTs:
- Decode using online tools or local scripts
### 3. Modify Token Data
Attempt changes such as:
- Changing user ID
- Modifying role (`user` → `admin`)
- Removing expiration claims
- Altering token signature

Example modified payload:
```json
{
  "user":"admin",
  "role":"administrator"
}
```
### 4. Replay or Reuse Token
Test:
- Expired tokens
- Logged-out tokens    
- Tokens from another account
### 5. Attempt Algorithm Manipulation (JWT)
Check for insecure configurations such as:
- `alg:none`
- Weak signing secrets

Example:
```json
{
  "alg":"none",
  "typ":"JWT"
}
```
### 6. Send Modified Token
Replace the original token with the modified version and resend the request.
### 7. Verify Exploitation
If the application:
- Accepts forged tokens
- Grants unauthorized access
- Ignores expiration/signature validation
-> vulnerability confirmed

# Impact
Improper Token Validation can lead to:
- Authentication bypass
- Account takeover
- Privilege escalation
- Unauthorized API access
- Session hijacking
- Exposure of sensitive data
In severe cases, attackers may gain full administrative access.
## Remediation
1. Properly validate token signatures
2. Reject tokens using insecure algorithms (`alg:none`)
3. Use strong secret keys and secure signing algorithms
4. Validate token expiration (`exp`) and issuer claims
5. Implement token revocation and rotation mechanisms
6. Use short-lived access tokens
7. Bind tokens to users/devices where possible
8. Store tokens securely (avoid local storage when possible)
# Severity

**High to Critical**

# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```
**Score:** 9.8 (Critical)
