# Description

Unvalidated Webhook is a vulnerability that occurs when a web application accepts and processes webhook requests without properly validating their authenticity, integrity, or source.
Webhooks are commonly used for:
- Payment notifications
- CI/CD integrations
- Third-party service communication
- Messaging and automation systems

If webhook requests are not verified, attackers may forge requests and send malicious data to the application.

Common causes include:
- Missing signature verification
- No source validation
- Trusting user-controlled payloads    
- Lack of replay protection
This can allow attackers to trigger unauthorized actions or manipulate application behavior.
## Steps to Reproduce
### 1. Identify Webhook Endpoint
Locate webhook URLs such as:
```http
POST /webhook/payment
POST /api/webhooks/github
```
### 2. Intercept Legitimate Webhook Requests
Use:
- Burp Suite
- Request logging tools
- Application debugging logs
Capture:
- Headers
- Payload
- Signature fields    
### 3. Replay the Webhook Request
Resend the same request manually:
```bash
curl -X POST https://example.com/webhook/payment \
-H "Content-Type: application/json" \
-d '{"status":"paid","amount":"1000"}'
```
### 4. Modify Payload Data
Change sensitive values:
```json
{
  "status":"paid",
  "amount":"999999",
  "user":"admin"
}
```
### 5. Remove or Tamper Signature Headers
Modify or delete verification headers such as:
```http
X-Signature
X-Hub-Signature
Stripe-Signature
```
Check whether the application still processes the request.
### 6. Test Replay Protection
Send the same webhook multiple times.
If duplicate processing occurs → replay protection missing.
### 7. Verify Exploitation
If the application:
- Accepts unsigned requests
- Processes modified payloads
- Trusts attacker-controlled data
-> vulnerability confirmed
## Impact
Unvalidated Webhooks can lead to:
- Unauthorized transaction processing
- Fake payment confirmations
- Privilege escalation
- Triggering internal workflows
- Data manipulation
- Business logic abuse
In severe cases, attackers may compromise financial or operational processes.
## Remediation
1. Validate webhook signatures using shared secrets
2. Verify webhook source IPs where possible
3. Use HMAC verification for payload integrity
4. Implement replay protection using timestamps/nonces
5. Reject unsigned or malformed requests
6. Log and monitor webhook activity
7. Apply rate limiting to webhook endpoints
## Severity
**High**
## CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:L
```
**Score:** 8.8 (High)
