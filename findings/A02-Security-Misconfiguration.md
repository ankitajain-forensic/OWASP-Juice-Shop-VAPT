# A02:2025 — Security Misconfiguration

## Finding

**Vulnerability:** Exposure of Application Configuration and Security-Sensitive Information

**Status:** Confirmed

**Severity:** High

**Affected Functionality:** Application configuration endpoint

---

## Description

The application was found to expose detailed configuration information through an accessible application endpoint.

During testing, the endpoint returned JSON containing security-sensitive application information, including security-question metadata and associated answer values.

The exposure of such information can provide an attacker with information that should not be publicly accessible and may also support further attacks against application functionality.

---

## Testing Methodology

1. The application was explored to identify accessible endpoints and exposed functionality.
2. Requests were intercepted and examined using Burp Suite.
3. Accessible application endpoints were tested for unintended information disclosure.
4. The identified configuration-related endpoint was requested.
5. The response was examined for sensitive configuration and security-related information.

---

## Observed Result

The application returned detailed JSON containing security-question metadata and answer values.

The information was accessible through the application without adequate protection.

This demonstrated that security-sensitive configuration information was exposed to an unauthorized client.

---

## Security Impact

Exposure of configuration and security-related information may:

- Reveal information useful for further attacks
- Expose security-question information
- Reduce the effectiveness of application security controls
- Support account compromise when exposed information is used with vulnerable recovery mechanisms
- Disclose internal application information that should remain protected

---

## Root Cause

Sensitive configuration and security-related information was exposed through an accessible application endpoint without sufficient access control or information filtering.

Security-sensitive information should not be returned to an unauthorized client when it is not required for normal application functionality.

---

## Remediation

Recommended controls include:

1. Restrict access to configuration and administrative endpoints.
2. Prevent sensitive configuration data from being exposed to clients.
3. Remove security-question answers and other sensitive values from API responses.
4. Apply appropriate authentication and authorization controls.
5. Review API responses for unnecessary sensitive information disclosure.
6. Follow secure configuration practices throughout the application.

---

## Evidence

Evidence was collected during testing using Burp Suite.

Screenshots should be sanitized before publication.

Sensitive information such as authentication tokens, session identifiers, personal information, credentials, and other confidential values must be removed or masked.

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
