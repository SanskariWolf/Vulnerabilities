# Description
Brute Force Attack is a vulnerability (or security weakness) that occurs when an application allows repeated authentication attempts without sufficient protections, enabling attackers to systematically guess valid credentials, tokens, keys, or authentication values until successful.

Attackers typically automate repeated requests against authentication mechanisms to discover valid credentials.

Targets commonly include:
- Login forms
- Administrative portals
- API authentication endpoints
- Password reset mechanisms
- OTP verification flows
- Session identifiers
- Access tokens

Common brute force techniques include:
- Password guessing
- Credential stuffing
- Password spraying
- Token brute forcing
- OTP guessing

Common causes include:
- Missing rate limiting
- No account lockout policy
- Weak password requirements
- Missing Multi-Factor Authentication (MFA)
- Unlimited login attempts
- Predictable authentication values
# Steps to Reproduce
### 1. Identify Authentication Mechanisms
Locate authentication-related functionality:
- Login pages
- API authentication endpoints
- Administrative interfaces
- Recovery mechanisms
### 2. Establish Baseline Authentication Behavior
Submit normal authentication requests.
Example:
```http
POST /login
```
Observe:
- Response behavior
- Error handling
- Authentication flow
### 3. Perform Multiple Authentication Attempts
Attempt repeated authentication requests using different credential values.
Evaluate whether controls exist for:
- Rate limiting
- Temporary blocking
- CAPTCHA
- Progressive delays
### 4. Monitor Response Behavior
Check whether:
- Unlimited attempts are allowed
- Response timing remains unchanged
- No detection occurs
### 5. Evaluate Account Protection
Verify whether:
- Account lockout is enforced
- MFA is required
- Suspicious activity alerts trigger
### 6. Validate Recovery and OTP Flows
Check whether:
- Password reset requests can be abused
- Verification codes permit excessive attempts
### 7. Verify Exploitation
If authentication controls:
- Allow excessive attempts
- Permit credential guessing without effective mitigation
-> vulnerability confirmed
# Impact
Brute Force Attack can lead to:
- Account takeover
- Unauthorized access
- Credential compromise
- Administrative access abuse
- Increased success of credential stuffing
- Service disruption
Impact increases significantly for privileged or externally accessible accounts.
# Remediation
1. Implement rate limiting on authentication endpoints
2. Enforce account lockout or progressive delays
3. Enable Multi-Factor Authentication (MFA)
4. Require strong password policies
5. Deploy CAPTCHA where appropriate
6. Monitor and alert on abnormal login patterns
7. Restrict authentication attempts by IP, device, or behavior
8. Secure password reset and OTP workflows
# Severity
**Medium to High**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:L
```
**Score:** 8.1 (High)