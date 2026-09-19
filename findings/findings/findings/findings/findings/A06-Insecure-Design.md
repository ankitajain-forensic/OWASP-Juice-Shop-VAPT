# A06:2025 — Insecure Design

## Finding

**Vulnerability:** Weak Security-Question-Based Password Recovery

**Status:** Confirmed

**Severity:** High

**Affected Functionality:** Password recovery

---

## Description

The password recovery functionality was found to rely on knowledge-based security questions as an authentication factor.

The recovery mechanism did not provide an additional out-of-band verification mechanism. During the assessment, the security-question mechanism was also considered in combination with information exposed by the application's configuration functionality.

This design can weaken the overall security of the account recovery process.

---

## Testing Methodology

1. The application's password recovery functionality was identified.
2. The password recovery workflow was examined.
3. The security-question mechanism used during account recovery was reviewed.
4. The available verification factors were assessed.
5. The relationship between the recovery mechanism and information exposed elsewhere in the application was considered.

---

## Observed Result

The password recovery process relied on a security question as a knowledge-based verification mechanism.

No additional out-of-band verification mechanism was identified during the assessment.

The assessment also identified exposure of security-question metadata and answer values through an application endpoint, increasing the risk associated with the recovery design.

---

## Security Impact

A weak account recovery design may allow an attacker to compromise an account if the required security-question information becomes known.

Potential impacts include:

- Unauthorized account recovery
- Account compromise
- Loss of confidentiality
- Unauthorized access to user functionality
- Increased impact when combined with information-disclosure vulnerabilities

---

## Root Cause

The password recovery mechanism relied on a knowledge-based security question without sufficient additional verification.

The design did not provide adequate assurance that the person requesting account recovery was the legitimate account owner.

---

## Remediation

Recommended controls include:

1. Use stronger account recovery mechanisms.
2. Implement multi-factor or out-of-band verification where appropriate.
3. Avoid relying solely on knowledge-based security questions.
4. Do not expose security-question answers through application endpoints.
5. Apply appropriate authentication and authorization controls to recovery functionality.
6. Review account recovery workflows against realistic attack scenarios.

---

## Evidence

Evidence was collected during testing of the password recovery functionality.

Screenshots should be sanitized before publication.

Sensitive information, including security-question answers, authentication tokens, session identifiers, credentials, and personal information, must be removed or masked.

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
