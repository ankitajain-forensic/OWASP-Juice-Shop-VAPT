# A04:2025 — Cryptographic Failures

## Finding

**Vulnerability:** Sensitive Authentication Data Transmitted over HTTP

**Status:** Confirmed

**Severity:** Medium

**Affected Functionality:** User authentication / Login

---

## Description

The application was observed transmitting sensitive authentication-related data over unencrypted HTTP.

During testing, the login process was examined using Burp Suite. The application was operating over HTTP rather than HTTPS, meaning sensitive information transmitted between the client and application was not protected by transport-layer encryption.

---

## Testing Methodology

1. The application's login functionality was identified.
2. Login requests were intercepted using Burp Suite.
3. The request and response traffic was examined.
4. The protocol used for communication was reviewed.
5. Sensitive authentication-related information transmitted during the login process was assessed for transport protection.

---

## Observed Result

Authentication-related data was transmitted over HTTP without TLS encryption.

The testing environment used the local address `127.0.0.1`.

Therefore, the assessment demonstrated the use of unencrypted HTTP in the laboratory environment but did not demonstrate exploitation over an external network.

---

## Security Impact

If sensitive authentication information is transmitted without encryption over an untrusted network, an attacker positioned to intercept network traffic may potentially obtain or manipulate the transmitted information.

Potential impacts include:

- Exposure of authentication information
- Session compromise
- Credential interception
- Increased risk of man-in-the-middle attacks
- Loss of confidentiality during transmission

---

## Root Cause

The application was configured to use HTTP for authentication-related communication rather than enforcing HTTPS with appropriate TLS protection.

---

## Remediation

Recommended controls include:

1. Enforce HTTPS for all application traffic.
2. Configure TLS correctly and use a trusted certificate.
3. Redirect HTTP requests to HTTPS where appropriate.
4. Prevent sensitive information from being transmitted over unencrypted connections.
5. Configure secure cookie attributes such as `Secure` where applicable.
6. Ensure authentication endpoints are accessible only through encrypted communication.

---

## Evidence

Evidence was collected during testing using Burp Suite.

Screenshots should be sanitized before publication.

Sensitive information such as credentials, authentication tokens, session identifiers, cookies, and personal information must be removed or masked.

**Evidence status:** To be added after sanitization.

---

## Environment

**Application:** OWASP Juice Shop

**Testing Environment:** Local authorized laboratory environment

**Tools:** Kali Linux, Burp Suite, Firefox/Burp Suite Browser

**Assessment Type:** Web Application Vulnerability Assessment

---

## Disclaimer

This finding was identified in an intentionally vulnerable application within an authorized laboratory environment. The testing was performed for educational and security assessment purposes.
