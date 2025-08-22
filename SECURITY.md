# Security Policy for Project Citadel

## Introduction

The security of Project Citadel and the protection of user data is our highest priority. We value the contributions of security researchers and the community in helping us maintain a secure application. This document outlines the process for reporting security vulnerabilities.

We are committed to a process of responsible disclosure. We ask that all researchers practice responsible disclosure and report any potential vulnerabilities to us privately.

**Please do not report security vulnerabilities through public GitHub issues.**

---

## Supported Versions

Our security policy and updates apply only to the latest stable release of the project. Vulnerabilities will only be investigated against the most recent version available in the `main` branch.

| Version           | Supported          |
| ----------------- | ------------------ |
| Latest stable     | Yes                |
| `< 1.0` / alpha   | Not Supported      |

---

## Reporting a Vulnerability

To report a security vulnerability, please send a detailed email to: **saurabhmishra.24x@gmail.com**

To ensure we can address the issue efficiently, your report **must** include the following:

* **Description:** A clear and concise description of the vulnerability, its technical details, and its potential impact.
* **Reproduction Steps:** Detailed, step-by-step instructions required to reproduce the vulnerability. This is the most critical part of the report.
* **Proof-of-Concept (PoC):** A script, sample vault file, or other PoC that demonstrates the vulnerability.
* **Environment Details:** The operating system, Python version, and any other relevant environmental information.
* **Contact Information:** Your name or alias for public credit and a method for us to contact you during the remediation process.

---

## Reporting Process and Timeline

Upon receiving a security report, our team is committed to the following process:

1.  **Acknowledge Receipt:** We will acknowledge receipt of your report within 48 hours.
2.  **Initial Triage:** We will perform an initial analysis to confirm the vulnerability and determine its severity. You will be updated on the status of this triage.
3.  **Remediation:** Our team will develop and test a patch to address the vulnerability.
4.  **Coordinated Disclosure:** We will work with you to coordinate a public announcement of the vulnerability after a fix has been released.
5.  **Attribution:** We will publicly credit you for the discovery in the project's release notes and relevant documentation, unless you request to remain anonymous.

---

## Scope of Vulnerabilities

### In Scope

Any reproducible vulnerability that has a direct security impact on the application's core logic, cryptographic implementation, or data handling is considered in scope. This includes, but is not limited to:

* Remote Code Execution (RCE)
* Cryptographic flaws leading to data exposure
* Authentication or authorization bypass
* Data integrity violations

### Out of Scope

The following are generally considered out of scope for our security policy:

* Vulnerabilities in third-party dependencies (these should be reported to the respective project maintainers).
* Attacks requiring physical access to an unlocked device or session.
* Attacks requiring the user's master password.
* Attacks requiring the application to be run on a compromised operating system (e.g., with a keylogger or malware installed).
* Social engineering and phishing attacks.

---

## Compensation and Bug Bounties

At this time, Project Citadel does not have a formal bug bounty program or offer monetary compensation for vulnerability reports. However, we are immensely grateful for all security contributions and will provide public attribution to researchers who report valid issues.

Thank you for helping to keep Project Citadel secure.
