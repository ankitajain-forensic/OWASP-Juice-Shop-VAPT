# A03:2025 — Software Supply Chain Failures

## Finding

**Vulnerability:** Known Vulnerabilities in Container Base Image Dependencies (OpenSSL, glibc)

**Status:** Confirmed

**Severity:** High

**Affected Functionality:** Application dependencies and externally sourced software components (Docker base image)

**Target Image:** `bkimminich/juice-shop:latest`

---

## Description

Software Supply Chain Failures refer to security weaknesses introduced through the software components, libraries, packages, dependencies, container images, or other third-party resources used by an application, rather than through the application's own source code.

The OWASP Juice Shop Docker image was scanned for known vulnerabilities in its underlying container base packages. The scan identified multiple vulnerable components, including outdated versions of `libssl3t64` (OpenSSL) and `libc6` (glibc), both of which are core system libraries inherited from the container's base OS layer rather than from the application's own `package.json` dependencies.

The presence of known vulnerabilities in these base-image packages demonstrates that software supply chain risk extends beyond application-level dependencies to the underlying container image itself.

---

## Testing Procedure

1. The OWASP Juice Shop application was deployed using its Docker image (`bkimminich/juice-shop:latest`) in the controlled laboratory environment.
2. A vulnerability scan was performed against the deployed Docker image to identify known vulnerabilities in its software components and base packages.
3. Scan results were reviewed to identify vulnerable libraries, their installed versions, associated CVE identifiers, and severity ratings.
4. Particular attention was given to core system libraries flagged with High or Medium severity findings.
5. Results were recorded as evidence where a vulnerable installed version and corresponding fixed version were both identified.

---

## Observation

The scan identified 30 vulnerabilities across the container's base packages, notably:

- **`libssl3t64` (OpenSSL)**, installed version `3.5.0-1-deb13u2`:
  - `CVE-2026-14458` (**High**) — Denial of Service via unbounded memory growth in the QUIC server when processing INITIAL packets. Fixed in `3.5.7-1-deb13u2`.
  - `CVE-2026-18798` (Medium) — QUIC server may trigger a double free when processing an INITIAL packet.
  - `CVE-2026-63072` (Medium) — Heap buffer overflow in CMS key unwrapping.
  - `CVE-2026-63076` — Invalid pointer dereference in the CMP server via a crafted protocol message.
  - `CVE-2026-14457` (Low) — RPK server signature algorithm selection with deference to a missing certificate.
- **`libc6` (glibc)**: Multiple buffer-overflow and denial-of-service vulnerabilities, including `CVE-2026-18374`, `CVE-2026-19499`, and `CVE-2026-19542`.

A fixed version of `libssl3t64` (`3.5.7-1-deb13u2`) was identified as available for the high-severity finding, confirming the installed version was outdated relative to the vendor's patched release.

---

## Security Impact

The presence of vulnerable third-party dependencies can introduce security risk into the application even when the vulnerability exists in an externally developed library rather than the application's own code.

An attacker may potentially exploit a known vulnerability in an affected dependency if the vulnerable functionality is reachable in the application's environment. In this assessment, the high-severity `libssl3t64` finding (`CVE-2026-14458`), combined with multiple glibc-level vulnerabilities, indicates the deployed container environment requires dependency updates and ongoing monitoring, and could affect the confidentiality, integrity, or availability of the application depending on successful exploitation.

---

## Root Cause

Inadequate management and monitoring of third-party software dependencies within the application's Docker base image. Vulnerable versions of core system libraries remained in the deployed image despite patched versions being publicly available, indicating that dependency security was not addressed as part of the image build/maintenance process.

---

## Remediation

1. Update the base image and vulnerable packages (`libssl3t64`, `libc6`) to their patched versions.
2. Maintain an up-to-date dependency and base-image inventory to track all third-party components.
3. Implement Software Composition Analysis (SCA) / container image scanning during build and deployment.
4. Monitor security advisories and CVEs affecting third-party and base-image components.
5. Establish a patching process that prioritizes remediation by severity and exploitability.
6. Rebuild and redeploy the Docker image after updates, and perform a follow-up scan to verify remediation.

---

## Evidence

Screenshots below show the vulnerability scan results identifying `libssl3t64` (`CVE-2026-14458`, High) and `libc6` as vulnerable, with associated CVE IDs, severity, and fixed versions. Sensitive values have been redacted prior to publishing.

![Vulnerability scan results identifying known vulnerabilities in container base packages](images/a03-01-scan-results-overview.jpg)`
`![Advisory detail for libssl3t64 and libc6 findings](images/a03-02-advisory-detail.jpg)`

---

## Environment

**Application:** OWASP Juice Shop

**Testing Environment:** Local authorized laboratory environment (Docker)

**Tools:** Kali Linux, Docker, container vulnerability scanner

**Assessment Type:** Web Application Vulnerability Assessment

---

## Disclaimer

This finding was identified in an intentionally vulnerable application within an authorized laboratory environment. The testing was performed for educational and security assessment purposes.
