# Description
User Enumeration is a vulnerability that occurs when an application unintentionally reveals whether a user account, username, email address, phone number, or identifier exists within the system.

By observing differences in application behavior, attackers can determine valid users and build targeted account lists for further attacks.

User Enumeration commonly occurs in:
- Login pages
- Registration flows
- Password reset functionality
- Account recovery mechanisms
- Public profile endpoints
- APIs and authentication services

Typical enumeration indicators include:
- Different error messages
- Different HTTP status codes
- Response timing differences
- Different redirects
- Distinct email or notification behavior

Examples:
```text
Username does not exist
```
vs
```text
Incorrect password
```
Although User Enumeration and [[Account Enumeration]] are closely related, User Enumeration focuses specifically on revealing **valid identities**, while Account Enumeration may include broader account-state discovery.

Common causes include:
- Verbose authentication messages
- Detailed API responses
- Improper error handling
- Weak recovery workflows
- Public user discovery functionality
# Steps to Reproduce
### 1. Identify User-Related Endpoints
Locate functionality such as:
- Login pages
- Registration forms
- Password reset pages
- User lookup APIs
- Profile discovery features
### 2. Submit Requests Using Valid and Invalid Users
Send requests with:
- A known valid identifier
- A random or invalid identifier
Example:
```http
POST /login
```
Observe response behavior.
### 3. Compare Application Responses
Review differences in:
- Error messages
- Response codes
- Response size
- Redirect behavior
- Processing time
Examples:
```text
Incorrect password
```
vs
```text
User not found
```
### 4. Test Recovery and Registration Flows
Attempt:
- Password reset requests
- Account registration
- Username availability checks
Observe whether existence is disclosed.
### 5. Review Side Effects
Determine whether differences exist in:
- Email delivery
- SMS notifications
- Verification messages
### 6. Evaluate API Behavior
Inspect whether APIs expose:
```json
{
  "exists": true
}
```
or similar indicators.
### 7. Verify Exploitation
If the application:
- Reveals valid user identities
- Produces distinguishable behavior
-> vulnerability confirmed
# Impact
User Enumeration can lead to:
- Targeted credential attacks
- Password spraying
- Credential stuffing
- Privacy exposure
- Improved phishing success
- More efficient account takeover attempts
This weakness often reduces attacker effort significantly.
# Remediation
1. Return generic authentication responses
Example:
```text
Invalid credentials
```
2. Standardize response timing
3. Use consistent HTTP status codes
4. Avoid disclosing account existence in recovery flows
5. Implement rate limiting and abuse detection
6. Monitor enumeration attempts
7. Apply CAPTCHA where appropriate
8. Limit public user discovery mechanisms
# Severity
**Low to Medium**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N
```
**Score:** 5.3 (Medium)