# Description
Account Enumeration is a vulnerability that occurs when an application reveals whether a user account exists by returning distinguishable responses during authentication, registration, password recovery, or account management flows.

Instead of returning generic responses, the application unintentionally exposes information that allows attackers to determine whether usernames, email addresses, phone numbers, or user IDs are valid.

Attackers commonly exploit this weakness to build lists of valid accounts before conducting further attacks.

Account enumeration may occur through:
- Login forms
- Password reset functionality
- Registration pages
- Account recovery flows
- API responses
- Error messages

Common indicators include:
- Different error messages
- Different response codes
- Response timing differences
- Different redirects
- Different email or SMS behavior

Examples:
```text
Invalid password
```
vs
```text
User does not exist
```
# Steps to Reproduce
### 1. Identify User-Related Functionality
Locate endpoints such as:
- Login pages
- Password reset forms
- Registration pages    
- Account recovery APIs
### 2. Submit Requests with Existing and Non-Existing Accounts
Send requests using:
- A known valid account
- A random or invalid account

Example:
```http
POST /login
```
Observe application behavior.
### 3. Compare Responses
Check whether differences exist in:
- Error messages
- HTTP status codes
- Response body length
- Redirect behavior
- Response timing

Examples:
```text
Incorrect password
```
vs
```text
Account not found
```
### 4. Test Password Recovery Flows
Submit password reset requests using:
- Existing accounts
- Non-existing accounts
Observe whether responses differ.
### 5. Evaluate Registration Behavior
Attempt account creation using
- Existing identifiers
- New identifiers
Determine whether account existence is disclosed.
### 6. Review Side Effects
Observe:
- Email delivery behavior
- SMS responses
- Notification differences
### 7. Verify Exploitation
If the application:
- Reveals whether accounts exist
- Produces distinguishable responses
-> vulnerability confirmed
# Impact
Account Enumeration can lead to:
- Targeted credential attacks
- Credential stuffing
- Password spraying
- User privacy exposure
- Increased success of account takeover attempts
- More effective phishing campaigns
Although account enumeration does not directly compromise accounts, it significantly reduces attacker effort.
# Remediation
1. Return generic authentication responses

Example:
```text
Invalid username or password
```
2. Standardize response timing
3. Use identical HTTP status codes
4. Avoid revealing account existence in recovery flows
5. Apply rate limiting and monitoring
6. Introduce abuse detection controls
7. Use CAPTCHA where appropriate
8. Log enumeration attempts for investigation
# Severity
**Low to Medium**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N
```
**Score:** 5.3 (Medium)