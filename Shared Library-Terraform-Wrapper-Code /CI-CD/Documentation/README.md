<img width="400" height="400" alt="Terraform Shared Library" src="https://github.com/user-attachments/assets/placeholder-shared-library.png" />

---

## Author Information

| Last Updated On | Version | Author           | Level            | Reviewer          |
|-----------------|---------|-----------------|-----------------|-----------------|
| 01-10-2025      | V1.0    | Kawalpreet Kour | Internal Review | Sharvari         |
|                 |         | Kawalpreet Kour | L0              | Shreya           |
|                 |         | Kawalpreet Kour | L1              | Abhishek V       |
|                 |         | Kawalpreet Kour | L2              | Abhishek Dubey   |

---

<details>
  <summary><h2><strong>Table of Contents</strong></h2></summary>

1. [Introduction](#introduction)  
2. [What is the Shared Library?](#what-is-the-shared-library)  
3. [Why Use a Shared Library?](#why-use-a-shared-library)  
4. [Integration With Terraform Wrapper CI/CD](#integration-with-terraform-wrapper-cicd)  
   - [Reusable Functions](#reusable-functions)  
   - [Stages Controlled by Shared Library](#stages-controlled-by-shared-library)  
5. [Required Configurations](#required-configurations)  
6. [Environment Variable Handling](#environment-variable-handling)  
7. [Workflow Diagram](#workflow-diagram)  
8. [Best Practices](#best-practices)  
9. [FAQs](#faqs)  
10. [Contact Information](#contact-information)  
11. [References](#references)  

</details>

---

## Introduction

This document describes the **Shared Library** for Terraform wrapper CI/CD pipelines. The shared library centralizes reusable functions and standardizes Terraform operations across multiple projects and environments. It reduces duplication, enforces best practices, and allows multiple Terraform wrapper scripts to rely on a consistent automation layer.

---

## What is the Shared Library?

The **Shared Library** is a set of scripts, functions, and helper utilities that encapsulate common Terraform operations, such as:

- Initialization (`init`)  
- Validation (`validate`)  
- Planning (`plan`)  
- Applying changes (`apply`)  
- Destroying resources (`destroy`)  

It is designed to be called from multiple Terraform wrapper scripts across different repositories, ensuring consistency in CI/CD execution.

---

## Why Use a Shared Library?

| Benefit        | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| Reusability    | Common functions are centralized and can be reused across multiple projects.|
| Consistency    | Guarantees all wrapper scripts follow the same Terraform workflow and standards. |
| Maintainability| Updates to Terraform processes only need to be done in the shared library, propagating to all consumers. |
| Security       | Sensitive variable handling and backend configurations are standardized.    |
| Automation     | Simplifies integration with CI/CD pipelines, reducing manual errors.       |

---

## Integration With Terraform Wrapper CI/CD

The shared library is integrated into wrapper scripts via **sourcing or importing functions**. Wrapper scripts use the library to execute CI/CD stages consistently.

---

## Reusable Functions

| Function       | Purpose                                                                 |
|----------------|-------------------------------------------------------------------------|
| `tf_init`      | Initializes Terraform, sets backend configuration.                      |
| `tf_validate`  | Validates the Terraform configuration files for syntax and correctness.|
| `tf_plan`      | Generates an execution plan using environment-specific variables.      |
| `tf_apply`     | Applies the Terraform plan safely.                                      |
| `tf_destroy`   | Destroys infrastructure, usually used for dev or QA environments.       |
| `tf_output`    | Retrieves output values from the Terraform state.                       |
| `check_env_vars` | Ensures required environment variables are set.                        |
| `lock_state`   | Handles state locking to prevent concurrent operations.                 |
| `log_message`  | Standard logging function for CI/CD output messages.                    |

---

## Stages Controlled by Shared Library

| Stage       | Wrapper Script Command        | Shared Library Function | Purpose                                           |
|------------|-------------------------------|------------------------|-------------------------------------------------|
| Init       | `./wrapper.sh init <env>`     | `tf_init`             | Initializes backend, downloads modules, sets up environment. |
| Validate   | `./wrapper.sh validate <env>` | `tf_validate`         | Ensures syntax and module correctness.         |
| Plan       | `./wrapper.sh plan <env>`     | `tf_plan`             | Creates an execution plan (`plan.out`) for review. |
| Apply      | `./wrapper.sh apply <env>`    | `tf_apply`            | Applies approved Terraform changes.           |
| Destroy    | `./wrapper.sh destroy <env>`  | `tf_destroy`          | Destroys infrastructure in non-production environments. |
| Output     | `./wrapper.sh output <env>`   | `tf_output`           | Retrieves Terraform outputs such as endpoints or IPs. |

---

## Required Configurations

### Backend Configuration
- `backend.tfvars` must exist for each environment (`dev`, `staging`, `prod`).  
- Example: S3 bucket + DynamoDB table for locking.

### Environment Variables
- Must define the target environment (`ENV`) and optionally credentials for secret managers.

### Variable Files
- Each environment has its own `main.tfvars` with resource parameters.

### CI/CD Secrets
- Platform secrets (GitHub/GitLab/Azure DevOps) should store sensitive values like API tokens or access keys.

---

## Environment Variable Handling

- The shared library ensures all required environment variables are checked before execution.  
- Example:

```bash
export ENV=dev
export AWS_ACCESS_KEY_ID=xxxx
export AWS_SECRET_ACCESS_KEY=xxxx
Missing required variables trigger a controlled failure with descriptive logging.

Secrets are never printed to console, and Terraform sensitive variables are marked with sensitive = true.

---

## Workflow Diagram

graph TD
    A[Developer: Push Code / Merge PR] --> B[CI: Wrapper script calls Shared Library functions]
    B --> C[tf_init, tf_validate, tf_plan]
    C --> D[Plan Artifact Ready]
    D --> E{Manual Approval?}
    E -- Approve --> F[CD: tf_apply]
    E -- Reject --> G[Pipeline Stops / Notify]
    F --> H[Infrastructure & State Updated]
    F -- Fail --> I[Notification: Apply Failed]
```
---
## Best Practices

| Best Practice              | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| Centralize Common Functions| Keep reusable logic in the shared library, not individual wrappers.        |
| Environment Isolation      | Always use `.tfvars` files per environment.                                 |
| Use Remote Backend         | Ensure state files are centralized with locking enabled.                    |
| Secrets Management         | Never commit secrets; use CI/CD secrets or Vault.                           |
| Logging & Error Handling   | Use consistent logging and error handling in shared functions.             |
| Keep Library Lightweight   | Avoid environment-specific logic in the shared library; delegate that to wrapper scripts. |

---

## FAQs

**Q: Can multiple projects use the same shared library?**  
**A:** Yes, by sourcing or importing the library in each wrapper script.

**Q: How are environment variables validated?**  
**A:** The shared library provides a `check_env_vars` function that ensures required variables exist and are not empty.

**Q: Can the library handle manual approval gates?**  
**A:** Yes, wrapper scripts control approvals, but the library provides functions to generate and apply plans safely.

---

## Contact Information

| Name               | Email                                     |
|-------------------|-------------------------------------------|
| **Kawalpreet Kour** | kawalpreet.kour.snaatak@mygurukulam.co |

---

## References

| Description                       | Link                                                           |
|----------------------------------|---------------------------------------------------------------|
| Terraform Official Documentation  | [https://www.terraform.io/docs](https://www.terraform.io/docs) |
| Terraform CI/CD Best Practices    | [https://learn.hashicorp.com/collections/terraform/cicd](https://learn.hashicorp.com/collections/terraform/cicd) |
| HashiCorp Vault (Secrets Management) | [https://www.vaultproject.io](https://www.vaultproject.io)      |

