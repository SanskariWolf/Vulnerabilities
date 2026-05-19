# Description
HTTP Response Splitting is a vulnerability that occurs when an application includes untrusted user input in HTTP response headers without proper validation or encoding, allowing attackers to manipulate how responses are interpreted by browsers, proxies, or downstream systems.

HTTP responses use headers and body sections separated by line delimiters. If attackers can inject special characters into response headers, they may alter response structure and cause unintended behavior.

This vulnerability commonly affects:
- Redirect functionality
- Header generation
- Cookie handling
- Custom response headers
- Proxy integrations

Common causes include:
- Unsanitized user input in headers
- Improper redirect handling
- Unsafe cookie generation
- Missing header validation

Historically, exploitation often relied on CRLF (Carriage Return + Line Feed) injection.
# Steps to Reproduce
### 1. Identify Header Reflection Points
Locate user-controlled input reflected into response headers.
Examples:
- Redirect parameters
- Custom headers
- Download filenames
- Cookie values
### 2. Capture Baseline Response
Send a normal request and inspect:
```http
HTTP/1.1 302 Found
Location: /dashboard
```
Observe response structure.
### 3. Modify User Input
Provide specially crafted input intended to alter response formatting.
Examples to test:
- Unexpected line breaks
- Header separators
- Encoded control characters
Observe whether additional response elements appear.
### 4. Inspect Returned Headers
Review whether:
- Additional headers appear
- Existing headers are modified
- Response structure changes
Example indicators:
```http
Set-Cookie:
Location:
Content-Type:
```
### 5. Validate Response Behavior
Check whether manipulation results in:
- Unexpected redirects
- Header modification
- Altered cache behavior
- Incorrect rendering
### 6. Review Cross-Component Effects
Determine whether:
- Proxies behave differently
- Browsers interpret responses unexpectedly
- Cache behavior changes
### 7. Verify Exploitation
If attacker-controlled input:
- Modifies response headers
- Alters response boundaries
- Influences browser or proxy behavior
-> vulnerability confirmed
# Impact
HTTP Response Splitting can lead to:
- Cache poisoning
- Session manipulation
- Redirect abuse
- Content injection
- Information disclosure
- Cross-user response impact
Impact depends on affected infrastructure and response handling.
# Remediation
1. Validate and sanitize all data used in response headers
2. Reject control characters in header values
3. Use framework-managed response APIs
4. Avoid direct header construction from user input
5. Encode user-controlled values appropriately
6. Implement strict redirect validation
7. Monitor abnormal header generation behavior
8. Keep web frameworks and proxies updated
# Severity
**Medium to High**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:H/A:N
```
**Score:** 7.4 (High)