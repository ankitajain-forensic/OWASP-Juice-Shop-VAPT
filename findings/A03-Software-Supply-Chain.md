# A03:2025 — Software Supply Chain Failures

## Finding

**Vulnerability:** Vulnerable Third-Party Dependencies

**Status:** Confirmed

**Severity:** High

**Affected Component:** Application dependencies

---

## Description

A dependency assessment of the OWASP Juice Shop environment identified third-party software components with known security vulnerabilities.

The dependency assessment identified vulnerabilities associated with installed package versions, demonstrating the security risk that can arise from using vulnerable third-party components within an application environment.

---

## Testing Methodology

1. The application environment and its dependencies were assessed.
2. Installed package versions were identified.
3. Dependency information was compared against known vulnerability information using vulnerability scanning.
4. Identified vulnerable components and their associated CVEs were documented.
5. The potential security impact of the vulnerable dependencies was assessed.

---

## Observed Result

The assessment identified vulnerabilities affecting third-party components.

The report identified:

- **CVE-2026-41907** affecting `libssl3t64`
- **CVE-2024-37890** affecting `libc6`

The installed versions identified during the assessment were:

| Component | Installed Version | Associated CVE |
|---|---:|---|
| `libssl3t64` | 8.3.2 | CVE-2026-41907 |
| `libc6` | 7.4.6 | CVE-2024-37890 |

Newer fixed versions were identified by the vulnerability assessment process.

---

## Security Impact

Vulnerable third-party components can introduce security weaknesses into an otherwise secure application.

Depending on the vulnerability, exploitation may result in:

- Unauthorized access
- Information disclosure
- Application compromise
- Increased attack surface
- Compromise through a vulnerable dependency rather than directly through application code

---

## Root Cause

The identified software components contained known vulnerabilities that had not been sufficiently addressed through dependency management and update processes.

---

## Remediation

Recommended controls include:

1. Maintain an inventory of application dependencies.
2. Regularly scan dependencies for known vulnerabilities.
3. Update vulnerable packages to appropriate fixed versions.
4. Remove unnecessary dependencies.
5. Monitor security advisories and CVE databases.
6. Integrate dependency scanning into the software development lifecycle.
7. Establish a process for timely security updates and patch management.

---

## Evidence

Dependency and vulnerability assessment results were collected during the assessment.

Any screenshots or exported scanner results should be reviewed and sanitized before public publication.

**Evidence status:** To be added after sanitization.

---

## Environment

**Application:** OWASP Juice Shop

**Testing Environment:** Local authorized laboratory environment

**Tools:** Kali Linux, vulnerability assessment tools

**Assessment Type:** Web Application Vulnerability Assessment

---

## Disclaimer

This finding was identified in an intentionally vulnerable application within an authorized laboratory environment. The testing was performed for educational and security assessment purposes.
