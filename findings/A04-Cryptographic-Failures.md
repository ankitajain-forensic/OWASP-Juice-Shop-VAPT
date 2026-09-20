# A04:2025 — Cryptographic Failures

## Finding

**Vulnerability:** Authentication Data Transmitted over Unencrypted HTTP

**Status:** Confirmed

**Severity:** Medium

**Affected Functionality:** User Authentication / Login

**Endpoint:** `POST /rest/user/login`

---

## Description

Cryptographic Failures occur when an application fails to adequately protect sensitive data in transit or at rest, commonly through the absence of encryption, use of weak cryptographic protocols, or misconfigured transport security.

During testing, requests to the application's login functionality were observed being transmitted over plain HTTP rather than HTTPS/TLS. As a result, authentication credentials and session-related data were transmitted without encryption.

---

## Testing Procedure

1. The login functionality of OWASP Juice Shop was identified during application testing.
2. Login requests were intercepted using Burp Suite to inspect the transport-layer configuration of the request.
3. The protocol used for the request (HTTP vs. HTTPS) was recorded.
4. The request and response were examined to confirm whether credentials and authentication tokens were visible in plaintext.

---

## Observation

The login request was observed being sent over HTTP, with the username/email and password values visible in plaintext within the intercepted request body. The corresponding response, containing the authentication token, was likewise unencrypted in transit.

The assessment was performed against the application running on `127.0.0.1` in the local laboratory environment, so exploitation of this weakness across an external network (e.g., via network sniffing or a man-in-the-middle position) was not practically demonstrated, though the absence of TLS on the login endpoint was directly confirmed.

---

## Security Impact

Transmitting authentication data over an unencrypted channel exposes credentials and session tokens to interception by any party with access to the network path between client and server.

Depending on the network position of an attacker, this weakness could lead to:

- Credential theft via network interception
- Session hijacking through captured authentication tokens
- Full account compromise if intercepted credentials are reused

The practical severity is influenced by deployment context — this weakness carries substantially higher real-world risk when the application is exposed on an untrusted or shared network rather than a local loopback address.

---

## Root Cause

The application did not enforce HTTPS/TLS for authentication-related traffic, allowing the login request and response to be transmitted without encryption.

---

## Remediation

Recommended controls include:

1. Enable HTTPS/TLS for all application communication, with particular priority on authentication and session-related endpoints.
2. Redirect all HTTP requests to HTTPS at the server or load-balancer level.
3. Enforce HTTP Strict Transport Security (HSTS) to prevent protocol downgrade.
4. Ensure authentication tokens and session cookies are only transmitted over secure channels (`Secure` cookie flag).
5. Regularly audit application endpoints to confirm no sensitive functionality is reachable over unencrypted HTTP.

---

## Evidence

Screenshots below show the intercepted login request and response transmitted over HTTP, with credentials and token values visible. Sensitive values have been redacted prior to publishing.

![Login request intercepted over HTTP showing plaintext credentials](images/a04-01-request-http-login.png)`
`![Login response over HTTP showing authentication token](images/a04-02-response-http-token.png)`

---

## Environment

**Application:** OWASP Juice Shop

**Testing Environment:** Local authorized laboratory environment

**Tools:** Kali Linux, Burp Suite, Firefox/Burp Suite Browser

**Assessment Type:** Web Application Vulnerability Assessment

---

## Disclaimer

This finding was identified in an intentionally vulnerable application within an authorized laboratory environment. The testing was performed for educational and security assessment purposes.
