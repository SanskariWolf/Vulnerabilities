# Description

Broken OAuth Implementation is a vulnerability that occurs when an application improperly implements the OAuth authentication or authorization flow, allowing attackers to bypass authentication, steal tokens, or gain unauthorized access to user accounts.

OAuth is commonly used to allow users to authenticate using third-party providers such as:
- Google
- Microsoft
- GitHub
- Facebook

Improper validation of OAuth parameters, redirect URIs, tokens, or scopes can introduce serious security risks.

Common implementation flaws include:
- Missing `state` parameter validation
- Open redirect vulnerabilities
- Token leakage
- Improper redirect URI validation
- Account linking issues
- Weak scope validation
# Steps to Reproduce

### 1. Identify OAuth Authentication Flow
Locate OAuth-based login functionality such as:
- “Login with Google”
- “Sign in with GitHub”
- OAuth API authorization flows
### 2. Intercept OAuth Requests
Use:
- Browser Developer Tools
- Burp Suite

Capture authorization requests and responses.
Example request:
```http
GET /authorize?
client_id=example123
&redirect_uri=https://example.com/callback
&response_type=code
&state=random123
```
### 3. Test `state` Parameter Validation
Modify or remove the `state` parameter:
```http
&state=attackercontrolled
```
Check whether the application properly validates it.
### 4. Test Redirect URI Validation
Modify the `redirect_uri` parameter:
```http
&redirect_uri=https://attacker.com/callback
```
If accepted -> potential token theft/open redirect.
### 5. Attempt Authorization Code Reuse
Replay authorization codes or exchange them multiple times.

### 6. Analyze Token Handling
Inspect:
- Access tokens
- ID tokens
- Refresh tokens

Check whether:
- Tokens expire properly
- Tokens are validated correctly
- Tokens are exposed in URLs or logs
### 7. Verify Exploitation
If the application:
- Accepts malicious redirect URIs
- Fails to validate `state`
- Allows token reuse
- Improperly links accounts
-> vulnerability confirmed
## Impact
Broken OAuth Implementation can lead to:
- Account takeover 
- Authentication bypass
- Token theft
- Unauthorized API access
- Session hijacking
- Privilege escalation
In severe cases, attackers may fully compromise user accounts.
## Remediation
1. Strictly validate `redirect_uri` values
2. Always implement and verify the `state` parameter
3. Use secure OAuth flows (Authorization Code + PKCE)
4. Avoid exposing tokens in URLs
5. Properly validate scopes and permissions
6. Expire authorization codes after single use
7. Securely store and rotate tokens
8. Follow OAuth 2.0 and OpenID Connect best practices
## Severity
**High to Critical**
## CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H
```
**Score:** 8.8 (High)
