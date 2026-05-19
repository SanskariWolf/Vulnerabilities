# Description
Cache Poisoning is a vulnerability that occurs when an attacker manipulates content stored in a cache so that malicious, incorrect, or attacker-controlled responses are served to legitimate users.

Caching mechanisms are commonly used to improve performance by storing previously generated responses. If cache keys, headers, or response logic are improperly configured, attackers may influence cached content and cause users to receive unintended responses.

Affected caching layers may include:
- Web caches
- Reverse proxies
- CDN caches
- Application caches
- API gateways
- Browser caches

Common causes include:
- Untrusted headers included in cache keys
- Improper cache-control configuration
- Dynamic content being cached
- Missing cache segmentation
- Cache key inconsistencies
- User-specific responses being cached globally
# Steps to Reproduce
### 1. Identify Cached Endpoints
Locate pages or APIs that appear to use caching.
Indicators may include:
```text
Cache-Control
ETag
Age
X-Cache
```
### 2. Capture a Baseline Response
Send a normal request.
Example:
```http
GET /profile
```
Observe:
- Response headers
- Content behavior
- Cache indicators
### 3. Identify Cache Influencing Inputs
Check whether responses vary based on:
- Query parameters
- Request headers
- Host values
- Language settings
- Forwarded headers
### 4. Manipulate Cache Inputs
Modify cache-related inputs and observe whether the response changes.
Examples:
```http
X-Forwarded-Host
Host
X-Original-URL
```
Check whether manipulated responses become cached.
### 5. Request Resource Again
Repeat the request without manipulation.
Determine whether:
- Modified content persists
- Cached content affects additional users
### 6. Verify Cache Scope
Check whether:
- Cache is shared
- Responses cross user boundaries
- Dynamic responses are cached globally
### 7. Verify Exploitation
If attacker-controlled responses:
- Become cached
- Are served to other users
-> vulnerability confirmed
# Impact
Cache Poisoning can lead to:
- Delivery of malicious content
- Session exposure
- Authentication confusion
- Information disclosure
- Stored client-side attacks
- Redirection to attacker-controlled content
- Denial of Service (DoS)
Impact depends on cache location and affected audience.
# Remediation
1. Define cache keys explicitly
2. Avoid caching user-specific responses
3. Ignore untrusted request headers in cache logic
4. Configure proper `Cache-Control` directives
5. Separate authenticated and unauthenticated cache content
6. Validate inputs affecting response generation
7. Implement cache invalidation policies
8. Monitor abnormal cache behavior
# Severity
**Medium to High**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:H/A:L
```
**Score:** 8.0 (High)