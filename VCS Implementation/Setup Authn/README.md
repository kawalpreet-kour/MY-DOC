# POC on VCS Implementation – Setup Authentication

<img width="200" height="148" alt="download" src="https://github.com/user-attachments/assets/620e96b3-60e6-40c2-a532-be6d191b535f" />

---
## Author Information

| Last Updated On | Version | Author           | Level           | Reviewer               |
|-----------------|---------|------------------|-----------------|------------------------|
| 18-08-2025      | V1.0    | Kawalpreet Kour  | Internal Review | Pritam                 |
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
    - [Step 1: Verify Organization & Teams](#step-1-verify-organization--teams)  
    - [Step 2: Navigate to Repository Access](#step-2-navigate-to-repository-access)  
    - [Step 3: Assign Team Permissions](#step-3-assign-team-permissions)  
    - [Step 4: Verify Access](#step-4-verify-access)  
5. [Best Practices](#best-practices)  
6. [SSO Integration (Optional)](#sso-integration-optional)  
7. [FAQs](#faqs)  
8. [Contact Information](#contact-information)  
9. [References](#references)  

</details>

---
## Purpose

This Proof of Concept (POC) demonstrates manual authentication and access provisioning in GitHub repositories.  
It verifies that team-based permissions (Read/Write) are enforced as per roles, and prepares the environment for future SSO integration.

---

## Pre-Requisites 

| Requirement                     | Description                                   |
|--------------------------------|-----------------------------------------------|
| GitHub Account                  | Access to the organization's GitHub          |
| Repository Access               | Must have admin rights to assign team permissions |
| Test Accounts                   | For Developer, Reviewer, Designer, Tester    |

---

## System Requirements

| Hardware/Software | Minimum Requirement |
|------------------|-------------------|
| Browser           | Chrome / Firefox / Edge |
| Internet          | Required to access GitHub |

---

## Setup and Execution

### Step 1: Verify Organization & Teams
- Go to **Organization → Teams**  
- Check teams and members  

<img width="450" height="200" alt="image" src="https://github.com/user-attachments/assets/644e3e38-1934-4933-ae94-951f00a36169" />


<img width="450" height="200" alt="Screenshot from 2025-08-17 23-07-20" src="https://github.com/user-attachments/assets/7a06af41-1510-4d76-8d93-7bbedceed083" />


### Step 2: Navigate to Repository Access
- Open repository (e.g., `APT-GET-SWAG/nitin_repo`)  
- Click **Settings → Access → Collaborators and Teams**  


<img width="450" height="200" alt="Screenshot from 2025-08-18 00-18-10" src="https://github.com/user-attachments/assets/9ad4fa28-4261-4bba-bd4a-d410b2d7f7df" />

<img width="450" height="200" alt="Screenshot from 2025-08-18 00-18-58" src="https://github.com/user-attachments/assets/b9931175-54a0-46f2-9606-b517dc8e4f91" />



### Step 3: Assign Team Permissions
- Select team and assign role:

| Team        | Permission    |
|------------|----------------|
| Developers | Write          |
| Reviewers  | Read           |


<img width="450" height="200" alt="image" src="https://github.com/user-attachments/assets/a6d79fd9-3948-4128-b671-eb8052df700d" />


### Step 4: Verify Access
- Login as test account per team/member  
- Check allowed actions:

| Role       | Actions Allowed           |
|-----------|---------------------------|
| Developer | Push code (Write)         |
| Reviewer  | Read/Write as assigned    |
| Viewer    | Read only                 |

<img width="450" height="200" alt="Screenshot from 2025-08-18 00-20-10" src="https://github.com/user-attachments/assets/672eb1bc-83c0-4d20-949f-e21f2c2ac9ea" />

<img width="450" height="200" alt="Screenshot from 2025-08-18 00-20-10" src="https://github.com/user-attachments/assets/1d4b0d27-cabf-4ccb-9407-7a431c538515" />


<img width="450" height="200" alt="Screenshot from 2025-08-18 00-26-46" src="https://github.com/user-attachments/assets/3de109b0-1173-4820-97ff-bd2846316662" />
<img width="450" height="200" alt="Screenshot from 2025-08-18 00-26-46" src="[https://github.com/user-attachments/assets/3de109b0-1173-4820-97ff-bd2846316662](https://github.com/user-attachments/assets/82acdf19-90b0-40fb-82f7-1e6e67ea48c9)" />


---

## Best Practices

| Practice                      | Description                                        |
|--------------------------------|--------------------------------------------------|
| Principle of Least Privilege   | Assign minimal permissions required per role    |
| Document Access                | Keep screenshots and logs for audit purposes    |
| Prepare for SSO Integration    | Map teams to SAML groups for easier management  |

---

## SSO Integration (Optional)

| Step No | Action                                               | Description                                        |
|---------|-----------------------------------------------------|--------------------------------------------------|
| 1       | Go to Organization → Settings → Security → SAML Single Sign-On | Opens the SSO configuration page in GitHub      |
| 2       | Connect to your IdP (Identity Provider)            | Authenticate and link your organization to IdP  |
| 3       | Map teams to SSO groups                             | Assign GitHub teams to corresponding IdP groups |


> Note: SSO is planned for future enforcement. Current setup is manual provisioning.

---


## FAQs

1. **How do I verify team permissions?**  
   Login with a test account and attempt actions according to role.

2. **What if someone has more permissions than assigned?**  
   Check repository and organization-level access; revoke unnecessary rights.

3. **Is SSO mandatory?**  
   No, manual provisioning works; SSO is optional for future integration.

---

## Contact Information

| Name             | Email                                  |
|-----------------|----------------------------------------|
| Kawalpreet Kour  | kawalpreet.kour.snaatak@mygurukulam.co |

---

## References

- [GitHub Docs – Managing Access](https://docs.github.com/en/organizations/managing-access-to-your-organizations-repositories)
- [GitHub Docs – Teams and Permissions](https://docs.github.com/en/organizations/organizing-members-into-teams)
