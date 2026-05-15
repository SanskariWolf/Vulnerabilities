# Description
JWT Signature Bypass is a vulnerability that occurs when an application improperly validates JSON Web Token (JWT) signatures, allowing attackers to modify token contents without possessing the legitimate signing key.

JWTs are commonly used for:
- Authentication
- Session management
- API authorization
- Identity assertions

A JWT normally contains:
- Header
- Payload
- Signature

Applications should always verify that:
- The token signature is valid
- The expected signing algorithm is enforced
- The token was issued by a trusted authority

If signature verification is missing or implemented incorrectly, attackers may tamper with claims such as user identity or role and gain unauthorized access.
Common causes include:
- Disabled signature verification
- Trusting the algorithm specified in the token
- Weak JWT library configuration
- Accepting unsigned or improperly signed tokens
- Confusion between symmetric and asymmetric algorithms
# Steps to Reproduce
### 1. Obtain a Valid JWT
Authenticate normally and capture a JWT.
Example:
```http
Authorization: Bearer eyJhbGciOi...
```
### 2. Decode the Token
Inspect:
- Header
- Payload
- Signature
Example:
```json
{
  "alg":"HS256",
  "typ":"JWT"
}
```
### 3. Modify Claims
Change authorization-related values.
Example:
```json
{
  "user":"admin",
  "role":"administrator"
}
```
### 4. Reconstruct the JWT
Create a modified token without using the legitimate signing key.
Examples of indicators to test:
- Altered payload accepted
- Invalid signatures accepted
- Signature ignored during validation
### 5. Submit Modified Token
Replace the original JWT and resend the request.
Example:
```http
Authorization: Bearer modified.jwt.token
```
### 6. Observe Application Behavior
Check whether:
- Authentication succeeds
- Privileges increase
- Protected endpoints become accessible
### 7. Verify Exploitation
If the application:
- Accepts modified JWTs
- Ignores signature validation
- Grants access based on altered claims
-> vulnerability confirmed
# Impact
JWT Signature Bypass can lead to:
- Authentication bypass
- Account takeover
- Privilege escalation
- Unauthorized API access
- Session compromise
- Full application compromise
Because JWTs are often trusted across systems, the impact can extend beyond a single application.
# Remediation
1. Always verify JWT signatures server-side
2. Enforce an expected signing algorithm
3. Reject unsigned or improperly signed tokens
4. Do not trust algorithm values supplied by clients
5. Use strong signing keys and rotate them periodically
6. Validate:
    - Signature
    - Issuer (`iss`)
    - Audience (`aud`)
    - Expiration (`exp`)
    - Subject (`sub`)
7. Use well-maintained JWT libraries with secure defaults
8. Perform authentication and authorization testing regularly
# Severity
**Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```
**Score:** 9.8 (Critical)