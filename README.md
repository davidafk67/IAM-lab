# 🚀 KeiLAB: Identity and Access Management (IAM) Sandbox

Welcome to my hands-on Cybersecurity and IAM portfolio. This repository documents my practical implementations of enterprise security architectures, access control models, and identity governance using cloud-native platforms and industry standards.

---

## 🛡️ Project 01: Implementing RBAC & Identity Lifecycle Auditing in Auth0

### 📝 Project Overview
This project demonstrates the deployment of a corporate testing environment using **Auth0 (Okta IDaaS)** to securely manage the identity lifecycle and mitigate insider risk by strictly enforcing the **Principle of Least Privilege (PoLP)**. 

### 🛠️ Core Skills & Concepts Applied
* **IDaaS (Identity as a Service):** Centralized cloud identity governance.
* **Identity Lifecycle Management:** Secure provisioning of new identities (*Joiner Scenario*).
* **RBAC (Role-Based Access Control):** Engineering access models based on functional business roles.
* **Security Auditing:** Interpreting system logs for compliance and forensic analysis.

---

### 🚀 Implementation Phases

#### 1. Identity Provisioning (*Joiner Scenario*)
Simulating a new hire joining the IT department, a test user was provisioned into the directory, validating credential hashing and initial metadata assignment.

#### 2. RBAC Architecture Engineering
To prevent privilege creep and avoid granting direct administrative rights, a custom role was designed and deployed:
* `soporte-TI`

This role serves as a container for granular permissions, ensuring the operational user only has the absolute minimum access required to execute daily tasks (Least Privilege). The provisioned user was successfully mapped to this role.

#### 3. Forensic Log Analysis & Audit Trail
To validate compliance and ensure all security events are traceable, I accessed the platform's **Monitoring** module to analyze the immutable digital trail of the infrastructure. 

---

### 📊 Technical Evidence (Audit Trail)

Below is the verified **Auth0 System Log** (`image_44b43c.png`) demonstrating the exact, chronological execution sequence of the IAM lifecycle:

<img width="1136" height="153" alt="image" src="https://github.com/user-attachments/assets/3643aabc-17bc-4f7e-918f-2891300a0636" />


**Breakdown of the Audit Trail:**
1. **`Success Signup` & `Create a User`:** Successful ingestion and initialization of the new identity.
2. **`Create a role`:** Provisioning of the custom security boundary (`soporte-TI`).
3. **`Assign users to a role`:** Enforcement of the RBAC policy, binding the identity to its restricted operational permissions.
4. **`Success Verification Email`:** Completion of the out-of-band identity verification flow.

---
### 📈 Next Steps for this Sandbox
* [ ] Implement Multi-Factor Authentication (MFA) conditional access policies.
* [ ] Federate a test application for Single Sign-On (SSO) workflows using OIDC/SAML.
* [ ] Automate user provisioning using Python scripts via the Okta/Auth0 Management API.
