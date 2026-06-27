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

```

The application core was architecture-designed to extract identity properties from the local runtime stack, leveraging the `find_dotenv()` loop to keep credentials fully isolated from the codebase.

#### 3. Execution, Error Ingestion & Troubleshooting

Upon initializing the backend engine using `python server.py`, an immediate structural breakdown occurred when routing transactions to `/login`, triggering consecutive **HTTP 500 Internal Server Error** breaks.

Two root causes were successfully isolated and resolved through technical auditing:

* **IDE Enforcement Constraints:** The development suite actively blocked automatic context injection, throwing a `terminal environment injection is disabled` fault. This required shifting execution paths to use absolute localized file targets.
* **Extension Mismatch (Plantilla Error):** The upstream repository bundled configuration parameters inside a `.env.example` template. Because of the `.example` extension, the initialization framework parsed values as null (`None`), breaking metadata synchronization. Renaming the asset strictly to `.env` resolved the handshake.

---

### 📊 Technical Evidence (Application Federation)

Below is the chronological execution path validating the federation loop from initial dependency staging to identity validation:

| Step | Objective | Technical Action / Log State | Visual Reference |
| --- | --- | --- | --- |
| **01** | Dependency Staging | Compiled `authlib` and `python-dotenv` packages into the local ecosystem. | <img width="674" height="341" alt="16" src="https://github.com/user-attachments/assets/7ff6276b-3984-41a0-80d3-f309239aed74" /> |
| **02** | Microservice Bootstrap | Initialized the local Flask daemon bound to interface port `3000`. | <img width="666" height="231" alt="17" src="https://github.com/user-attachments/assets/1b8aeeb1-1883-48a9-8051-45bdb10b1940" /> |
| **03** | Interface Baseline | Accessed the root edge mapping an unauthenticated state (`Welcome Guest`). | <img width="494" height="194" alt="12" src="https://github.com/user-attachments/assets/0a643b30-1e28-4dcb-bfa9-b8ac0d02885c" /> |
| **04** | Handshake Failure (Audit) | Intercepted an **HTTP 500** crash caused by null variables from `.env.example`. | <img width="488" height="240" alt="18" src="https://github.com/user-attachments/assets/3ccc9c02-944c-4d9a-8682-658b95061406" /> |
| **05** | IDE Context Block | Isolated a secondary workspace block preventing console runtime injection. | <img width="440" height="115" alt="19" src="https://github.com/user-attachments/assets/92678e98-8443-4703-a20c-9cdbda97a8f3" /> |
| **06** | IdP Interception | Applied environment patches; application successfully delegated routing to the Auth0 login portal. | <img width="480" height="475" alt="13" src="https://github.com/user-attachments/assets/8e8dfc92-8bce-43bf-9cd7-8e5008e75a75" /> |
| **07** | Step-Up Policy Check | Verified the application natively inherited the **MFA / TOTP** boundary engineered in Project 02. | <img width="471" height="412" alt="14" src="https://github.com/user-attachments/assets/802f70e8-29a2-41e3-8c84-522ae9fa92db" /> |
| **08** | Payload Parsing | Resolved transaction; the token returned an authenticated state exposing verified profile metadata. | <img width="1366" height="626" alt="15" src="https://github.com/user-attachments/assets/ec3b1de7-e54f-494a-a352-6d70d01b7cfd" /> |

---

### 🔍 Cryptographic Validation (ID Token Claim Audit)

Upon successful authentication resolution, the cryptographic payload signature returned by the Identity Provider was audited to verify enforcement compliance:

```json
{
  "userinfo": {
    "acr": "[http://schemas.openid.net/pape/policies/2007/06/multi-factor](http://schemas.openid.net/pape/policies/2007/06/multi-factor)",
    "amr": [
      "mfa"
    ],
    "email": "example@gmail.com",
    "email_verified": true
  }
}

