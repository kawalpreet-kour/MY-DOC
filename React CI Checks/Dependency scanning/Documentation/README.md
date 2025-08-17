# Documentation on React CI Checks – Dependancy Scanning
<img width="120" height="174" alt="download" src="https://github.com/user-attachments/assets/869b8250-6bc8-4720-8cdb-f9dda8949fa0" />
<img width="220" height="174" alt="download" src="https://github.com/user-attachments/assets/1a9c1057-d07f-4999-a714-a1719bcc286b" />



## Author Information

| Last Updated On | Version | Author           | Level           | Reviewer               |
|-----------------|---------|------------------|-----------------|------------------------|
| 17-08-2025      | V1.0    | Kawalpreet Kour  | Internal Review | Pritam                 |
|                 |         | Kawalpreet Kour  | L0              | Shreya/Sharvari        |
|                 |         | Kawalpreet Kour  | L1              | Abhishek V             |
|                 |         | Kawalpreet Kour  | L2              | Abhishek Dubey/Rishabh sharma |

---
<details>
  <summary><h2><strong>Table of Contents</strong></h2></summary>

- [Introduction](#introduction)  
- [What is Dependency Scanning?](#what-is-dependency-scanning)  
- [Why Dependency Scanning?](#why-dependency-scanning)  
- [Workflow Diagram](#workflow-diagram)  
- [Different Tools](#different-tools)  
- [Comparison](#comparison)  
- [Advantages](#advantages)  
- [Best Practices](#best-practices)  
- [Conclusion](#conclusion)  
- [FAQs](#faqs)  
- [References](#references)  

</details>


---

## Introduction

This document provides a guide to dependency scanning in React projects to track third-party npm packages and identify known security vulnerabilities.

---

## What is Dependency Scanning?

Dependency scanning involves checking all project dependencies against a database of known security vulnerabilities. The scanner identifies outdated, vulnerable, or risky packages that could compromise the application.
 

---

## Why Dependency Scanning?

| Benefit            | Description                                               |
|-------------------|-----------------------------------------------------------|
| Early detection    | Identifies vulnerabilities before production deployment. |
| Compliance         | Ensures the project meets security and organizational standards. |
| Risk reduction     | Prevents attacks exploiting vulnerable dependencies.    |
| Maintainability    | Keeps dependencies up-to-date and safe.                 |

---

## Workflow Diagram

```mermaid
flowchart LR
A[Code Commit] --> B[Clone Project Locally]
B --> C[Install Dependencies]
C --> D[Run Snyk Dependency Scan]
D --> E[Generate JSON Report]
E --> F[Convert to Readable Table]
F --> G[Review Vulnerabilities & Take Action]
```
---

## Different Tools

| Tool                     | Supported Languages                       | Notes                                    |
|---------------------------|------------------------------------------|------------------------------------------|
| Snyk                     | Go, Node.js, Java, Python, Ruby, PHP    | Popular tool with detailed reports       |
| Dependabot               | Multiple (GitHub projects)              | Automated updates and vulnerability alerts |
| OWASP Dependency-Check    | Java, .NET, Node.js                     | Open-source scanner for security testing |

---

## Comparison

| Feature                     | Snyk             | Dependabot        | OWASP Dependency-Check |
|------------------------------|-----------------|-----------------|-----------------------|
| Manual Scan                  | Yes             | No              | Yes                   |
| Report Output                | JSON/HTML       | Limited         | JSON                  |
| Multiple Language Support    | Yes             | Limited         | Limited               |
| Integration with CI/CD       | Yes             | Yes             | Yes                   |

---

## Advantages

| Advantage                        | Description                                              |
|---------------------------------|----------------------------------------------------------|
| Secure code                       | Helps maintain secure code by detecting vulnerable dependencies. |
| Multi-language support            | Supports multiple programming languages including Go.  |
| Detailed reports                  | Provides detailed reports for developers.              |
| CI/CD integration                 | Can be integrated into CI/CD pipelines or run manually. |

---

## Best Practices

| Practice                           | Description                                               |
|-----------------------------------|-----------------------------------------------------------|
| Update dependencies                | Regularly update dependencies to the latest safe versions. |
| Monitor vulnerabilities            | Monitor new vulnerabilities for existing packages.       |
| Use automated tools                 | Use automated tools for continuous scanning.            |
| Review reports                     | Format and review reports to prioritize critical vulnerabilities. |

---

## Conclusion

For React projects, Snyk is recommended for dependency scanning as it efficiently identifies vulnerabilities in npm packages and provides actionable remediation steps. It is easy to use and well-suited for React/Node.js projects.

---

## FAQs

1. **What is dependency scanning in React projects?**  
   - It is the process of checking all npm packages used in a React project for known security vulnerabilities.  

2. **Can dependency scanning also suggest fixes?**  
   - Yes, tools like Snyk provide actionable steps such as upgrading or patching vulnerable packages.  

3. **How often should dependency scanning be done?**  
   - Regularly, especially before production releases or after adding new dependencies.

---

## Contact Information

| Name             | Email                          |
|------------------|--------------------------------|
| Kawalpreet Kour  | kawalpreet.kour.snaatak@mygurukulam.co |

---
## References

| Description                               | Link                                                                 |
|-------------------------------------------|----------------------------------------------------------------------|
| React Official Documentation | [https://react.dev/learn/thinking-in-react](https://react.dev/learn/thinking-in-react) |
| Snyk CLI Documentation                     | https://docs.snyk.io/developer-tools/snyk-cli                       |
| Getting Started with Snyk CLI             | https://docs.snyk.io/developer-tools/snyk-cli/getting-started-with-the-snyk-cli |
