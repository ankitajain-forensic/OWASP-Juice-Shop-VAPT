# A09:2025 — Security Logging and Alerting Failures

## Finding

**Vulnerability:** Absence of Observable Security Logging and Alerting for Anomalous and Malicious Activity

**Status:** Confirmed

**Severity:** Medium

**Affected Functionality:** Application-wide — Authentication and Basket API

---

## Description

The application did not provide observable indications that anomalous or malicious activity was being detected, flagged, or triggering a defensive response.

Because this assessment was conducted as a black-box assessment, server-side log files could not be directly inspected. Therefore, this finding is based on observable application behaviour during controlled testing.

Three activities were examined:

- SQL Injection authentication bypass
- Repeated brute-force login attempts
- Malformed basket-ID input

---

## Testing Methodology

### 1. SQL Injection

The SQL Injection authentication bypass documented under A05 was reviewed for any observable indication of detection or defensive response, such as:

- Session termination
- Account flagging
- Security warning
- Alert or other defensive response

### 2. Brute-Force Login Attempts

The login endpoint was tested using **110 requests through Burp Intruder**.

The application responses were examined for changes in behaviour that could indicate detection or defensive action.

### 3. Malformed Basket Identifier

A malformed request was submitted to the basket API:

    GET /rest/basket/abc

The response was examined to determine whether the invalid input was flagged, rejected, or handled differently from a normal request.

---

## Observed Result

### SQL Injection

The SQL Injection authentication bypass using:

    ' OR 1=1--

successfully returned a valid authentication token.

No observable client-side indication showed that the request had been detected, blocked, or treated as anomalous.

### Brute-Force Attempts

Across **110 submitted login attempts**, every response remained:

    HTTP 401 Unauthorized

The response behaviour remained consistent throughout the attack.

No observable CAPTCHA challenge, rate-limit response, account-lockout message, or other defensive response was triggered.

### Malformed Basket Request

The request:

    GET /rest/basket/abc

returned:

    HTTP 200 OK

with the response:

    {"status":"success","data":null}

The malformed input therefore produced a success-like response rather than an explicit error or observable indication that the request was anomalous.

### Overall Observation

Across all three test cases, there was no client-observable evidence such as:

- Security warning
- Changed response pattern
- CAPTCHA challenge
- Session termination
- Account flagging
- Security notice

indicating that the activity had been detected or had triggered a meaningful defensive response.

---

## Security Impact

Insufficient logging and alerting can allow security-relevant activity to occur without timely detection.

Potential impacts include:

- Increased attacker dwell time
- Delayed incident response
- Reduced visibility into attack activity
- Difficulty identifying attack patterns
- Reduced forensic investigation capability
- Increased opportunity for an attacker to continue malicious activity undetected

---

## Root Cause

The probable root cause is the absence of, or inadequate configuration of, security-event logging and alerting mechanisms for:

- Authentication failures
- Injection attempts
- Malformed or anomalous requests

The application did not appear to differentiate suspicious activity from normal application behaviour through observable defensive responses.

---

## Remediation

Recommended controls include:

1. Implement logging for security-relevant events, including failed login attempts, unusual authentication patterns, injection attempts, and malformed requests.
2. Configure alerting thresholds for repeated failed logins and suspected injection activity.
3. Integrate application logs with a centralized logging or SIEM solution.
4. Log malformed or unexpected input and reject it with an appropriate error response where applicable.
5. Periodically test logging and alerting mechanisms using controlled attack scenarios.
6. Ensure logs contain sufficient contextual information such as timestamp, source, endpoint, user identifier, and result.
7. Avoid logging sensitive information such as passwords, authentication tokens, or other confidential data.

---

## Evidence

Evidence was collected through observable application behaviour during controlled testing.

Evidence includes:

- SQL Injection authentication-bypass behaviour
- 110 Burp Intruder login attempts
- Malformed basket-ID request
- HTTP response behaviour observed during testing

Screenshots should be sanitized before public documentation.

**Evidence status:** To be added after sanitization.

---

## Assessment Limitation

The assessment was performed as a black-box test and did not provide direct access to server-side log files.

Therefore, the finding establishes the absence of **client-observable detection or defensive response** during testing. It does not independently prove that no server-side logs were generated.

---

## Environment

**Application:** OWASP Juice Shop

**Testing Environment:** Local authorized laboratory environment

**Tools:** Kali Linux, Burp Suite, Firefox/Burp Suite Browser

**Assessment Type:** Black-box Web Application Vulnerability Assessment

---

## Disclaimer

This finding was identified in an intentionally vulnerable application within an authorized laboratory environment. The testing was performed for educational and security assessment purposes.
