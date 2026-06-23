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

---

## 🛡️ Project 02: Enforcing Global Multi-Factor Authentication (MFA) via TOTP

### 📝 Project Overview
This project demonstrates the implementation of a defensive access control posture by enforcing tenant-wide **Multi-Factor Authentication (MFA)**. The objective is to mitigate single-factor vulnerabilities (such as credential reuse or phishing) by requiring a secondary out-of-band validation mechanism before access token issuance.

### 🛠️ Core Skills & Concepts Applied
* **MFA Enrollment Policies:** Engineering global conditional triggers (`Always Require`).
* **Cryptographic Seed Distribution:** Understanding QR-based provisioning vs. manual secret keys for TOTP.
* **Identity Interception Flow:** Analyzing how Identity Providers (IdP) halt authentication phases.
* **Transaction Testing:** Validating policy enforcement using identity platform simulator consoles.

---

### 🚀 Implementation Phases

#### 1. Factor Activation & Policy Governance
Within the tenant security infrastructure, the **One-Time Password (OTP)** MFA factor was enabled to accept cryptographically generated codes from validation engines like Google Authenticator (`1.PNG`). To prevent bypass vectors, the evaluation policy was systematically updated from its default state to **Always Require**, binding all downstream applications under this security boundary (`2.PNG`).

#### 2. Authentication Flow Testing Simulation
To safely evaluate the policy enforcement layer without breaking active administrative sessions, the platform's database connection simulation subsystem (`Try Connection`) was initialized (`3.PNG`). An initial sanity-check authentication was executed to baseline successful end-user ingestion parameters prior to testing the blocking state (`4.PNG`).

#### 3. Interception Verification
With the updated policy successfully committed (`5.PNG`), a testing routine was initialized again. As engineered, the Identity Provider successfully intercepted the user lifecycle post-password validation, blocking the authentication loop and presenting an immutable cryptographic enrollment challenge (`6.PNG`). After successfully handling the security check, the transaction completed with updated claims metadata (`7.PNG`).

---

### 📊 Technical Evidence (MFA Enforcement)

Below is the structured walkthrough of the project implementation using the recorded audit trail:

| Step | Objective | Technical Action | Visual Reference |
| :--- | :--- | :--- | :--- |
| **01** | Enable OTP Factor | Toggled Authenticator App factor to an active state. | ![OTP Factor Activation]<img width="1037" height="141" alt="1" src="https://github.com/user-attachments/assets/be5b0f2c-f3c9-484c-ad3b-2302a1ce8dd4" /> |
| **02** | Configure Governance Policy | Bound the tenant to require a second factor on every transaction. | ![Always Require Policy Configuration]<img width="842" height="448" alt="2" src="https://github.com/user-attachments/assets/b9adc0e0-1e09-4ec7-83b0-19534702b842" /> |
| **03** | Sandbox Initialization | Initialized the IdP directory transaction tool (`Try Connection`). | ![Database Connection Trial Launch]<img width="903" height="205" alt="3" src="https://github.com/user-attachments/assets/d765ee70-a3e3-458f-b036-71e6eb43b7b6" /> |
| **04** | Baseline Test | Confirmed normal user profile mapping prior to strict policy enforcement. | <img width="733" height="554" alt="4" src="https://github.com/user-attachments/assets/cb3f352d-678b-4025-b565-e501a8a9dc2d" /> |
| **05** | Policy Update Enforcement | Validated that the global multi-factor constraints were securely deployed. | ![Policy State Verification]<img width="897" height="438" alt="5" src="https://github.com/user-attachments/assets/9514aa67-72b1-4a0d-818c-a87c0ec6da57" /> |
| **06** | Universal Login Interception | Verified the operational security layer actively forcing TOTP enrollment. | ![MFA QR Code Enrollment Prompt]<img width="505" height="641" alt="6" src="https://github.com/user-attachments/assets/c38dd6c5-e50b-4c50-838a-520ab2762a74" /> |
| **07** | Transaction Resolution | Confirmed identity validation completeness after processing the flow. | <img width="747" height="510" alt="7" src="https://github.com/user-attachments/assets/b4cb701d-d8bc-481b-94e0-de25ec2b4c25" /> |

---

### 📈 Next Steps for this Sandbox
* [ ] Federate a test application for Single Sign-On (SSO) workflows using OIDC/SAML protocols.
* [ ] Implement conditional access policies to trigger step-up authentication based on risk vectors.
