# Description
HTTP Request Smuggling is a vulnerability that occurs when inconsistencies in HTTP request parsing between multiple servers (such as a reverse proxy, load balancer, CDN, API gateway, or backend server) allow attackers to manipulate how requests are interpreted and processed.

This vulnerability typically arises when two systems disagree on request boundaries.

Common scenarios involve:
- Frontend proxy + backend server
- Load balancer + application server
- CDN + origin server
- API gateway + backend API

Request parsing inconsistencies commonly involve:
- `Content-Length (CL)`
- `Transfer-Encoding (TE)`
- Conflicting headers
- Incomplete request normalization

When exploited, attackers may cause one server to interpret part of a request differently from another server.

Common variants include:
- CL.TE (Content-Length → Transfer-Encoding)
- TE.CL (Transfer-Encoding → Content-Length)
- TE.TE (Transfer-Encoding ambiguity)
# Steps to Reproduce
### 1. Identify Multi-Tier HTTP Architecture
Determine whether requests pass through:
- Reverse proxies
- Load balancers
- CDNs
- Backend application servers

Observe headers such as:
```http
Via
X-Forwarded-For
Server
```
### 2. Capture Baseline Requests
Send normal requests and observe:
- Response behavior
- Connection reuse
- Header normalization
Example:
```http
GET / HTTP/1.1
Host: example.com
```
### 3. Test Request Parsing Behavior
Send malformed or ambiguous requests and observe whether frontend and backend process them differently.
Focus areas:
- Multiple transfer indicators
- Inconsistent body handling
- Unexpected response desynchronization
### 4. Observe Desynchronization Indicators
Look for:
- Unexpected redirects
- Responses belonging to other requests
- Delayed responses
- Backend processing anomalies
### 5. Test Request Queue Behavior
Determine whether:
- Responses become misaligned
- Cached responses appear unexpectedly
- Requests affect subsequent users
### 6. Validate Session and Routing Behavior
Check whether desynchronization impacts:
- Authentication state
- Request routing
- Response delivery
### 7. Verify Exploitation
If HTTP parsing inconsistencies:
- Alter request boundaries
- Affect backend processing
- Cause request desynchronization
-> vulnerability confirmed
# Impact
HTTP Request Smuggling can lead to:
- Authentication bypass
- Session hijacking
- Cache poisoning
- Request desynchronization
- Access control bypass
- Information disclosure
- Credential theft
- Cross-user impact
Because attacks may affect other users, impact can extend beyond a single session.
# Remediation
1. Normalize HTTP request parsing across infrastructure
2. Ensure consistent handling of request boundaries
3. Reject ambiguous or malformed requests
4. Disable unsupported transfer behaviors
5. Keep reverse proxies and backend servers updated
6. Use secure gateway configurations
7. Monitor abnormal request patterns
8. Test request parsing during security assessments
# Severity
**High to Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:H/PR:N/UI:N/S:C/C:H/I:H/A:L
```
**Score:** 8.6 (High)