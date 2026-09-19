# A05:2025 — Injection

## Finding

**Vulnerability:** SQL Injection

**Status:** Confirmed

**Severity:** Critical

**Affected Functionality:** User authentication

**Endpoint:** `POST /rest/user/login`

---

## Description

The application's login functionality was found to be vulnerable to SQL Injection.

A crafted SQL expression was supplied through the email parameter of the login request. The application processed the manipulated input and returned a successful authentication response.

The test demonstrated that user-supplied input could alter the intended authentication query.

---

## Testing Methodology

1. The login functionality was identified during application testing.
2. The login request was intercepted using Burp Suite.
3. The `email` parameter was selected for controlled testing.
4. A SQL injection payload was inserted into the parameter.
5. The modified request was forwarded to the application.
6. The HTTP response and authentication information were examined.

### Test Payload

```text
' OR 1=1--
