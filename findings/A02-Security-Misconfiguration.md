# A02:2025 — Security Misconfiguration

## Finding

**Vulnerability:** Exposure of Application Configuration and Security-Sensitive Information

**Status:** Confirmed

**Severity:** High

**Affected Functionality:** Application Configuration

**Endpoint:** `GET /rest/admin/application-configuration`

---

## Description

The application exposed an administrative configuration endpoint that returned extensive internal application details in its response, without requiring proper authorization.

The response included configuration data beyond what should be accessible to a standard or unauthenticated user, including information relevant to the account-recovery process.

---

## Testing Methodology

1. The application's endpoints were reviewed for administrative or configuration-related routes.
2. The `/rest/admin/application-configuration` endpoint was identified and accessed using Burp Suite.
3. The request was sent without elevated privileges to determine whether the endpoint properly restricted access.
4. The response body was reviewed for sensitive or security-relevant data.

---

## Observed Result

The endpoint returned a large amount of application configuration data, including security-question answers used in the password recovery process.

This confirmed that the endpoint did not adequately restrict access to configuration data that should be treated as sensitive.

---

## Security Impact

Exposure of application configuration data can assist an attacker in planning further attacks and may directly undermine other security controls.

In this case, the disclosed security-question answers directly weaken the account-recovery mechanism (see A06:2025), since an attacker with access to this endpoint could use the disclosed answers to bypass password recovery for affected accounts.

---

## Root Cause

The configuration endpoint did not enforce appropriate server-side authorization controls, and the application returned more configuration detail in the response than was necessary or safe to expose.

---

## Remediation

Recommended controls include:

1. Restrict access to configuration endpoints using appropriate server-side authorization checks.
2. Return only the minimum configuration data required for legitimate client functionality.
3. Remove security-question answers and other sensitive values from API responses entirely.
4. Apply authentication and role-based access control to administrative and configuration routes.
5. Review all API responses for unnecessary disclosure of internal or security-relevant information.
6. Follow a secure-by-default configuration approach, disabling verbose or debug-level responses in production.

---

## Evidence

Screenshots below show the request to the configuration endpoint and the response containing the exposed security-question data. Sensitive values have been redacted prior to publishing.

*[Add screenshots here, e.g.:]*
`![Request to the application configuration endpoint](images/a02-01-request-config-endpoint.jpg)`
`![Response exposing security-question data](images/a02-02-response-exposed-config-data.jpg.jpg)`

---

## Environment

**Application:** OWASP Juice Shop

**Testing Environment:** Local authorized laboratory environment

**Tools:** Kali Linux, Burp Suite, Firefox/Burp Suite Browser

**Assessment Type:** Web Application Vulnerability Assessment

---

## Disclaimer

This finding was identified in an intentionally vulnerable application within an authorized laboratory environment. The testing was performed for educational and security assessment purposes.
