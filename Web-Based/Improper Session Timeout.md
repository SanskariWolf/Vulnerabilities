# Description
Improper Session Timeout is a vulnerability that occurs when an application does not invalidate user sessions after an appropriate period of inactivity or after session termination events such as logout.

Session timeout mechanisms are intended to reduce the window in which a stolen, abandoned, or unattended session can be abused.

If sessions remain active longer than necessary, attackers may reuse valid sessions to gain unauthorized access.

Common session management issues include:
- Excessively long inactivity timeout
- Sessions remaining valid after logout
- No absolute session expiration
- Persistent authentication without re-verification
- Tokens remaining active after password change

Sensitive session data commonly affected:
- Session identifiers
- Authentication tokens
- Access tokens
- Persistent login cookies

Common causes include:
- Weak session lifecycle management
- Convenience-focused configurations
- Missing server-side invalidation
- Stateless token misuse
# Steps to Reproduce
### 1. Authenticate to the Application
Log in using valid credentials and establish a session.
### 2. Capture Session Information
Observe:
- Session cookies
- Authentication tokens
- Session identifiers
Example:
```http
Set-Cookie: sessionid=abc123
```
### 3. Remain Inactive
Do not interact with the application for the expected timeout duration.
Examples:
- 15 minutes
- 30 minutes
- Organization policy duration
### 4. Resume Session
Attempt to continue using the application without re-authentication.
Check whether:
- Session remains active
- Sensitive operations are still allowed
### 5. Test Logout Behavior
Log out and attempt to reuse:
- Old cookies
- Existing browser tabs
- Stored session identifiers
### 6. Verify Session Lifecycle Events
Check whether sessions are invalidated after:
- Password change
- Account disablement
- Credential reset
### 7. Verify Exploitation
If sessions:
- Remain valid beyond expected timeout
- Continue functioning after logout
- Allow reuse without re-authentication
-> vulnerability confirmed
# Impact
Improper Session Timeout can lead to:
- Session hijacking
- Unauthorized account access
- Persistent unauthorized sessions
- Increased exposure from abandoned devices
- Privilege misuse
Impact increases significantly for privileged accounts.
# Remediation
1. Implement inactivity-based session expiration
2. Configure absolute session lifetime limits
3. Invalidate sessions on logout server-side
4. Rotate session identifiers after authentication events
5. Invalidate sessions after password changes
6. Require re-authentication for sensitive actions
7. Apply shorter timeout values for administrative sessions
8. Monitor abnormal session duration patterns
# Severity
**Medium**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:L/A:N
```
**Score:** 6.5 (Medium)