```

* **`"amr": ["mfa"]` Claim:** The *Authentication Methods Reference* claim provides strict, immutable cryptographic proof that the downstream service provider successfully intercepted the identity loop and verified the secondary TOTP factor before granting authorization.

---

### 📈 Next Steps for this Sandbox

* [ ] Automate user provisioning using Python scripts via the Auth0 Management API.
* [ ] Implement OAuth 2.0 Scopes to enforce fine-grained API Authorization boundaries.


## 🛡️ Project 04: Engineering Fine-Grained RBAC & API Authorization Limits via OAuth 2.0 Scopes

### 📝 Project Overview
This project demonstrates the transition from basic identity verification (Authentication) to strict resource control (Authorization). By deploying a **Role-Based Access Control (RBAC)** architecture, a local Python Flask web application was configured to act as a secure **Resource Server**. The backend microservice was hardened using custom Python middleware to parse cryptographically signed Access Tokens, intercept incoming HTTP traffic, and enforce access boundaries based on custom OAuth 2.0 claims (`scopes`), successfully mitigating privilege creep.

### 🛠️ Core Skills & Concepts Applied
* **API Access Management:** Registering cryptographic resource servers to decouple business logic permissions from the Identity Provider.
* **OAuth 2.0 Scope Enforcement:** Requesting and verifying granular permissions (`read:admin-dashboard`) within active runtime sessions.
* **Python Metaprogramming (Decorators):** Engineering reusable security middleware functions (`@requires_scope`) to protect application routing layers.
* **Advanced Code Auditing & Troubleshooting:** Resolving cross-origin trust failures, handling client assignment mismatches, and managing HTTP 403 vs 404 response states.

---

### 🚀 Implementation Phases

#### 1. Identity Provider API & Role Architecture
A dedicated Resource Server representing the internal enterprise API (`https://onflame.api`) was provisioned inside the Identity Provider (IdP) control panel. Two structural user roles were engineered to test the directory boundary:
* **`Admin`:** Bound tightly to the custom administrative scope entitlement (`read:admin-dashboard`).
* **`Employee`:** Maintained as a baseline security boundary without specialized permissions.

#### 2. Middleware Implementation & Environment Configuration
The Python Flask backend was refactored to register the remote audience identifier inside the runtime system state. To enforce these constraints programmatically without polluting local business routing logic, a custom Python decorator function was engineered to inspect the encrypted runtime data pipeline:

```python
def requires_scope(required_scope):
    def decorator(f):
        @wraps(f)
        def decorated(*args, **kwargs):
            user = session.get("user")
            if not user:
                return redirect(url_for("login"))
            user_scopes = user.get("scope", "")
            if required_scope not in user_scopes.split():
                abort(403)
            return f(*args, **kwargs)
        return decorated
    return decorator

```

#### 3. Forensic Debugging & Handshake Troubleshooting

During the integration loop, several operational breakdowns occurred and were systematically resolved through logging analysis:

* **The `abort` Name Resolution Fault:** The IDE static analyzer caught an undefined variable block due to a missing framework import, requiring an update to the core Flask import declaration.
* **The Architecture Freezing Block (HTTP 404 Error):** Protected endpoints were initially appended below the server lifecycle listener invocation (`app.run`), rendering the operational hooks invisible to the daemon routing tree. Re-ordering core controller definitions resolved the system visibility block.
* **The API Access Client Trust Mismatch (OAuthError):** The local framework failed the back-channel exchange protocol, throwing an `invalid_request: Client is not authorized to access resource server` exception. This was fixed by modifying the Auth0 console to authorize the Client App profile to request tokens from the newly generated API resource plane.

---

### 📊 Technical Evidence (Chronological Implementation & Verification)

Below is the structured walkthrough of the authorization enforcement loop and token claim behavior using the recorded audit trail:

