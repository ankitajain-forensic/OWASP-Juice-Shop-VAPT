# A07:2025 — Authentication Failures

## Finding

**Vulnerability:** Lack of Brute-Force Protection and Weak Password Policy

**Status:** Confirmed

**Severity:** High

**Affected Functionality:** User authentication / Login

---

## Description

The application's authentication mechanism was found to lack adequate protection against repeated failed login attempts.

Testing also identified a weak password policy that allowed trivial passwords.

Together, these weaknesses can increase the risk of unauthorized account access through password guessing and brute-force attacks.

---

## Testing Methodology

1. The application's login functionality was identified.
2. Login requests were intercepted using Burp Suite.
3. Multiple failed authentication attempts were generated in the controlled laboratory environment.
4. The responses were examined for rate limiting, account lockout, CAPTCHA, or other brute-force protections.
5. The application's password policy was also examined.

---

## Observed Result

Repeated failed login attempts did not result in an observable rate-limiting or account-lockout mechanism.

A total of **110 failed login attempts** were tested during the assessment. The responses remained uniformly `401 Unauthorized`.

The password policy was also found to accept a trivial password such as:

```text
12345
