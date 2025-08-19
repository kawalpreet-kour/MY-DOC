
# POC on Python CI Bug Analysis – attendance-api & notification-worker

<img width="262" height="181" alt="python-bug analysis-logo" src="https://github.com/user-attachments/assets/9bb2f33e-d132-4f82-94de-85a6ed1fcfbf" />

---

## Author Information

| Last Updated On | Version | Author           | Level           | Reviewer               |
|-----------------|---------|-----------------|----------------|-----------------------|
| 20-08-2025      | V1.0    | Kawalpreet Kour | Internal Review | Pritam                |
|                 |         | Kawalpreet Kour | L0             | Shreya/Sharvari       |
|                 |         | Kawalpreet Kour | L1             | Abhishek V            |
|                 |         | Kawalpreet Kour | L2             | Abhishek Dubey/Rishabh Sharma |

---

<details>
  <summary><h2><strong>Table of Contents</strong></h2></summary>

- [Purpose](#purpose)
- [Pre-Requisites](#pre-requisites)
- [System Requirements](#system-requirements)
- [Setup and Execution](#setup-and-execution)
- [Troubleshooting](#troubleshooting)
- [Best Practices](#best-practices)
- [Contact Information](#contact-information)
- [References](#references)

</details>

---

## Purpose

This POC demonstrates using **SonarQube** and **pytest** to perform Python CI Bug Analysis for:

- `attendance-api`
- `notification-worker`

It ensures code quality, detects runtime bugs, security vulnerabilities, and enforces coding standards before integration.

---

## Pre-Requisites

| Requirement                 | Description                                        |
|-----------------------------|---------------------------------------------------|
| Git installed               | Required to clone and access the repository      |
| Python ≥ 3.8 & pip ≥ 21     | Required to run Python tests and coverage        |
| Pytest ≥ 7.0 & pytest-cov ≥ 3.0 | For automated testing & coverage reports      |
| SonarQube v10+ & SonarScanner | For static analysis and dashboard reporting     |
| SonarQube Token             | For authentication with SonarScanner             |
| Access to Git repositories  | `attendance-api` & `notification-worker`         |

---

## System Requirements

| Hardware/Software           | Minimum Requirement                   |
|-----------------------------|--------------------------------------|
| Processor                   | 2 CPU cores                           |
| RAM                         | 4 GiB                                  |
| Disk                        | 10 GB                                  |
| OS                          | Ubuntu 22.04 LTS / Windows 10+ / macOS 11+ |
| Python Version              | 3.8+                                   |
| SonarScanner Version        | Latest compatible                      |

---

## Setup and Execution

### Clone the Repositories
```bash
git clone https://github.com/OT-MICROSERVICES/attendance-api.git
git clone https://github.com/OT-MICROSERVICES/notification-worker.git
