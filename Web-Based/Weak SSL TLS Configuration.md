# Description
**SSL (Secure Sockets Layer)** and **TLS (Transport Layer Security)** are cryptographic protocols used to secure communication over networks.

Modern systems primarily use TLS (SSL is deprecated). When HTTP is secured using TLS, it becomes HTTPS, ensuring:
- **Confidentiality** (encryption of data)
- **Integrity** (protection against tampering)
- **Authentication** (server identity via certificates)

However, improper configuration of SSL/TLS can introduce serious vulnerabilities, such as:
- Support for **deprecated protocols** (SSLv2, SSLv3, TLS 1.0, TLS 1.1)
- Use of **weak cipher suites** (e.g., RC4, DES, NULL ciphers)
- Misconfigured certificate chains
- Lack of protections against known attacks (e.g., BEAST, POODLE, CRIME)

These weaknesses may allow attackers to:
- Decrypt sensitive communications
- Perform Man-in-the-Middle (MITM) attacks
- Downgrade connections to weaker encryption
- Cause denial-of-service conditions
# Steps
1. Identify SSL/TLS Services
	- Scan for open SSL/TLS ports and services:
	- `nmap -sV --reason -PN -n --top-ports 100 www.example.com`
2. Enumerate Supported Protocols & Ciphers
	- Check for weak protocols and cipher suites:
	- `nmap --script ssl-cert,ssl-enum-ciphers -p 443,465,993,995 www.example.com`
3. Analyze Certificate & Handshake via [OpenSSL](https://www.openssl.org/) (Manually)
	- `openssl s_client -connect www2.example.com:443`
	- Look for: Expired/self-signed certificates, Weak signature algorithms (e.g., SHA1), Improper certificate chain
4. (Optional) Java-based Testing Tool via [TestSSLServer](https://www.bolet.org/TestSSLServer/)
	- `java -jar TestSSLServer.jar www3.example.com 443`
	- This checks for: POODLE, BEAST, CRIME, Heartbleed, Weak ciphers
5. Advanced Scanning with [sslyze](https://github.com/nabla-c0d3/sslyze)
	- `./sslyze.py --regular example.com:443`
6. Test for Known SSL/TLS Vulnerabilities with [testssl.sh](https://github.com/testssl/testssl.sh)
	- `testssl.sh owasp.org`
# Impact
Weak SSL/TLS configurations can lead to:
- Man-in-the-Middle (MITM) attacks
- Decryption of sensitive data (credentials, tokens, sessions)
- Session hijacking
- Downgrade attacks
- Loss of data confidentiality and integrity
- Compliance violations (PCI-DSS, GDPR)
# Remediation
1. Disable deprecated protocols
    - Disable: SSLv2, SSLv3, TLS 1.0, TLS 1.1
    - Enable only: TLS 1.2 and TLS 1.3
2. Use strong cipher suites
    - Prefer: AES-GCM, CHACHA20-POLY1305
    - Avoid: RC4, DES, 3DES, NULL ciphers
3. Enable Perfect Forward Secrecy (PFS)
    - Use ECDHE key exchange
4. Configure secure renegotiation
    - Disable insecure renegotiation
5. Use valid certificates
    - Signed by trusted CA
    - Avoid expired/self-signed certs
6. Enable HTTP Strict Transport Security (HSTS)
7. Regularly test SSL/TLS configuration
    - Use tools like:
        - testssl.sh
        - sslyze
# Severity
**Medium to High** (can be Critical in specific cases)
- **Medium** → Weak ciphers but no practical exploit
- **High** → Supports deprecated protocols enabling downgrade/MITM
- **Critical** → Actively exploitable vulnerabilities (e.g., Heartbleed, POODLE with real impact)
# CVSS
**High Severity (Weak protocols + MITM possible)**
`CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:L/A:N`
**Score:** ~7.4 (High)

**Medium Severity (Weak ciphers only)**
`CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N`
**Score:** ~5.3 (Medium)