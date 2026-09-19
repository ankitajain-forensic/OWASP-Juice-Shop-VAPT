# A09:2025 — Security Logging and Alerting Failures

## Finding

**Vulnerability:** Insufficient Observable Security Logging and Alerting

**Status:** Confirmed

**Severity:** Medium

**Assessment Type:** Black-box Web Application Assessment

---

## Description

The application did not provide observable indications of security monitoring or alerting when several suspicious or malicious activities were performed during the assessment.

Because the assessment was conducted as a black-box test, server-side logs could not be directly inspected. Therefore, the finding is based on application-observable behaviour during controlled testing.

---

## Testing Methodology

The following activities were performed in the authorized laboratory environment:

1. SQL Injection testing against the login functionality.
2. Repeated failed authentication attempts.
3. Malformed input testing against the basket endpoint.
4. Application responses were monitored for observable security alerts, warnings, or other indications of detection.
5. The consistency of responses was examined to determine whether suspicious activity produced any observable security indication.

---

## Observed Result

During the assessment, suspicious activity did not produce an observable client-side indication of security detection or alerting.

For example:

- SQL Injection authentication-bypass testing did not produce an observable security alert.
- **110 failed login attempts** were performed, with the responses remaining uniformly `401 Unauthorized`.
- A malformed basket identifier such as `abc` produced an HTTP `200` response with:

```json
{"status":"success","data":null}
