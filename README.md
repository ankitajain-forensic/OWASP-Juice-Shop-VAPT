# OWASP Juice Shop — Web Application VAPT

A practical web application security assessment of OWASP Juice Shop conducted in a controlled laboratory environment.

## Objective

The objective of this project was to identify, validate, document, and assess common web application security vulnerabilities using the OWASP Top 10 as a reference framework.

The assessment focused on understanding how vulnerabilities can be discovered, reproduced in a controlled environment, and documented with appropriate remediation recommendations.

## Lab Environment

- Target: OWASP Juice Shop
- Operating System: Kali Linux
- Deployment: Docker
- Testing Tools: Burp Suite, Nmap, Browser Developer Tools
- Environment: Controlled local laboratory

## Methodology

The assessment followed a structured vulnerability assessment workflow:

1. Application reconnaissance
2. Endpoint and functionality identification
3. Request and response analysis
4. Manual security testing
5. Vulnerability validation
6. Evidence collection
7. Severity assessment
8. Remediation recommendations

## Vulnerabilities Investigated

The assessment included vulnerabilities and security weaknesses related to:

- Broken Access Control
- Injection
- Authentication Failures
- Security Misconfiguration
- Cryptographic Failures
- Insecure Design
- Software or Data Integrity Failures
- Software Supply Chain Failures
- Security Logging and Alerting Failures
- Mishandling of Exceptional Conditions

## Tools Used

| Tool | Purpose |
|---|---|
| Burp Suite | HTTP request interception and web application testing |
| Nmap | Network and service reconnaissance |
| Kali Linux | Security testing environment |
| Docker | Local deployment of the vulnerable application |
| Browser Developer Tools | Client-side and application analysis |

## Findings

This assessment identified 10 confirmed vulnerabilities, one mapped to each OWASP Top 10:2025 category.
Each finding below links to its full write-up, including testing methodology, evidence, and remediation guidance.

| # | OWASP Category | Finding | Severity | Status | Report |
|---|---|---|---|---|---|
| A01 | Broken Access Control | Insecure Direct Object Reference (IDOR) | High | Confirmed | [View](findings/A01-Broken-Access-Control.md) |
| A02 | Security Misconfiguration | Exposure of application configuration and security-sensitive information | High | Confirmed | [View](findings/A02-Security-Misconfiguration.md) |
| A03 | Software Supply Chain Failures | Known vulnerabilities in container base image dependencies (OpenSSL, glibc) | High | Confirmed | [View](findings/A03-Software-Supply-Chain-Failures.md) |
| A04 | Cryptographic Failures | Authentication data transmitted over unencrypted HTTP | Medium | Confirmed | [View](findings/A04-Cryptographic-Failures.md) |
| A05 | Injection | SQL Injection in user authentication | Critical | Confirmed | [View](findings/A05-Injection.md) |
| A06 | Insecure Design | Insecure design of password recovery mechanism | High | Confirmed | [View](findings/A06-Insecure-Design.md) |
| A07 | Authentication Failures | No brute-force protection and weak password policy | High | Confirmed | [View](findings/A07-Authentication-Failures.md) |
| A08 | Software or Data Integrity Failures | Client-controlled coupon data accepted without integrity verification | Medium | Confirmed | [View](findings/A08-Software-or-Data-Integrity-Failures.md) |
| A09 | Security Logging and Alerting Failures | No observable detection or alerting for malicious activity | Medium | Confirmed | [View](findings/A09-Security-Logging-and-Alerting-Failures.md) |
| A10 | Mishandling of Exceptional Conditions | Fail-open behavior on malformed basket identifier | Low | Confirmed | [View](findings/A10-Mishandling-of-Exceptional-Conditions.md) |

## Evidence & Remediation

Evidence and remediation guidance for each finding are documented individually in the linked reports above. All screenshots have been reviewed and redacted to remove session tokens, cookies, credentials, and other sensitive values prior to publishing.

## Limitations

This assessment was performed against an intentionally vulnerable application in a controlled laboratory environment. Findings should not be interpreted as evidence of vulnerabilities in unrelated production systems.

## Disclaimer

This project was conducted for educational and cybersecurity learning purposes against an intentionally vulnerable application in a controlled environment.

No unauthorised systems were targeted.

## Status

**Completed Lab Project — Documentation in Progress**
