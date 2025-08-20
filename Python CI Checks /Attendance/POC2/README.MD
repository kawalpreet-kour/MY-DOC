
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

## Table of Contents

1. [Introduction](#1-introduction)
2. [Prerequisites](#2-prerequisites)
3. [System Requirements](#3-System-Requirements)
4. [Setup and Execution](#4-Setup-and-Execution)
5. [Troubleshooting](#5-troubleshooting)
6. [FAQs](#6-FAQs)
7. [Contact Information](#7-contact-Information)
8. [References](#8-references)


---

## 1. Introduction

This document provides a Proof of Concept (POC) for implementing Python  checks using SonarQube for static code analysis

---
## 2. Prerequisites

| Dependency            | Version                   |
| --------------------- | ------------------------- |
| **Java**              | JDK 11+                   |
| **SonarQube**         | v9.x or above             |
| **SonarQube Scanner** | Latest compatible version |

---
## 3. System Requirements

| Hardware/Software | Minimum Recommendation                     |
| ----------------- | ------------------------------------------ |
| **Processor**     | 2 CPU cores                                |
| **RAM**           | 4 GiB                                      |
| **Disk**          | 10 GB                                      |
| **OS**            | Ubuntu 22.04 LTS / Windows 10+ / macOS 11+ |

---


## 4. Setup and Execution

### Update System Packages & Install java

_Follow this link for Installation_  
(**[Click here to view Setup guide](https://github.com/Snaatak-Apt-Get-Swag/documentation/tree/89c6c6e8de0b6e6abbca8273c7f8ae0051f65c9b/Softwares/Java/Installation/Manual)**)


```bash
sudo apt update 
```
<img width="1447" height="612" alt="Screenshot 2025-08-16 162620" src="https://github.com/user-attachments/assets/e002874b-a32d-469b-9db7-ecb859703478" />

---
### Step 2: Install java and verify

```bash
sudo apt install openjdk-17-jdk -y
java -version
```
<img width="1522" height="493" alt="Screenshot 2025-08-16 162628" src="https://github.com/user-attachments/assets/c0fb479f-c7f2-4f58-a0e3-1a0376c43a7d" />

---

### Step 3: Install SonarQube

```bash
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.5.1.90531.zip
sudo apt install unzip -y
unzip sonarqube-10.5.1.90531.zip
mv sonarqube-10.5.1.90531 sonarqube

```
<img width="1917" height="298" alt="Screenshot 2025-08-16 162720" src="https://github.com/user-attachments/assets/4e89030b-dd21-4798-b5d0-18a1ce1544d6" />

---
### Step 4: Create Systemd Service File

```bash
sudo nano /etc/systemd/system/sonarqube.service
```
and paste these line 

```bash
[Unit]
Description=SonarQube service
After=syslog.target network.target

[Service]
Type=forking
ExecStart=/home/ubuntu/sonarqube/bin/linux-x86-64/sonar.sh start
ExecStop=/home/ubuntu/sonarqube/bin/linux-x86-64/sonar.sh stop
User=ubuntu
Group=ubuntu
Restart=always

[Install] WantedBy=multi-user.target
```
---
### Step 5: Reload, Enable & start the Service

```bash
sudo systemctl daemon-reload
sudo systemctl start sonarqube
sudo systemctl enable sonarqube
```
<img width="1918" height="470" alt="Screenshot 2025-08-16 162738" src="https://github.com/user-attachments/assets/23a87118-b2eb-428b-abdf-d9838e1482bb" />

---
### Step 6: Access the Dashboard

```bash
http://<INSTANCE_PUBLIC_IP>:9000
```
with the help of `username : admin ` and `password : admin`

---

### Step 7: Create a Project in SonarQube

1. Go to **Projects** → **Create Project**  
2. Select **Manually**  
3. Enter:  
   - **Project Key** → `python`  
   - **Project Name** → `python`  
4. Choose **Locally**

<img width="1919" height="607" alt="Screenshot 2025-08-16 162914" src="https://github.com/user-attachments/assets/43989c71-ed43-448d-ae2a-44dc9b263ebc" />
 
5. Generate a **Token** → copy it (we will need it in config)

   <img width="1846" height="656" alt="Screenshot 2025-08-16 162933" src="https://github.com/user-attachments/assets/f032f656-dd75-4f4e-96ef-1f3fddc115d5" />


---
### Step 8: Install SonarScanner

```bash
 wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip
unzip sonar-scanner-cli-5.0.1.3006-linux.zip
sudo mv sonar-scanner-5.0.1.3006-linux /opt/sonar-scanner
echo 'export PATH=$PATH:/opt/sonar-scanner/bin' >> ~/.bashrc
source ~/.bashrc
```

<img width="1919" height="344" alt="Screenshot 2025-08-16 162752" src="https://github.com/user-attachments/assets/85f75415-824c-4e9d-88c0-261f2f21cf47" />


---

### Step 9: Clone the project repo and navigate into it

```bash
git clone <url>
cd directory
```

<img width="1893" height="214" alt="Screenshot 2025-08-16 162817" src="https://github.com/user-attachments/assets/8337a765-4df4-4154-a078-6b5bb40ebb76" />

---
### Step 10: To run analysis on project copy the commands from sonarqube UI
<img width="1919" height="713" alt="Screenshot 2025-08-16 162944" src="https://github.com/user-attachments/assets/7dad235c-c538-4ea1-bfc8-acd3a2ab802f" />



```bash
 sonar-scanner \
  -Dsonar.projectKey=python \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://13.233.84.84:9000 \
  -Dsonar.token=sqp_1ec179e8e7f92fbe73e2f72ac8a21334bd831b38
```
### Step 11. Now paste these commands in the project root folder

<img width="1919" height="963" alt="Screenshot 2025-08-16 162836" src="https://github.com/user-attachments/assets/6c192713-36e6-471f-a1ef-02f7e38c2462" />


### Step 12. Check the report on Sonarqube UI

#### Report for Attendance API

<img width="1906" height="860" alt="Screenshot 2025-08-16 162852" src="https://github.com/user-attachments/assets/6a250a93-9e92-4502-b745-f3f732c69f64" />

#### Report for Notificaton API

<img width="1910" height="882" alt="image" src="https://github.com/user-attachments/assets/e1b66f7d-4a17-42a6-ad6e-ce151a356598" />



---

## 5. Troubleshooting

| Issue | Possible Cause | Solution |
|-------|----------------|----------|
| SonarQube service not starting | Insufficient RAM (needs 2GB+ free) | Allocate more memory or increase swap space |
| Port 9000 not accessible | Firewall blocking / Security Group not open | Allow inbound traffic on port 9000 |
| "Java not found" error | Java not installed or PATH not set | Verify with `java -version` and install JDK 11+ |
| SonarScanner not recognized | PATH not updated | Run `source ~/.bashrc` or add scanner bin path manually |
| Authentication failed (token) | Wrong/expired token used | Regenerate token in SonarQube UI and update command |

---

## 6. FAQs
**1. Do I need PostgreSQL for SonarQube?**  
→ For production use, yes. For POC/testing, embedded H2 DB works but data resets on restart.  
 

**2. How do I reset the admin password?**  
→ Use default `admin/admin`. If changed and forgotten, update `users` table in DB or reset via DB query.  

**3. Can SonarQube analyze multiple languages?**  
→ Yes, it supports 20+ languages (Python, Java, JS, C#, etc.) with built-in plugins.  

**4. How do I stop SonarQube service?**  
→ Run `sudo systemctl stop sonarqube`.  
