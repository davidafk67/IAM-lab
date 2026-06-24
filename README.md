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
| **01** | Enable OTP Factor | Toggled Authenticator App factor to an active state. | <img width="1037" height="141" alt="1" src="https://github.com/user-attachments/assets/be5b0f2c-f3c9-484c-ad3b-2302a1ce8dd4" /> |
| **02** | Configure Governance Policy | Bound the tenant to require a second factor on every transaction. | <img width="842" height="448" alt="2" src="https://github.com/user-attachments/assets/b9adc0e0-1e09-4ec7-83b0-19534702b842" /> |
| **03** | Sandbox Initialization | Initialized the IdP directory transaction tool (`Try Connection`). | <img width="903" height="205" alt="3" src="https://github.com/user-attachments/assets/e541824b-a48d-47cc-9ca9-3a51bec9cc02" /> |
| **04** | Baseline Test | Confirmed normal user profile mapping prior to strict policy enforcement. | <img width="733" height="554" alt="4" src="https://github.com/user-attachments/assets/cb3f352d-678b-4025-b565-e501a8a9dc2d" /> |
| **05** | Policy Update Enforcement | Validated that the global multi-factor constraints were securely deployed. | <img width="897" height="438" alt="5" src="https://github.com/user-attachments/assets/9514aa67-72b1-4a0d-818c-a87c0ec6da57" /> |
| **06** | Universal Login Interception | Verified the operational security layer actively forcing TOTP enrollment. | <img width="505" height="641" alt="6" src="https://github.com/user-attachments/assets/c38dd6c5-e50b-4c50-838a-520ab2762a74" /> |
| **07** | Transaction Resolution | Confirmed identity validation completeness after processing the flow. | <img width="747" height="510" alt="7" src="https://github.com/user-attachments/assets/b4cb701d-d8bc-481b-94e0-de25ec2b4c25" /> |

---

### 📈 Next Steps for this Sandbox
* [ ] Federate a test application for Single Sign-On (SSO) workflows using OIDC/SAML protocols.
* [ ] Implement conditional access policies to trigger step-up authentication based on risk vectors.

## 🛡️ Project 03: Federating a Web Application for OIDC Single Sign-On (SSO) & MFA Validation

### 📝 Project Overview
This project demonstrates the complete federation of a local **Python Flask** web application (acting as the Service Provider or SP) with **Auth0** (acting as the Identity Provider or IdP). The objective was to implement a secure **Single Sign-On (SSO)** architecture under the **OpenID Connect (OIDC)** and OAuth 2.0 frameworks, ensuring that downstream services natively inherit global tenant security policies (such as MFA) without altering the application's monolithic source code.

### 🛠️ Core Skills & Concepts Applied
* **Federated Identity & SSO:** Outsourcing authentication loops to a centralized cloud Identity Provider.
* **OIDC Cryptographic Handshake:** Utilizing `Client ID` and `Client Secret` tokens for secure back-channel validation.
* **Environment Configuration & Decoupling:** Managing sensitive credentials through secure runtime environments (`python-dotenv`) to prevent hardcoding risks.
* **Advanced Token Analysis & Troubleshooting:** Investigating HTTP 500 error states and parsing OIDC ID Tokens for cryptographic verification claims (`amr`).

---

### 🚀 Implementation Phases

#### 1. Identity Provider Service Provisioning
A dedicated client descriptor profile named **OnFlame** was provisioned inside the Auth0 Dashboard as a *Regular Web Application*. During this phase, security boundaries were established by locking allowed callback targets strictly to the application's local runtime interface (`http://localhost:3000/callback`).

#### 2. Service Provider Initialization & Environment Hardening
The application microservice template was deployed locally. Dependencies, including the secure OAuth integration engine (`authlib`) and the environment injection parser (`python-dotenv`), were compiled natively via the package manager:
```bash
pip install -r requirements.txt
The application core was architecture-designed to extract identity properties from the local runtime stack, leveraging the find_dotenv() loop to keep credentials fully isolated from the codebase.3. Execution, Error Ingestion & TroubleshootingUpon initializing the backend engine using python server.py, an immediate structural breakdown occurred when routing transactions to /login, triggering consecutive HTTP 500 Internal Server Error breaks.Two root causes were successfully isolated and resolved through technical auditing:IDE Enforcement Constraints: The development suite actively blocked automatic context injection, throwing a terminal environment injection is disabled fault. This required shifting execution paths to use absolute localized file targets.Extension Mismatch (Plantilla Error): The upstream repository bundled configuration parameters inside a .env.example template. Because of the .example extension, the initialization framework parsed values as null (None), breaking metadata synchronization. Renaming the asset strictly to .env resolved the handshake.📊 Technical Evidence (Application Federation)Below is the chronological execution path validating the federation loop from initial dependency staging to identity validation:StepObjectiveTechnical Action / Log StateVisual Reference01Dependency StagingCompiled authlib and python-dotenv packages into the local ecosystem.02Microservice BootstrapInitialized the local Flask daemon bound to interface port 3000.03Interface BaselineAccessed the root edge mapping an unauthenticated state (Welcome Guest).04Handshake Failure (Audit)Intercepted an HTTP 500 crash caused by null variables from .env.example.05IDE Context BlockIsolated a secondary workspace block preventing console runtime injection.06IdP InterceptionApplied environment patches; application successfully delegated routing to the Auth0 login portal.07Step-Up Policy CheckVerified the application natively inherited the MFA / TOTP boundary engineered in Project 02.08Payload ParsingResolved transaction; the token returned an authenticated state exposing verified profile metadata.🔍 Cryptographic Validation (ID Token Claim Audit)Upon successful authentication resolution, the cryptographic payload signature returned by the Identity Provider was audited to verify enforcement compliance:JSON{
  "userinfo": {
    "acr": "[http://schemas.openid.net/pape/policies/2007/06/multi-factor](http://schemas.openid.net/pape/policies/2007/06/multi-factor)",
    "amr": [
      "mfa"
    ],
    "email": "milechitac@gmail.com",
    "email_verified": true
  }
}
"amr": ["mfa"] Claim: The Authentication Methods Reference claim provides strict, immutable cryptographic proof that the downstream service provider successfully intercepted the identity loop and verified the secondary TOTP factor before granting authorization.📈 Next Steps for this Sandbox[ ] Automate user provisioning using Python scripts via the Auth0 Management API.[ ] Implement OAuth 2.0 Scopes to enforce fine-grained API Authorization boundaries.
