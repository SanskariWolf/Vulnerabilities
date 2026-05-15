# Description
Insecure Logout is a vulnerability that occurs when an application fails to properly terminate user sessions after logout, allowing authenticated sessions to remain active or reusable.

Logging out should invalidate the user's authenticated state both client-side and server-side. If session invalidation is incomplete, attackers may continue using previously issued session identifiers, tokens, or active browser sessions.

Common logout weaknesses include:
- Session remains valid after logout
- Server-side session not invalidated
- Tokens remain usable after logout
- Logout only clears client-side storage
- Multiple active sessions remain unaffected
- Refresh tokens remain active

Affected session mechanisms may include:
- Session cookies
- Access tokens
- Refresh tokens
- Persistent login mechanisms
# Steps to Reproduce
### 1. Authenticate to the Application
Log in using valid credentials and establish an authenticated session.
### 2. Capture Session Information
Observe active session identifiers.
Examples:
```http
Set-Cookie: sessionid=abc123
```
or
```http
Authorization: Bearer access_token
```
### 3. Perform Logout
Use the application's logout functionality.
Example:
```http
POST /logout
```
### 4. Attempt Session Reuse
Try reusing:
- Existing browser tabs
- Stored cookies
- Previously captured tokens
Check whether authenticated access is still allowed.
### 5. Test Multi-Session Behavior
If multiple devices/sessions are supported:
- Log out from one device
- Verify whether other active sessions remain valid
### 6. Test Token Revocation
Check whether:
- Access tokens remain usable
- Refresh tokens can still generate sessions
- Cached sessions survive logout
### 7. Verify Exploitation
If logout:
- Does not invalidate server-side sessions
- Allows reuse of previous credentials
- Leaves authenticated access active
-> vulnerability confirmed
# Impact
Insecure Logout can lead to:
- Session hijacking
- Unauthorized account access
- Persistent authenticated sessions
- Abuse of shared devices
- Increased exposure after credential compromise
Impact becomes more severe for privileged or administrative accounts.
# Remediation
1. Invalidate sessions server-side during logout
2. Revoke access and refresh tokens immediately
3. Clear client-side session data and cookies
4. Destroy server session state completely
5. Invalidate all active sessions after sensitive actions:
    - Password change
    - Credential reset
    - Account recovery
6. Implement short session lifetimes
7. Require re-authentication for sensitive operations
8. Provide users the ability to terminate all active sessions
# Severity
**Medium to High**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:L/A:N
```
**Score:** 6.5 (Medium)