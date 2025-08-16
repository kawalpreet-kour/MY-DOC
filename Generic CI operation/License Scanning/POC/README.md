# POC on Snyk – License Scanning

<img width="210" height="169" alt="download" src="https://github.com/user-attachments/assets/9261c208-056b-4d32-af65-70bd88229b51" />

---
## Author Information

| Last Updated On | Version | Author           | Level           | Reviewer               |
|-----------------|---------|------------------|-----------------|------------------------|
| 16-08-2025      | V1.0    | Kawalpreet Kour  | Internal Review | Pritam                 |
|                 |         | Kawalpreet Kour  | L0              | Shreya/Sharvari        |
|                 |         | Kawalpreet Kour  | L1              | Abhishek V             |
|                 |         | Kawalpreet Kour  | L2              | Abhishek Dubey/Rishabh sharma |

---
<details>
  <summary><h2><strong>Table of Contents</strong></h2></summary>

1. [Purpose](#purpose)
2. [Pre-Requisites](#pre-requisites)
3. [System Requirements](#system-requirements)
4. [Setup and Execution](#setup-and-execution)
5. [Troubleshooting](#troubleshooting)
6. [Best Practices](#best-practices)
7. [FAQs](#faqs)
8. [Contact Information](#contact-information)
9. [References](#references)

</details>

---

## Purpose

This Proof of Concept (POC) demonstrates using Snyk to perform license scanning for a GoLang project. It aims to automatically check project dependencies for restricted or prohibited licenses during the CI process and generate a readable report, helping teams maintain license compliance efficiently.

---

## Pre-Requisite 

| Requirement                     | Description                                   |
|--------------------------------|-----------------------------------------------|
| Git installed                  | Required to clone and access the repository  |
| Node.js and npm installed      | Needed to run Snyk CLI                        |
| Access to the Git repository   | To scan the project dependencies             |
| Snyk account with auth token   | For authenticating and running Snyk scans    |


---

## System Requirements

| Hardware/Software | Minimum Requirement |
|------------------|-------------------|
| Processor        | 1 CPU (t2.micro EC2) |
| RAM              | 1 GiB             |
| Disk             | 8 GB              |
| OS               | Ubuntu 22.04 LTS  |
| Node.js Version  | 18.x+             |
| NPM Version      | 9.x+              |
| Snyk CLI Version | latest            |
| Go Version       | 1.20+             |

---
## Setup and Execution


### Clone the Repo
```bash
git clone https://github.com/OT-MICROSERVICES/employee-api.git
```
<img width="743" height="157" alt="Screenshot from 2025-08-16 14-21-02" src="https://github.com/user-attachments/assets/a9a89f71-c91d-4581-9f84-31b41940bcd2" />

```bash
cd employee-api
```
<img width="512" height="421" alt="Screenshot from 2025-08-16 14-22-44" src="https://github.com/user-attachments/assets/a897cf93-98e6-4e94-acbb-97c1d254510a" />

 > Clones the repository locally and navigates into the project directory.

### Install Prerequisites

>Updates package lists and upgrades installed packages.

### Install Go programming language
```bash
sudo apt install -y golang-go
```
<img width="531" height="31" alt="image" src="https://github.com/user-attachments/assets/db026c8b-0619-4a26-b988-ddf667b15df6" />

```bash
go version
```
<img width="466" height="71" alt="Screenshot from 2025-08-16 14-43-02" src="https://github.com/user-attachments/assets/5e141e43-e83c-4276-b62c-5349e2da09d1" />


### Install Node.js
```bash
sudo apt install -y nodejs
```
<img width="519" height="26" alt="image" src="https://github.com/user-attachments/assets/d4f785be-3a92-4595-97e3-699d268885e9" />

```bash
node -v
```
<img width="354" height="30" alt="image" src="https://github.com/user-attachments/assets/b6238d9c-4854-4310-aa66-5fd6c7e8a31d" />


### Install npm (Node.js package manager)
```bash
sudo apt install -y npm
```
<img width="519" height="26" alt="image" src="https://github.com/user-attachments/assets/88b53bfa-bd77-4575-8bd8-60184e5a369e" />

```bash
npm -v
```
<img width="354" height="30" alt="image" src="https://github.com/user-attachments/assets/77db80d7-46ca-49a3-9e96-8635052dc761" />

> Installs Node.js, npm, and Go .

### Install Snyk CLI globally
```bash
sudo npm install -g snyk
```
<img width="1290" height="272" alt="Screenshot from 2025-08-16 14-32-28" src="https://github.com/user-attachments/assets/a7d02888-a576-4f21-aedc-2af94adcf390" />

>Installs Snyk CLI globally using npm.

### Authenticate Snyk
```bash
snyk auth <your-snyk-auth-token>
```
<img width="618" height="87" alt="Screenshot from 2025-08-16 14-39-18" src="https://github.com/user-attachments/assets/e2e0da81-3d62-4202-87d9-c8398ecad331" />

>Authenticates your Snyk account to allow scanning of projects.

### Run License Scan
```bash
snyk test --license
```
<img width="1264" height="363" alt="Screenshot from 2025-08-16 19-51-16" src="https://github.com/user-attachments/assets/d3630df3-e456-4053-b18a-b93252adc904" />

>Generates a JSON report containing license policy details only.


### Convert License Policy to Readable Table
```bash
cat snyk-license-report.json | jq -r '
  ["License", "Severity", "Instructions"],
  (.licensesPolicy.orgLicenseRules | to_entries[] | [.value.licenseType, .value.severity, .value.instructions])
  | @tsv
'
```
<img width="814" height="342" alt="image" src="https://github.com/user-attachments/assets/416f0506-a72d-45ab-b2a7-44fe47cafa96" />

>Converts the JSON license report into a readable tabular format with columns: License, Severity, and Instructions.

---

## Troubleshooting

| Issue                           | Solution                                                      |
|---------------------------------|---------------------------------------------------------------|
| snyk: command not found          | Ensure Snyk CLI is installed globally (`npm install -g snyk`) |
| Scan fails to detect licenses    | Verify project dependencies are installed (`npm install`)     |
| Authentication issues            | Run `snyk auth` again and verify account credentials          |

---
## Best Practices

| Practice                 | Description                                |
|--------------------------|--------------------------------------------|
| Allowlist                | Maintain approved licenses list            |
| Fail build on restricted | Stop build if restricted licenses detected |
| Keep tools updated       | Update Snyk CLI and dependencies regularly |

---

## FAQs

1. **Can Snyk scan licenses without scanning vulnerabilities?**  
   Yes, use the `--license` flag to focus only on license compliance.

2. **Which package managers are supported?**  
   Snyk supports npm, Node.js, Go (gomodules), Python (pip), Java (Maven/Gradle), and more.

3. **How can I update the license rules or severities?**  
   Update your `licensesPolicy` in Snyk settings or configure a custom policy file for the project.

---

## Contact Information

| Name             | Email                          |
|------------------|--------------------------------|
| Kawalpreet Kour  | kawalpreet.kour.snaatak@mygurukulam.co |

---
## References

| Description                               | Link                                                                 |
|-------------------------------------------|----------------------------------------------------------------------|
| Snyk CLI Documentation                     | https://docs.snyk.io/developer-tools/snyk-cli  
| Getting Started with Snyk CLI             | https://docs.snyk.io/developer-tools/snyk-cli/getting-started-with-the-snyk-cli |

