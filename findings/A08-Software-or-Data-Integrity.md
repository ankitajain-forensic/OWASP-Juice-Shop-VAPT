# A08:2025 — Software or Data Integrity Failures

## Finding

**Vulnerability:** Client-Controlled Coupon/Discount Data

**Status:** Confirmed

**Severity:** Medium

**Affected Functionality:** Checkout

**Endpoint:** `POST /rest/basket/{id}/checkout`

---

## Description

The checkout functionality was found to accept client-controlled coupon or discount-related data without sufficient server-side integrity verification.

During testing, the request was intercepted using Burp Suite and the client-supplied `couponData` field was modified.

The modified request was accepted by the application, demonstrating insufficient server-side validation of client-controlled data.

---

## Testing Methodology

1. The checkout functionality was identified.
2. The checkout request was intercepted using Burp Suite.
3. The request body was examined to identify client-controlled parameters.
4. The `couponData` field was modified using Burp Repeater.
5. The modified request was forwarded to the application.
6. The server response and resulting order status were examined.

---

## Observed Result

The modified `couponData` value was accepted by the application.

The server returned a successful order confirmation despite the client-side modification.

This demonstrated that the application did not adequately verify the integrity and validity of the coupon-related data on the server side.

---

## Security Impact

Insufficient server-side integrity validation may allow users to manipulate client-controlled data and potentially influence application behaviour.

Potential impacts include:

- Unauthorized discounts
- Financial loss
- Manipulation of transaction-related information
- Circumvention of business rules
- Abuse of application functionality

---

## Root Cause

The application relied on client-supplied coupon or discount information without sufficient server-side verification.

Security-sensitive business logic should not depend solely on values supplied by the client.

---

## Remediation

Recommended controls include:

1. Perform all security-sensitive validation on the server.
2. Never trust client-controlled coupon or discount values.
3. Recalculate discounts server-side.
4. Verify coupon validity, ownership, expiration, and applicable conditions.
5. Ensure transaction-related values cannot be arbitrarily modified by the client.
6. Apply integrity checks to security-sensitive application data.

---

## Evidence

Evidence was collected using Burp Suite and Burp Repeater.

Before publishing screenshots, remove or mask:

- Session identifiers
- Authentication tokens
- Cookies
- Personal information
- Other sensitive application data

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
