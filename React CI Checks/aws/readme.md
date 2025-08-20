<img width="504" height="250" alt="image" src="https://github.com/user-attachments/assets/2631fa8a-5121-4fec-ab8e-857e9aea33f5" />


# AWS Service Control Policies (SCP) — Step‑by‑Step Setup Guide

## Author Information

| Created by   | Created on | Version | Last Updated On | Pre Reviewer    | L0 Reviewer | L1 Reviewer   | L2 Reviewer  |
| ------------ | ---------- | ------- | --------------- | --------------- | ----------- | ------------- | ------------ |
| Divya Mishra | 16-08-2025 | V 1.0   | 16-08-2025      | Sahil/Siddharth | Ram Ratan   | Gaurav Singla | Mahesh Kumar |

---

## Table of Contents

1. [Purpose](#1-purpose)  
2. [Prerequisites](#2-prerequisites)  
3. [SCP Deployment Steps & Naming Conventions](#3-scp-deployment-steps--naming-conventions)  

4. [AWS Service Control Policies UI Step-by-Step Guide](#4-aws-service-control-policies-ui-step-by-step-guide)  
   <details>
   <summary>Click to expand Steps</summary>  

   - [4.1 Create Organization Unit for Management Account](#step-41-create-organization-unit-for-management-account)  
   - [4.2 Accept Invitation to Join Organization](#step-42-accept-invitation-to-join-organization)  
   - [4.3 Create a new Organization](#step-43-create-a-new-organization)  
   - [4.4 Add OU to Member Account](#step-44-add-ou-to-member-account-to-apply-scp-on-the-same-as-per-the-attahced-scp)  
   - [4.5 Create a New SCP Policy](#step-45-create-a-new-scp-policy)  
   - [4.6 Attach SCP to OU or Account](#step-46-attach-scp-to-an-organizational-unit-ou-or-account)  
   - [4.7 Test the SCP](#step-47-test-the-scp)  

   </details>  

5. [Explore Spot Instances](#5-explore-spot-instances)  
6. [Troubleshooting](#6-troubleshooting)  
7. [FAQs](#7-faqs)  
8. [Conclusion](#8-conclusion)  
9. [Contact Information](#9-contact-information)  
10. [References](#10-references)  

---

## 1. Purpose

The purpose of this document is to provide a clear understanding of AWS Service Control Policies (SCPs) and their role in managing permissions across multiple AWS accounts within an organization. It outlines how SCPs help enforce governance, strengthen security, and maintain compliance by defining permission boundaries at the organizational level. This document serves as a reference for implementing SCPs effectively to achieve consistent, controlled, and secure access management in AWS environments.

#### Please refer the to AWS Service Control Policies  [Refer this Documentation](https://github.com/Snaatak-Cloudops-Crew/documentation/tree/scrum-116-aryan-mishra/Cost-Optimization/Service-Control-Policies)

---

## 2. Prerequisites

| Requirement                           | Description                                                                                                                       |
| ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **AWS Organizations (All features)**  | SCPs work only when your AWS Organization is set to **All features** mode.                                                        |
| **Management account access**         | You must use the management (root) account to create, edit, and attach SCPs.                                                      |
| **Administrator permissions**         | An IAM user or role in the management account with `organizations:*` plus read-only access to all accounts and OUs.               |
| **Defined OU and account structure**  | A clear plan of your Organizational Units (OU) hierarchy and which SCPs apply at each stage (e.g., Sandbox → Pilot → Production). |

**Note:** SCPs set the **maximum permission boundaries** for accounts—they **cannot** grant permissions on their own.

---

## 3. SCP Deployment Steps & Naming Conventions

**Strategy:** Begin with targeted **deny-list** guardrails applied together with the default `FullAWSAccess` policy, test them in a staging OU, then progressively expand to production OUs after validation.

**Suggested naming convention:**

| Policy Name                       | Purpose                                       |
| --------------------------------- | --------------------------------------------- |
| `SCP-Deny-LeavingOrg`             | Prevent member accounts from leaving the org. |
| `SCP-Deny-DisallowedRegions`      | Deny usage outside approved regions.          |
| `SCP-Protect-Security-Services`   | Deny disabling CloudTrail/Config/GuardDuty.   |
| `SCP-Protect-AdminRole-Exception` | Protect IAM admin role; allow exception.      |
| `SCP-Block-Root-Access`           | Restrict root user access to services.        |

**OU rollout order:**

* **Sandbox** → Low risk testing.
* **Development** → Early validation.
* **Test** → Final checks.
* **Production** → After validation.
  
---

## 4. AWS Service Control Policies UI Step-by-Step Guide

* An AWS Organization already created.
* A member account under the organization to test SCP.
* IAM permissions to create and attach Service Control Policies.

### Step 4.1: Create Organization unit for Management Account

<details>
<summary>Click on Screenshot</summary>

<img width="1750" height="795" alt="image" src="https://github.com/user-attachments/assets/d2e365d4-3a4c-4218-a457-6d463bcf2299" />


</details>

### Step 4.2: Accept Invitation to join Organization

1. Go to AWS organization.
2. Click on View Inviation
3. Accept the invite to join the organization.

<details>
<summary>Click on Screenshot</summary>

<img width="1761" height="426" alt="image" src="https://github.com/user-attachments/assets/5d6536d1-69ae-4692-8d19-5f566461e4e8" />



<img width="1760" height="835" alt="image" src="https://github.com/user-attachments/assets/735e4f54-1c25-4010-8082-4f7dac058714" />


</details>


### Step 4.3: Create a new Organization

1. Go to Root User account for Management Account in AWS Organization. Select Account Managment for eg : snatakp15 and click on Create new.
2. CLick on Actions and create an Organization unit for eg development.
3. Developmet OU is created.

<details>
<summary>Click on Screenshot</summary>

<img width="1835" height="832" alt="image" src="https://github.com/user-attachments/assets/44b20c15-7b5f-493f-bf09-893e1908fe34" />

<img width="1835" height="832" alt="image" src="https://github.com/user-attachments/assets/bcc753c8-dcf2-4848-9213-104f317277bc" />

<img width="1838" height="863" alt="image" src="https://github.com/user-attachments/assets/1f814503-0458-4c18-b433-e12b16aa2387" />


</details>



### Step 4.4: Add OU to Member account to apply SCP on the same as per the attahced SCP

1. Click on Account ( Divya Mishra ) as per the to add OU.
2. Go to Policies and attached Development OU as created to attach.

<details>
<summary>Click on Screenshot</summary>

<img width="1838" height="863" alt="image" src="https://github.com/user-attachments/assets/7343984b-efb2-4666-9761-798628fc1071" />

<img width="1838" height="863" alt="image" src="https://github.com/user-attachments/assets/f9f59924-2de9-401f-b5e3-1c9b29a2f809" />

<img width="1838" height="863" alt="image" src="https://github.com/user-attachments/assets/23f73f4d-27cd-4b31-8b92-06c4e067864d" />

<img width="1838" height="863" alt="image" src="https://github.com/user-attachments/assets/498d5db4-0ce4-4884-a15a-420f1ec75e8c" />


</details>

### Step 4.5: Create a New SCP Policy

1. In the left panel, click on **Policies**.
2. Select **Service control policies**.
3. Click **Create policy**.
4. Enter a **name** (e.g., `AllowOnlyApprovedEC2Types`).
5. Paste the following JSON into the policy editor:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyNonApprovedInstanceTypes",
      "Effect": "Deny",
      "Action": "ec2:RunInstances",
      "Resource": "*",
      "Condition": {
        "StringNotEqualsIfExists": {
          "ec2:InstanceType": [
            "t3.micro",
            "t3.small",
            "m5.large"
          ]
        }
      }
    }
  ]
}
```

6. Click **Create policy** to save.

<details>
<summary>Click on Screenshot</summary>

<img width="1837" height="865" alt="image" src="https://github.com/user-attachments/assets/07d0ceef-95f6-4650-a897-db7cbe67722e" />

<img width="1828" height="610" alt="image" src="https://github.com/user-attachments/assets/b714b017-94d5-454a-9eca-81e0dc846338" />


</details>

---

### Step 4.6: Attach SCP to an Organizational Unit (OU) or Account

1. Navigate to **Organize accounts** in AWS Organizations.
2. Select the **OU or account** you want to restrict.
3. Go to the **Service control policies** tab.
4. Click **Attach** and choose your newly created policy.
5. Save the changes.

<details>
<summary>Click on Screenshot</summary>

<img width="1828" height="610" alt="image" src="https://github.com/user-attachments/assets/f7422520-43ba-4666-9d8f-0baaaafb1a9b" />

<img width="1826" height="731" alt="image" src="https://github.com/user-attachments/assets/bb6e9cb1-1469-42bf-b011-f4267e956233" />

<img width="1841" height="890" alt="image" src="https://github.com/user-attachments/assets/81aa0517-594a-4d18-b460-20b89347f76f" />

<img width="1836" height="832" alt="image" src="https://github.com/user-attachments/assets/aaa39ba5-0e14-48c3-abc0-712bf9ff4581" />

<img width="1826" height="803" alt="image" src="https://github.com/user-attachments/assets/1f5819d3-1f74-4431-9314-507636942513" />


</details>

---

### Step 4.7: Test the SCP

1. Switch to the **member account** (where the policy is attached).
2. Go to **EC2 → Launch Instance**.
3. Try launching:

   * **Allowed type**: `t3.micro` → should succeed.
   * **Restricted type**: e.g., `t2.micro` → should fail with an **AccessDenied** error.

<details>
<summary>Click on Screenshot</summary>

<img width="1772" height="872" alt="Screenshot from 2025-08-16 16-32-26" src="https://github.com/user-attachments/assets/1f256338-6d6f-41e2-adab-df0c1d83e17e" />

<img width="1772" height="872" alt="image" src="https://github.com/user-attachments/assets/aa450a27-18be-4cf6-80c2-30fa5ca9e402" />

<img width="1772" height="872" alt="image" src="https://github.com/user-attachments/assets/a671ecae-e793-4bfc-a6da-dad4b00a85d3" />

<img width="1816" height="878" alt="image" src="https://github.com/user-attachments/assets/5515e818-a8f6-4ad9-9d20-eceafa6d1598" />


</details>

---


## 5. Explore Spot Instances

For cost optimization, you can also try **EC2 Spot Instances** with the approved instance types.

* While launching EC2, choose **Request Spot Instances** in the **Purchase options** section.
* Ensure your SCP allows the instance type you select.
* This helps reduce costs while still enforcing organizational policies.

---

## 6. Troubleshooting

| Issue                                     | Cause                                     | Solution                                                              |
| ----------------------------------------- | ----------------------------------------- | --------------------------------------------------------------------- |
| SCP not applying                          | SCPs are not enabled for the Org          | Go to **AWS Organizations → Settings** and enable SCPs                |
| Policy attached but no effect             | SCP needs to be attached to OU or account | Verify that the SCP is attached properly                              |
| User still launching restricted instances | IAM permissions allow EC2 launch          | Remember: SCPs set a maximum boundary, IAM must also allow the action |
| JSON error while creating policy          | Syntax issue in JSON                      | Validate JSON before saving (use online validator or AWS editor)      |

---

## 7. FAQs

**1. What is the difference between IAM Policies and SCPs?**

IAM Policies control what a specific user or role can do within an AWS account, while SCPs apply at the AWS Organization level and set **guardrails** that restrict what actions can be allowed across accounts, regardless of IAM policies.

**2. Why did my EC2 instance launch fail even though I used the correct instance type?**

This usually happens if the SCP was not updated or if the condition was incorrectly configured. Always verify the SCP JSON and ensure it includes the correct `ec2:InstanceType`.

**3. Can I apply SCPs directly to individual IAM users?**

No. SCPs can only be attached to AWS Organizations entities: **root, organizational units (OUs), or accounts.** They do not attach directly to IAM users or roles.

**4. What happens if I don’t attach any SCP?**

By default, if no SCP is attached, the account has **Full AWS Access**, subject only to IAM policies.

**5. Can SCPs be used to allow actions?**

No, SCPs are **not permission-granting policies**. They only define the maximum available permissions. IAM policies are still required to grant access. SCPs only restrict.

---

## 8. Conclusion

AWS Service Control Policies (SCPs) provide a structured way to enforce governance and security across an organization. By applying SCPs, administrators can define clear permission boundaries, ensuring that accounts only have access to the services and actions necessary for business needs. This reduces the risk of misconfigurations, unauthorized access, and policy drift across environment.

---

## 9. Contact Information
| Name         | Email                                                                             |
| ------------ | --------------------------------------------------------------------------------- |
| Divya Mishra | [divya.mishra.snaatak@mygurukulam.co](mailto:divya.mishra.snaatak@mygurukulam.co) |


---

## 10. References

| Link                                                                                              | Description                                                                                     |
| ------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| [Link](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html) | Official AWS guide to create, manage, and attach Service Control Policies (SCPs).               |
| [Link](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_console.html)              | Step-by-step guide for using AWS Management Console to manage organizations, OUs, and policies. |
| [Link](https://docs.aws.amazon.com/ec2/)                                                          | Official documentation for Amazon EC2, including details on instance types like T3 micro.       |

---
