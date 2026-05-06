# Description
Missing Multi-Factor Authentication (MFA) is a security weakness where an application relies solely on a single authentication factor, typically a username and password, without requiring additional verification methods.

Multi-Factor Authentication enhances security by requiring users to provide two or more authentication factors, such as:
- Something they know (password)
- Something they have (OTP device, mobile app)
- Something they are (biometrics)

Without MFA, compromised credentials alone may be sufficient for attackers to gain unauthorized access to user accounts or administrative systems.

This issue is especially critical for:
- Administrative accounts
- Financial systems
- Remote access portals
- Cloud dashboards
- Email accounts
# Steps to Reproduce
### 1. Identify Authentication Functionality
Locate login interfaces such as:
- Web application login pages
- VPN portals
- Administrative dashboards
- API authentication endpoints
### 2. Attempt Standard Login
Authenticate using valid credentials:
```http
POST /login
```
Observe whether access is granted immediately after entering username and password.
### 3. Check for Additional Verification
Verify whether the application requests:
- One-Time Passwords (OTP)
- Authenticator app verification
- Push notifications
- Hardware security keys
- Biometric confirmation
### 4. Attempt Login from New Device or Location
Test whether additional verification is triggered when:
- Logging in from a new IP
- Using a different browser/device
- Accessing sensitive functionality
### 5. Verify Exploitation
If the application grants access using only a password without additional verification:
-> vulnerability confirmed
# Impact
Missing Multi-Factor Authentication can lead to:
- Account takeover
- Unauthorized access
- Credential stuffing attacks
- Brute-force attack success
- Privilege escalation
- Exposure of sensitive data
If credentials are leaked or reused, attackers may immediately gain access.
# Remediation
1. Implement Multi-Factor Authentication for all users
2. Enforce MFA for administrative and privileged accounts
3. Support secure MFA methods:
    - Authenticator apps
    - Hardware security keys (FIDO2/WebAuthn)
    - Push-based authentication
4. Avoid relying solely on SMS-based MFA where possible
5. Implement adaptive/risk-based authentication
6. Require MFA during sensitive operations (password change, payment approval, etc.)
7. Monitor suspicious login activity
# Severity
**Medium to High**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:L
```
**Score:** 8.1 (High)