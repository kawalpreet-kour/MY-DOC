
# POC on React CI Checks – Dependency Scanning
<img width="120" height="174" alt="download" src="https://github.com/user-attachments/assets/869b8250-6bc8-4720-8cdb-f9dda8949fa0" />
<img width="220" height="174" alt="download" src="https://github.com/user-attachments/assets/1a9c1057-d07f-4999-a714-a1719bcc286b" />

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
<img width="476" height="25" alt="image" src="https://github.com/user-attachments/assets/bf6e6961-322e-4027-8f0a-15fdda18d761" />


```bash
npm -v
```
<img width="331" height="36" alt="image" src="https://github.com/user-attachments/assets/3d617362-142c-491a-8cb1-69bb8581bd49" />


> Installs Node.js, npm, and Go .

### Install Snyk CLI globally
```bash
sudo npm install -g snyk
```
<img width="454" height="28" alt="image" src="https://github.com/user-attachments/assets/8d469d2e-cd25-4098-b0b2-e51e314f8a56" />

>Installs Snyk CLI globally using npm.

### Authenticate Snyk
```bash
snyk auth <your-snyk-auth-token>
```
<img width="606" height="54" alt="image" src="https://github.com/user-attachments/assets/12c69192-c80a-4065-a2ce-09e7f39530c7" />

>Authenticates your Snyk account to allow scanning of projects.

### Install Project Dependencies

```bash
npm install
```
<img width="416" height="28" alt="image" src="https://github.com/user-attachments/assets/910ac16f-6527-4134-9b31-9cd4cfa408e9" />

### Run Dependency Scan
```bash
snyk test --json > snyk-dependency-report.json
```
<img width="641" height="24" alt="image" src="https://github.com/user-attachments/assets/d2a85e17-3d21-499b-8ad6-a0062a542a71" />

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
<img width="605" height="460" alt="image" src="https://github.com/user-attachments/assets/cd842383-f9b7-47ec-979c-88c9c7987ed5" />


>Formats the dependency vulnerability report into a readable table showing Package, Version, Severity, and Direct Dependency.

---

## Troubleshooting

| Issue                                           | Solution                                                                                               |
|-------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| `snyk: command not found`                       | Ensure Snyk CLI is installed globally: `npm install -g snyk`                                           |
| Scan fails to detect dependencies              | Run `npm install` first to install all project dependencies                                           |
| `ENOTEMPTY` error during `npm install`         | Remove `node_modules` and `package-lock.json` then clean cache: `rm -rf node_modules package-lock.json && npm cache clean --force` |
| High number of vulnerabilities in `npm audit`  | Run `npm audit fix` for safe fixes, or `npm audit fix --force` for all (including breaking changes)    |

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
   Node.js with npm.

2. **How do I run a dependency scan?**  
   Use `snyk test --json > snyk-dependency-report.json`.

3. **How do I view scan results in a readable format?**  
   Format the JSON report using `jq` to get a table of vulnerabilities.

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