| Step | Objective | Technical Action / Log State | Visual Reference |
| --- | --- | --- | --- |
| **01** | **Role Engineering** | Generated the custom `Admin` containment boundary inside the User Management module. | <img width="846" height="299" alt="1" src="https://github.com/user-attachments/assets/aaa7719d-2520-4672-8fe7-95b237a54748" /> |
| **02** | **Permission Assignment** | Mapped the granular `read:admin-dashboard` scope from the Resource Server into the Admin role matrix. | <img width="795" height="474" alt="2" src="https://github.com/user-attachments/assets/ca1c730d-6a99-4dd6-88cf-8b501907aa92" /> |
| **03** | **Identity Assignment** | Provisioned the test users and bound the target account to the newly deployed administrative profile. | <img width="468" height="396" alt="3" src="https://github.com/user-attachments/assets/15389e23-79d1-4183-8a2d-9bb10d098daa" /> |
| **04** | **Static IDE Analysis** | Caught and corrected an undefined reference exception (`"abort" is not defined`) inside the decorator logic. | <img width="1148" height="448" alt="8862302b-fa16-4d41-a95f-5e45de2854af" src="https://github.com/user-attachments/assets/9e9d3d60-e98b-44a2-bfbc-dc562029e5a9" /> |
| **05** | **Application Freeze Audit** | Isolated an HTTP 404 routing failure caused by placing controllers below the live system execution block. | <img width="631" height="423" alt="cea60d21-525c-41df-9d34-729ae781235c" src="https://github.com/user-attachments/assets/433e0df3-236a-4a58-b897-76bcca76b3a6" /> |
| **06** | **Handshake Trust Breakdown** | Intercepted an `OAuthError (invalid_request)` during the OIDC callback loop due to an unauthorized API relation. | <img width="1366" height="711" alt="13c57cdb-619a-42aa-8fc0-6c5aadf7a706" src="https://github.com/user-attachments/assets/89ba024b-6cbe-443d-ae75-5f7ae715b335" /> |
| **07** | **Client API Authorization** | Linked the OIDC application client to the Resource Server plane, authorizing the scope transmission. | <img width="496" height="366" alt="11" src="https://github.com/user-attachments/assets/7ddcb506-c869-4726-bd06-3f3091559e8a" /> |
| **08** | **Unprivileged Token Ingestion** | User with employee role resolved authentication successfully; payload structure was strictly limited to default profile scopes. | <img width="511" height="509" alt="d61e0d1c-f10c-4ae3-8c33-68ff8ee5a47c" src="https://github.com/user-attachments/assets/ecbb1853-f753-454a-8f84-c6f5d8edf66e" /> |
| **09** | **Privileged Token Ingestion** | User admin role completed the loop; the IdP successfully appended the elevated permission: `"scope": "... read:admin-dashboard"`. | <img width="513" height="513" alt="49c88592-6885-42d2-b162-0318aeb031bf" src="https://github.com/user-attachments/assets/916cb8a5-daa0-4da1-9088-ea233f6b4b3f" /> |
| **10** | **Perimeter Enforcement Test** | The unprivileged account attempted a forced URL traversal attack to `/admin`. The backend middleware intercepted the transaction and threw an **HTTP 403 Forbidden** block. | <img width="600" height="195" alt="23" src="https://github.com/user-attachments/assets/3df4365e-75f9-4cf3-b462-9a7920fb7afd" /> |
| **11** | **Access Resolution Validation** | The privileged account navigated to the restricted zone. The middleware validated the signature token, granting entry to the critical zone. | <img width="569" height="180" alt="22" src="https://github.com/user-attachments/assets/b1b195bd-b230-4551-9f7a-76eae8c766f5" /> |

---

### 📈 Next Steps for this Sandbox

* [ ] Shift from static local user management to programmatic **Identity Lifecycle Management** utilizing the Auth0 Management API.
* [ ] Automate user ingestion models (*Joiner/Mover/Leaver Scenarios*) using independent Python administrative tool scripts.




