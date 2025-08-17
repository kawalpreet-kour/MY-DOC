
# POC on React CI Checks – Dependency Scanning



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

This Proof of Concept (POC) demonstrates dependency scanning of a React project using Snyk CLI. It analyzes project dependencies for known vulnerabilities and generates reports to maintain secure and compliant code in the CI pipeline.  

---

## Pre-Requisites 

| Requirement                     | Description                                   |
|--------------------------------|-----------------------------------------------|
| Git installed                  | Required to clone and access the repository  |
| Go installed                  | Required to build and manage dependencies    |
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
| React Version     | 18+              |

---
## Setup and Execution


### Clone the Repo
```bash
git clone https://github.com/OT-MICROSERVICES/frontend.git
```
<img width="640" height="114" alt="Screenshot from 2025-08-17 16-10-19" src="https://github.com/user-attachments/assets/cb6171e4-5959-4fa2-98f3-9454a37ef621" />


```bash
cd frontend
```


 > Clones the repository locally and navigates into the project directory.

### Install Prerequisites

>Updates package lists and upgrades installed packages.

### Install Node.js
```bash
sudo apt install -y nodejs
```
<img width="796" height="368" alt="Screenshot from 2025-08-17 16-17-30" src="https://github.com/user-attachments/assets/fc6baa82-687c-4c73-8dab-34242afa990a" />

```bash
node -v
```



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

### Install Project Dependencies

```bash
npm install
```

### Run Dependency Scan
```bash
snyk test --json > snyk-dependency-report.json
```

> Scans project dependencies for vulnerabilities and saves the JSON report.

### Convert Dependency Report to Readable Table
```bash
cat snyk-dependency-report.json | jq -r '
  ["Package", "Version", "Severity", "Direct Dependency"],
  (.vulnerabilities[] | [
    .packageName, 
    .version, 
    .severity, 
    (if (.from | type=="array") then .from[0:2] | join(" > ") else .from end)
  ]) | @tsv
'
```


>Formats the dependency vulnerability report into a readable table showing Package, Version, Severity, and Direct Dependency.

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
| Fail build on restricted licenses| Stop build if restricted licenses detected |
| Keep tools updated       | Update Snyk CLI and dependencies regularly |

---

## FAQs

1. **Which package manager is used in this project?**  
   Go modules (gomod).

2. **Which package managers are supported?**  
  `snyk test --json > snyk-dependency-report.json`

3. **How do I view the scan results?**  
   Format the JSON report using `jq` to get a readable table.

---

## Contact Information

| Name             | Email                          |
|------------------|--------------------------------|
| Kawalpreet Kour  | kawalpreet.kour.snaatak@mygurukulam.co |

---
## References

| Description                               | Link                                                                 |
|-------------------------------------------|----------------------------------------------------------------------|
| Go Programming Language Official Website  | [https://go.dev/](https://go.dev/)                                   |
| Snyk CLI Documentation                     | https://docs.snyk.io/developer-tools/snyk-cli                       |
| Getting Started with Snyk CLI             | https://docs.snyk.io/developer-tools/snyk-cli/getting-started-with-the-snyk-cli |

