# Description
JWT None Algorithm Attack is a vulnerability that occurs when an application improperly accepts JSON Web Tokens (JWTs) using the `alg: none` algorithm and treats unsigned tokens as valid.

JWTs are commonly used for:
- Authentication
- Session management
- API authorization
- Identity federation

A JWT normally contains:
- Header
- Payload
- Signature

If signature verification is disabled or incorrectly implemented, attackers may modify token contents and submit an unsigned token to impersonate users or elevate privileges.

Example vulnerable JWT header:
```json
{
  "alg": "none",
  "typ": "JWT"
}
```

This vulnerability generally occurs due to:
- Trusting client-provided algorithms
- Disabled signature verification
- Insecure JWT library configuration
- Improper authentication implementation
# Steps to Reproduce
### 1. Obtain a Valid JWT
Authenticate normally and capture the issued JWT.
Example:
```http
Authorization: Bearer eyJhbGciOiJIUzI1Ni...
```
### 2. Decode the Token
Inspect the JWT components:
- Header
- Payload
- Signature
Review whether the token uses:
```json
{
  "alg":"HS256"
}
```
or another signed algorithm.
### 3. Modify the Header
Change the algorithm value:
```json
{
  "alg":"none",
  "typ":"JWT"
}
```
### 4. Modify Claims
Attempt changing authorization-related fields.
Example:
```json
{
  "user":"admin",
  "role":"administrator"
}
```
### 5. Remove the Signature
Construct an unsigned JWT:
- Header
- Payload
- Empty signature section
### 6. Submit Modified Token
Replace the original JWT with the modified token and resend the authenticated request.
### 7. Verify Exploitation
If the application:
- Accepts unsigned tokens
- Grants access using modified claims
- Ignores signature validation
-> vulnerability confirmed
# Impact
JWT None Algorithm Attack can lead to:
- Authentication bypass
- Account takeover
- Privilege escalation
- Unauthorized API access
- Session compromise
- Full application compromise
Impact is typically severe because trust boundaries are broken.
# Remediation
1. Explicitly disable support for `alg: none` in production
2. Enforce strict server-side algorithm validation
3. Never trust algorithm values provided by clients
4. Require signature verification for all JWTs
5. Use modern JWT libraries with secure defaults
6. Rotate signing keys periodically
7. Validate:
    - Signature
    - Issuer (`iss`)
    - Audience (`aud`)
    - Expiration (`exp`)
8. Perform authentication security reviews regularly
# Severity
**Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```
**Score:** 9.8 (Critical)