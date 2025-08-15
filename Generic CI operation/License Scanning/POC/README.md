# POC on Generic CI Operation – License Scanning


## Author Information

| Last Updated On | Version | Author           | Level           | Reviewer               |
|-----------------|---------|------------------|-----------------|------------------------|
| 15-08-2025      | V1.0    | Kawalpreet Kour  | Internal Review | Pritam                 |
|                 |         | Kawalpreet Kour  | L0              | Shreya/Sharvari        |
|                 |         | Kawalpreet Kour  | L1              | Abhishek V             |
|                 |         | Kawalpreet Kour  | L2              | Abhishek Dubey/Rishabh sharma |

---

## Table of Contents

1. [Purpose](#1-purpose)  
2. [Pre-Requisites](#2-pre-requisites)  
3. [System Requirements](#3-system-requirements)  
4. [Setup and Execution](#4-setup-and-execution)  
5. [Troubleshooting](#5-troubleshooting)  
6. [Best Practices](#6-best-practices)  
7. [FAQs](#7-faqs)  
8. [Contact Information](#8-contact-information)  
9. [References](#9-references)  

---

## 1. Purpose

This Proof of Concept (POC) demonstrates integrating **Snyk** for license scanning in a CI pipeline.  
The goal is to automatically detect restricted licenses in third-party dependencies during the build process and maintain compliance.

---

## 2. Pre-Requisites

- Node.js installed  
- npm installed  
- Snyk account and CLI installed  
- Git installed  
- Jenkins server (optional for CI integration)  

---

## 3. System Requirements

| **Hardware/Software** | **Minimum Requirement** |
|----------------------|-----------------------|
| Processor            | 1 CPU (t2.micro EC2)  |
| RAM                  | 1 GiB                 |
| Disk                 | 8 GB                  |
| OS                   | Ubuntu 22.04 LTS      |
| Node.js Version      | 16.x+                 |
| npm Version          | 8.x+                  |
| Snyk CLI             | Latest                |
| Git                  | Latest                |

---

## 4. Setup and Execution

### 1. Clone the sample project

```bash
git clone https://github.com/snyk-fixtures/npm-package.git
cd npm-package
```
### 2. Install dependencies
```bash
npm install
```

### 3. Install Snyk CLI
npm install -g snyk

### 4. Authenticate Snyk
snyk auth

### 5. Run a license scan
snyk test --all-projects --license

### 6. Generate JSON report
snyk test --all-projects --license --json > snyk-license-report.json

### 7. Integrate into CI Pipeline
- Add Snyk step in Jenkinsfile or YAML pipeline
- Trigger scan on every build
- Configure build to fail if restricted licenses are detected

### 8. Screenshots
**Clone Project**  
_Add screenshot here_

**Snyk License Scan Output**  
_Add screenshot here_

**Generated Report**  
_Add screenshot here_

---
### 5. Troubleshooting

| Issue                           | Solution                                                      |
|---------------------------------|---------------------------------------------------------------|
| snyk: command not found          | Ensure Snyk CLI is installed globally (`npm install -g snyk`) |
| Scan fails to detect licenses    | Verify project dependencies are installed (`npm install`)     |
| Authentication issues            | Run `snyk auth` again and verify account credentials          |

---
### 6. Best Practices
- Run scans in CI pipeline for every build
- Maintain an allowlist of approved licenses
- Fail the build for restricted licenses
- Keep Snyk CLI and project dependencies updated

---
### 7. FAQs
**Can Snyk scan private repositories?**  
Yes, with proper authentication and access rights.

**Does Snyk detect only license issues?**  
No, Snyk can also detect security vulnerabilities in dependencies.

**Can license scanning be automated in CI/CD?**  
Yes, by integrating Snyk into Jenkins, GitHub Actions, GitLab CI, etc.

