# ISO/IEC 27001:2022 + GDPR Compliance Assessment

**Fictional Digital Payment Application — EuroPay**

*Self-Directed GRC Portfolio Project by Ketaki Chavan*

---

## Executive Summary

This report documents a self-driven Governance, Risk & Compliance (GRC) assessment conducted against **EuroPay**, a fictional online payment application, using **ISO/IEC 27001:2022** and the **EU General Data Protection Regulation (GDPR)** as the governing frameworks. The purpose of the assessment is to demonstrate, in a realistic and audit-ready format, how information security and data protection compliance are implemented, evidenced, and reported within a financial technology environment.

The assessment identifies **seven information security risks** spanning authentication, application security, insider threat, cloud configuration, supplier dependency, and operational resilience. Each risk is scored using a defined likelihood/impact methodology, mapped to relevant ISO/IEC 27001:2022 Annex A controls, and assigned a treatment plan with a resulting residual risk rating. In parallel, a GDPR data inventory, lawful-basis mapping, and Data Protection Impact Assessment (DPIA) were produced to evaluate the privacy implications of processing financial and personal data.

The assessment concludes that EuroPay's control environment, once the recommended treatments are applied, reduces residual risk to a **Medium-or-lower** level across all identified risks, which is considered acceptable for the scope of this exercise provided ongoing monitoring, periodic reassessment, and annual DPIA review are maintained. Two follow-up actions are recommended: formalizing a tested business-continuity plan (ISO control A.5.30) and strengthening the documented process for handling data subject access requests.

---

## 1.0 Introduction

This project is a self-driven, beginner-to-intermediate level GRC assessment conducted on EuroPay, a fictional online payment application created for the purposes of this exercise. The objective is to practically apply ISO/IEC 27001:2022 and GDPR concepts in a realistic scenario, producing the same set of artefacts an internal audit or compliance function would be expected to deliver: a risk register, a GDPR data inventory, a DPIA, foundational policies, a Statement of Applicability, and a final management report.

Payment applications sit at the intersection of high regulatory scrutiny and high attacker interest, since they combine sensitive personal data with direct financial value. This makes EuroPay a useful vehicle for demonstrating how structured GRC practice supports audit readiness, risk reduction, and regulatory compliance in a financial-services context.

### 1.1 Objectives

- Perform a structured ISO/IEC 27001:2022 risk assessment focused on payment-related threats such as account compromise, transaction manipulation, and data exposure.
- Identify key information security risks in a payment system, including financial data leakage, fraud, unauthorized access, and transactional integrity issues.
- Map identified risks to ISO/IEC 27001:2022 Annex A controls relevant to payment operations, sensitive financial data, and system security requirements.
- Build a GDPR data inventory for personal and transaction data, specifying lawful basis for processing, retention periods, and storage locations.
- Conduct a Data Protection Impact Assessment for high-risk financial processing, including necessity and proportionality considerations.
- Draft foundational Information Security and Data Protection policies tailored to a payment-application context.
- Prepare a Statement of Applicability reflecting applied, partially applied, and not-applicable controls, each with a documented rationale.

### 1.2 Assumptions

- The assessment is conducted as an internal audit exercise on EuroPay, performed under a Lead Auditor's guidance.
- Findings are reported to a higher authority (senior management / audit committee); corrective actions are implemented by the project team.
- The assessment represents one cycle within a continuous compliance review process, not a one-off exercise.
- EuroPay is assumed to operate entirely on cloud infrastructure with no organization-owned physical data centre.

### 1.3 Key Deliverables

- System overview document describing e-wallet and transaction workflows.
- ISO/IEC 27001 risk register and summary, including payment-specific threats and a defined scoring methodology.
- GDPR data mapping and retention schedule for account and transaction data.
- Data Protection Impact Assessment for high-risk financial transactions.
- Information Security Policy covering secure payments, MFA, encryption, and monitoring.
- Data Protection Policy covering user privacy and transaction confidentiality.
- Statement of Applicability for payment-related ISO controls, including justified exclusions.
- Final compliance assessment report for management review.

---

## 2.0 System Overview

### 2.1 Introduction

EuroPay is a digital payment application designed to allow users to send, receive, and track online payments. The platform provides e-wallet functionality, secure user authentication, account balance management, and transaction history. This overview supports the ISO 27001 and GDPR compliance assessment by establishing the application's data flows, technical environment, and processing activities, which form the foundation for the risk assessment, GDPR mapping, DPIA, and Statement of Applicability that follow.

### 2.2 Functional Capabilities

EuroPay enables registered users to:

- Sign up and log in to a personal account, protected by password and optional multi-factor authentication.
- Add funds to a digital wallet from a linked payment source.
- Send and receive peer-to-peer payments to other EuroPay users.
- View transaction history and current account balance.
- Receive notifications for successful, pending, or failed transactions.

### 2.3 High-Level Data Flow

At a conceptual level, a payment transaction flows as follows: a user authenticates through the mobile/web client, which communicates over TLS with the API gateway; the API gateway enforces rate-limiting and forwards authenticated requests to the Node.js REST API; the application layer validates the request, applies business logic (balance checks, fraud rules), and writes the transaction record to the PostgreSQL database; a notification service then informs both sender and receiver of the outcome. Security and access logs are generated at the gateway and application layer and streamed to a centralized logging service for monitoring and retention.

### 2.4 Data Processed

The application processes the following categories of personal and financial data:

- **Name** — used for account identification.
- **Email address** — used for authentication and notifications.
- **Phone number** — used for two-factor authentication (2FA) and account alerts.
- **Password hash (bcrypt)** — used for secure authentication; plaintext passwords are never stored.
- **Transaction data** — amount, timestamp, sender ID, receiver ID.
- **IP address and device metadata** — used for fraud monitoring and security logging.

### 2.5 Technical Environment

- **Backend:** Node.js REST API.
- **Database:** PostgreSQL, with column-level encryption for sensitive fields.
- **Infrastructure:** Hosted on EU-region cloud infrastructure under a shared-responsibility model.
- **Security measures:** TLS 1.2+ in transit, IAM roles for service-to-service access, database encryption at rest (AES-256), API gateway rate-limiting, and secure coding practices embedded in the SDLC.

This system overview provides the foundation for all subsequent compliance assessment activities, including risk assessment, GDPR mapping, DPIA, policy development, and Statement of Applicability preparation.

---

## 3.0 ISO/IEC 27001:2022 Risk Assessment

### 3.1 Methodology

The risk assessment follows a structured ISO/IEC 27001-aligned approach:

- **Identify assets** — e.g., user accounts, transaction data, backend systems, cloud storage.
- **Identify threats and vulnerabilities** — unauthorized access, fraud, system misconfiguration, supplier risk, availability loss.
- **Estimate likelihood and impact** — considering financial, reputational, operational, and regulatory consequences.
- **Map relevant ISO/IEC 27001:2022 Annex A controls** — controls applied to mitigate each identified risk.
- **Apply risk treatment** — technical, procedural, and monitoring measures to reduce risk to an acceptable residual level.

#### 3.1.1 Likelihood and Impact Scale

Likelihood and impact are each rated on a three-point scale (Low / Medium / High):

- **Likelihood** — Low: unlikely without a significant, coordinated effort by an attacker or a rare operational failure. Medium: plausible given known attack patterns against similar applications or realistic human error. High: expected to occur without additional controls, based on prevalence in comparable systems.
- **Impact** — Low: limited, easily contained effect on a small number of users or non-sensitive data. Medium: financial loss, service disruption, or exposure of personal data affecting a limited user group. High: material financial loss, exposure of financial/transaction data at scale, regulatory notification obligations, or reputational damage.

Inherent risk (before treatment) is derived from the combination of likelihood and impact using the matrix below; residual risk (after treatment) is then re-assessed against the same matrix based on the estimated effect of the applied controls.

| Likelihood \ Impact | Low | Medium | High |
|---|---|---|---|
| **High** | Medium | High | Critical |
| **Medium** | Low | Medium | High |
| **Low** | Low | Low | Medium |

### 3.2 Risk Register

The table below summarizes the seven risks identified during this assessment, their inherent and residual ratings, the ISO/IEC 27001:2022 Annex A controls applied, and the specific treatment implemented for each.

| Risk ID | Risk Description | Likelihood | Impact | Inherent Risk | ISO 27001 Controls | Treatment / Mitigation | Residual Risk |
|---|---|---|---|---|---|---|---|
| **R1** | Unauthorized wallet/account access due to weak or reused passwords, enabling fraudulent transactions | Medium | High | High | A.5.17 Logging; A.8.2 Access Control | Enforce MFA, strong password policy, brute-force lockouts, periodic access reviews | Medium |
| **R2** | API abuse enabling transaction manipulation or replay due to weak rate-limiting or integrity checks | Medium | High | High | A.8.12 Encryption; A.5.7 Secure SDLC | TLS 1.2+, HMAC request signing, API throttling, strict input validation | Medium |
| **R3** | SQL injection exposing the payment database due to insufficient input validation | Low | High | Medium | A.8.8 Secure Coding; A.5.20 Data Leakage Prevention | Parameterized queries, WAF, static/dynamic code scanning, secure SDLC gates | Medium |
| **R4** | Insider misuse or excessive privileges on admin dashboards / database access | Low | Medium | Medium | A.8.2 RBAC; A.8.16 Monitoring | RBAC, least privilege, quarterly privilege reviews, MFA for admins | Low |
| **R5** | Data leakage via misconfigured cloud storage (e.g., public S3-style buckets) or log repositories | Low | Medium | Medium | A.5.20 Data Leakage Prevention; A.8.12 Encryption | Private-by-default buckets, encryption at rest, periodic configuration audits | Low |
| **R6** | Third-party / supplier risk from the cloud hosting provider's shared-responsibility gaps | Low | Medium | Medium | A.5.10 Supplier Security; A.5.19 Supplier Relationships | Contractual security clauses, annual supplier security review, SOC 2 report review | Low |
| **R7** | Loss of transaction data availability due to inadequate backup or recovery procedures | Low | High | Medium | A.5.23 Information Backup; A.8.16 Monitoring | Daily backups, quarterly restore testing, documented disaster recovery plan | Low |

### 3.3 Risk Narratives

**R1 — Unauthorized Account Access**
Weak or reused user passwords could allow attackers to access user wallets or perform fraudulent transactions. This is treated by enforcing MFA, strong password policies, and brute-force protection, supported by A.5.17 (Logging) and A.8.2 (Access Control). The objective is to protect user authentication and transaction integrity for e-wallet operations.

**R2 — Transaction Manipulation Through API Abuse**
Payment APIs may be exploited if rate-limiting or integrity checks are weak, potentially allowing fraudulent or manipulated transactions. Treatment applies TLS encryption, HMAC validation, API throttling, and input validation, mapped to A.8.12 (Encryption) and A.5.7 (Secure SDLC), securing payment operations and maintaining integrity across backend services.

**R3 — Database Breach via SQL Injection**
Insufficient input validation could allow attackers to manipulate SQL queries, exposing sensitive financial and personal data. Treatment uses parameterized queries, a Web Application Firewall, and automated code scanning, mapped to A.8.8 (Secure Coding) and A.5.20 (Data Leakage Prevention), protecting stored transaction and account data and supporting GDPR confidentiality and integrity principles.

**R4 — Insider Threat / Excessive Privileges**
Admin dashboards or database access may allow employees to view or manipulate transaction data beyond their role. Treatment implements RBAC, logging, and regular privilege reviews, mapped to A.8.2 (RBAC) and A.8.16 (Monitoring), ensuring least privilege, monitoring, and accountability for payment data.

**R5 — Data Leakage via Misconfigured Storage**
Misconfigured cloud storage or log repositories could expose transaction or personal data. Treatment enforces private-by-default buckets, encryption at rest, and regular configuration audits, mapped to A.5.20 (Data Leakage Prevention) and A.8.12 (Encryption), protecting stored transaction data and aligning with GDPR retention and confidentiality requirements.

**R6 — Third-Party / Supplier Risk**
EuroPay depends on an external cloud provider for hosting under a shared-responsibility model; gaps in the provider's own controls could indirectly expose EuroPay data. Treatment includes contractual security clauses, an annual supplier security review, and review of the provider's SOC 2 report, mapped to A.5.10 (Supplier Security) and A.5.19 (Supplier Relationships).

**R7 — Loss of Transaction Data Availability**
Inadequate backup or recovery procedures could result in permanent loss of transaction or account records following an outage, ransomware event, or human error. Treatment applies daily backups, quarterly restore testing, and a documented disaster recovery plan, mapped to A.5.23 (Information Backup) and A.8.16 (Monitoring).

### 3.4 Overall Risk Posture

- **Current inherent risk level:** predominantly High-to-Medium across risks touching authentication, application security, and availability, reflecting the sensitivity of payment operations.
- **Residual risk after treatment:** reduced to Medium or Low across all seven risks, considered acceptable for the scope of this project provided periodic monitoring and reassessment are performed.
- **Reassessment cadence:** the risk register should be formally re-reviewed at least annually, or immediately following any material change to the application's architecture, threat landscape, or regulatory environment.

---

## 4.0 GDPR Data Mapping

### 4.1 Purpose

This GDPR data mapping was performed as part of the combined ISO 27001 + GDPR compliance assessment for EuroPay. The objective is to document personal data processing activities, identify lawful bases, define retention periods, and demonstrate accountability for high-risk financial data processing in line with GDPR requirements.

### 4.2 Personal Data Processed

EuroPay processes the following groups of personal data to support e-wallet and payment services:

- **Identification data:** name, email address, phone number.
- **Authentication data:** password hashes (bcrypt).
- **Financial transaction data:** amounts, timestamps, sender and receiver identifiers.
- **Technical and security data:** IP address, access logs, device metadata used for fraud detection and monitoring.

### 4.3 Roles and Responsibilities

- **Data Controller:** EuroPay — determines the purpose and means of processing.
- **Data Processor:** the EU-region cloud service provider, processing data under contractual and security obligations set out in a Data Processing Agreement (DPA).

### 4.4 Purpose of Processing

- Create and manage user accounts.
- Authenticate users and secure wallet access.
- Execute, record, and reconcile payment transactions.
- Detect fraud, prevent unauthorized access, and ensure transaction integrity.
- Meet financial, audit, and regulatory record-keeping requirements.

### 4.5 Lawful Basis (GDPR Article 6)

- **Art. 6(1)(b) — Contractual necessity:** account creation, login, wallet operations, and payment processing.
- **Art. 6(1)(f) — Legitimate interest:** fraud detection, security monitoring, and abuse prevention using IP and transaction logs, balanced against user privacy expectations via a documented legitimate-interest assessment.
- **Cookies:** only strictly necessary cookies are used, for session and security management; no consent-based tracking or advertising cookies are deployed.

### 4.6 Data Retention

- **Account data:** retained for the lifetime of the user account.
- **Transaction data:** retained for 5 years to meet accounting and financial compliance obligations.
- **Security logs and IP data:** retained for 30 days for monitoring and incident investigation, after which they are automatically purged.

### 4.7 Storage Location and Security Safeguards

- All data is stored within authorized EU-based cloud infrastructure, avoiding third-country transfer complications under GDPR Chapter V.
- Security controls include encryption at rest (AES-256), TLS 1.2+ in transit, role-based access control (RBAC), MFA for privileged access, logging, and continuous monitoring.
- Access is limited to authorized personnel on a least-privilege basis, reviewed quarterly.

### 4.8 Data Subject Rights

EuroPay supports the following data subject rights under GDPR Chapter III: right of access, right to rectification, right to erasure (subject to statutory retention obligations for transaction data), right to restriction of processing, and right to data portability. All verified requests are actioned within 30 days. This process is flagged in Section 9 as an area requiring further procedural strengthening — specifically, a documented identity-verification step and a tracked request log are recommended.

### 4.9 GDPR Data Inventory

| Data Category | Purpose | Lawful Basis (Art. 6) | Retention | Storage & Security |
|---|---|---|---|---|
| Name | Account identification | 6(1)(b) Contract | Account lifetime | EU cloud; AES-256; RBAC |
| Email address | Authentication, notifications | 6(1)(b) Contract | Account lifetime | EU cloud; TLS 1.2+; secure tokens |
| Phone number | 2FA, account alerts | 6(1)(b) Contract | Account lifetime | MFA; access logging |
| Password hash (bcrypt) | Authentication | 6(1)(b) Contract | Account lifetime | AES-256; RBAC; secure SDLC |
| Transaction data | Payments, reconciliation | 6(1)(b) Contract | 5 years | AES-256; TLS 1.2+; secure DB access |
| IP address / device metadata | Fraud detection, monitoring | 6(1)(f) Legitimate interest | 30 days | Access logs; monitoring; RBAC |
| Session cookies | Session management | 6(1)(b) Contract | Session lifetime | Encrypted; secure handling |

EuroPay's GDPR mapping ensures structured management of personal and financial data, supporting compliance with Article 5 principles — lawfulness, transparency, purpose limitation, data minimization, accuracy, storage limitation, and integrity/confidentiality. Combined with the ISO 27001 controls in Section 3, it strengthens overall risk mitigation for sensitive payment operations.

---

## 5.0 Data Protection Impact Assessment (DPIA)

### 5.1 Processing Description

EuroPay processes personal data and financial transaction data to deliver e-wallet and peer-to-peer payment services. Processing includes user onboarding and authentication, wallet balance management, transaction execution and recording, notifications, and security monitoring (e.g., fraud detection using IP address and access logs). Given the sensitivity of payment and account data, this DPIA assesses potential impacts on individuals' rights and freedoms and documents measures to reduce privacy risk, aligned to GDPR principles and ISO/IEC 27001:2022 controls.

### 5.2 Necessity and Proportionality

The processing described above is considered necessary because payment execution, fraud prevention, and regulatory record-keeping cannot be achieved without collecting identification, authentication, and transaction data. Data collection is limited to the minimum required for these purposes: no special-category data (e.g., health, biometric, or political data) is processed, and behavioural data (IP address, device metadata) is used solely for fraud detection rather than marketing or profiling. On this basis, the processing is assessed as proportionate to its stated purposes.

### 5.3 Consultation

As a self-driven training exercise with no live data subjects, external consultation with a Data Protection Officer or supervisory authority was not performed. In a production deployment, this DPIA would be reviewed by EuroPay's DPO prior to go-live, and the supervisory authority would be consulted under Article 36 if residual risk after mitigation remained High.

### 5.4 Identified Risks to Individuals

| Risk to Individual | Description | Likelihood | Severity | Mitigation |
|---|---|---|---|---|
| Unauthorized account access | Financial loss, unauthorized payments, loss of control over the account | Medium | High | MFA, strong password policy, brute-force protection |
| Identity misuse | Exposure or misuse of personal data (name, email, phone); phishing or account takeover | Low | High | Encryption, access controls, staff awareness training |
| Fraud & transaction manipulation | Incorrect transfers, disputes, financial harm, reduced trust | Medium | High | HMAC validation, rate limiting, anomaly detection |
| Behavioural profiling | Inferences from transaction patterns could reveal sensitive behaviour if misused | Low | Medium | Data minimization, purpose limitation, access restrictions on analytics |

### 5.5 Mitigation Measures

- **Authentication & access control:** MFA for privileged/admin access, RBAC, least privilege, strong password policy, brute-force protection, periodic access reviews.
- **Data security:** AES-256 encryption at rest, TLS 1.2+ in transit, EU-based hosting, secure key management, secure session handling.
- **Monitoring & fraud prevention:** centralized logging of admin and transaction events, audit trails, alerting and anomaly detection for suspicious activity.
- **Secure development:** secure SDLC, code scanning, peer review, parameterized queries/input validation, API integrity checks (HMAC), rate limiting.
- **Operational resilience:** backups and recovery procedures, quarterly restore testing, configuration reviews and hardening to reduce misconfiguration risk.

### 5.6 Residual Risk and Review

- **Residual risk:** Medium, acceptable for the scope of this project.
- Requires continuous monitoring, periodic reassessment, and an annual DPIA update, or sooner following a material change to processing activities.

EuroPay's DPIA demonstrates that privacy risks are mitigated through technical, procedural, and monitoring controls. Combined with the ISO 27001 risk treatments in Section 3 and the GDPR-aligned data practices in Section 4, the application supports secure handling of financial transactions and personal data while maintaining regulatory compliance.

---

## 6.0 Information Security Policy

### 6.1 Purpose
Protect personal and financial data processed by EuroPay, ensuring confidentiality, integrity, and availability in line with ISO/IEC 27001:2022 and GDPR.

### 6.2 Scope
This policy applies to all employees, contractors, systems, and cloud environments handling EuroPay data and services.

### 6.3 Access Control
- Role-Based Access Control (RBAC) for all users.
- Multi-Factor Authentication (MFA) for administrative accounts.
- Least privilege enforced; periodic reviews of roles and permissions.

### 6.4 Authentication
- Passwords hashed using bcrypt; plaintext passwords are never stored or logged.
- Brute-force protection for login and API endpoints.
- Secure session management with time-limited tokens.

### 6.5 Data Security & Encryption
- AES-256 encryption for data at rest.
- TLS 1.2+ for data in transit.
- EU-based cloud storage; regular configuration audits.

### 6.6 Logging & Monitoring
- All transactions and admin events logged.
- Logs retained 30 days; monitored for suspicious activity.
- Alerts configured for abnormal or fraudulent events.

### 6.7 Secure Development Lifecycle (SDLC)
- Secure coding practices to prevent SQL injection and related vulnerabilities.
- Code scanning, peer reviews, and automated testing applied before release.
- API security via HMAC signatures and rate-limiting.

### 6.8 Backup & Recovery
- Daily backups of transactional and account data.
- Quarterly restore testing.
- Disaster recovery plans maintained and updated.

### 6.9 Incident Management
- Security incidents classified and responded to within 24 hours.
- Breaches reported to the supervisory authority within 72 hours where GDPR notification thresholds are met.
- Lessons learned documented; corrective actions implemented and tracked to closure.

### 6.10 Compliance & Training
- Staff trained on ISO 27001 and GDPR requirements at onboarding and annually thereafter.
- Continuous monitoring and periodic internal audits conducted.
- Policy reviewed annually or when major changes occur.

---

## 7.0 Data Protection Policy

### 7.1 Purpose
Ensure that personal and financial data processed by EuroPay is handled lawfully, transparently, and securely, in compliance with GDPR and aligned with ISO 27001 principles.

### 7.2 Scope
This policy applies to all employees, contractors, systems, and cloud environments involved in EuroPay operations, including account management, payment processing, and transaction monitoring.

### 7.3 GDPR Principles
EuroPay commits to:

- **Lawfulness, fairness, and transparency:** data is processed for legitimate, clearly communicated purposes.
- **Data minimization:** only necessary personal and transaction data is collected.
- **Purpose limitation:** data is used solely for account management, payments, fraud prevention, and compliance.
- **Accuracy:** data is kept accurate and up to date, with correction mechanisms available to users.
- **Storage limitation:** data is retained only as required for operational, accounting, and regulatory purposes.
- **Integrity & confidentiality:** data is protected using the technical and organizational controls described in Section 6.

### 7.4 Data Subject Rights
Users may request access to their personal data, correction or deletion of inaccurate data, or restriction of processing. All requests are addressed within 30 days in line with GDPR, following identity verification and a logged request-tracking process.

### 7.5 Data Retention
- **Account data:** retained for the lifetime of the user account.
- **Transaction data:** retained 5 years for accounting and regulatory compliance.
- **Logs and IP data:** retained 30 days for monitoring, fraud detection, and incident investigation.

### 7.6 Security Measures
- Encryption at rest (AES-256) and in transit (TLS 1.2+).
- Multi-Factor Authentication (MFA) for privileged access.
- Role-Based Access Control (RBAC) and least-privilege principle.
- Logging, auditing, and monitoring for suspicious activity.
- SDLC controls including code scanning, peer review, and input validation.

### 7.7 Roles and Responsibilities
- **Data Controller:** EuroPay — defines purposes and means of processing.
- **Data Processor:** EU-based cloud provider — processes data under contractual obligations set out in a DPA.
- **Staff & contractors:** must follow data protection policies, report breaches promptly, and comply with GDPR requirements.

### 7.8 Compliance & Review
- Continuous monitoring of data processing activities and security controls.
- Periodic audits and DPIA updates for high-risk financial processing.
- Policy reviewed annually or upon major system or regulatory changes.

---

## 8.0 Statement of Applicability (SoA)

### 8.1 Scope

This Statement of Applicability documents the ISO/IEC 27001:2022 Annex A controls selected — or explicitly excluded — for EuroPay, covering e-wallet operations, peer-to-peer payments, and the processing of personal and financial transaction data. Controls are selected to address the key risks identified in Section 3, including unauthorized access, API abuse, SQL injection, insider misuse, cloud misconfiguration, supplier risk, and availability loss.

### 8.2 Applicability Table

| Control | Applied? | Reason / Context |
|---|---|---|
| A.5.7 Secure SDLC | Yes | Reduces application-layer risk in payment APIs through secure design, code review, scanning and testing; mitigates injection and broken access control. |
| A.5.10 Supplier Security | Yes | EuroPay relies on an EU-based cloud provider under a shared-responsibility model; contractual security obligations manage third-party risk. |
| A.5.17 Logging | Yes | Supports transaction traceability, fraud investigation, and auditability of account/admin activity. |
| A.5.19 Information Security in Supplier Relationships | Yes | Formalizes security expectations and review cadence with the cloud hosting provider and any payment-processing partners. |
| A.5.20 Data Leakage Prevention | Yes | Prevents unauthorized disclosure of personal and transaction data from storage misconfiguration or excessive access. |
| A.5.23 Information Backup | Yes | Protects availability and integrity of account and transaction records via daily backups and quarterly restore testing. |
| A.8.2 Privileged Access Rights / Access Control | Yes | RBAC and least privilege reduce unauthorized access risk; MFA required for privileged/admin operations. |
| A.8.8 Secure Coding | Yes | Parameterized queries and input validation reduce SQL injection and API vulnerability risk in the Node.js backend. |
| A.8.12 Data Encryption | Yes | AES-256 at rest and TLS 1.2+ in transit protect confidentiality of personal and financial data. |
| A.8.16 Monitoring Activities | Yes | Enables detection of abnormal behaviour and timely response to suspicious transactions and security events. |
| A.7 Physical Security controls (A.7.1–A.7.14) | **No** | Not applicable — EuroPay is fully hosted on cloud infrastructure with no organization-owned data centre or physical premises housing in-scope systems. |
| A.5.30 ICT Readiness for Business Continuity | **Partially** | Backup and restore testing are in place; a formal, tested business-continuity plan covering full service outage scenarios is not yet documented and is recommended as a follow-up action. |
| A.8.23 Web Filtering | **No** | Not applicable to this assessment scope — EuroPay's risk surface is API/backend-focused rather than end-user web-browsing within a corporate network. |

### 8.3 Residual Risk Management

- **Residual risk level:** Medium, acceptable for the project scope after applying the controls above.
- **Ongoing monitoring:** continuous logging/monitoring of transactions and privileged activity, with alerts for anomalous behaviour.
- **Review cadence:** periodic risk reassessment and annual DPIA updates, or earlier following major changes to processing, architecture, or the threat landscape.
- **Key mitigations in place:** MFA, RBAC/least privilege, encryption, logging and monitoring, secure SDLC, and fraud/anomaly detection controls.
- **Open follow-up action:** formalize and test a business-continuity plan to fully satisfy A.5.30, currently only partially applied via backup/restore testing.

---

## 9.0 Final Compliance Assessment Report

### 9.1 Assessment Scope
A combined ISO/IEC 27001:2022 and GDPR compliance assessment of EuroPay, a fictional payment application, covering e-wallet operations, peer-to-peer payments, personal data, and transaction metadata.

### 9.2 Objectives
- Identify high-level information security and privacy risks.
- Map risks to ISO 27001 Annex A controls.
- Evaluate GDPR compliance, including lawful basis, retention, and data subject rights.
- Conduct a DPIA for high-risk financial processing, including necessity and proportionality analysis.
- Review policies and prepare a Statement of Applicability.

### 9.3 ISO 27001 Risk Assessment Summary
- **High-risk areas identified:** unauthorized account access, API abuse, SQL injection, insider misuse, misconfigured storage, supplier dependency, backup/availability gaps.
- **Controls implemented:** MFA, RBAC, AES-256 encryption, TLS 1.2+, logging & monitoring, secure SDLC, supplier security review, backup & recovery.
- **Residual risk:** Medium or lower across all seven risks; acceptable with ongoing monitoring and periodic reassessment.

### 9.4 GDPR Assessment Summary
- **Personal data processed:** identification data (name, email, phone), authentication data (password hashes), transaction data, IP and device metadata.
- **Lawful basis:** Art. 6(1)(b) contractual necessity; Art. 6(1)(f) legitimate interest for fraud detection.
- **Retention:** account data — lifetime; transaction data — 5 years; logs/IP data — 30 days.
- **Compliance gap identified:** the process for handling data subject access requests lacks a documented identity-verification step and a formal request-tracking log; both are recommended before production deployment. Aside from this gap, GDPR practices align with the Article 5 principles.

### 9.5 DPIA Summary
- **Identified risks:** unauthorized access, identity misuse, fraud, behavioural profiling.
- **Necessity/proportionality:** processing assessed as necessary and proportionate; no special-category data involved.
- **Mitigations:** encryption, MFA, RBAC, logging, monitoring, secure SDLC, backups.
- **Residual risk:** Medium; acceptable with continuous monitoring and annual updates.

### 9.6 Policies & SoA Summary
- **Information Security Policy:** defines access, authentication, encryption, logging, SDLC, backup, incident management, and training requirements.
- **Data Protection Policy:** defines GDPR principles, data subject rights, retention, storage safeguards, and compliance responsibilities.
- **Statement of Applicability:** 10 Annex A controls applied, 1 partially applied, 2 marked not applicable with documented justification; residual risks monitored continuously.

### 9.7 Conclusions & Recommendations
- EuroPay demonstrates a reasonably strong security and privacy posture for a fictional payment application built and assessed within a constrained project scope.
- The seven identified risks are mitigated to a Medium-or-lower residual level through technical, procedural, and monitoring controls, each traceable to a specific Annex A control.
- GDPR compliance is generally robust, with one concrete improvement area: formalizing the data subject request process.
- A secondary recommendation is to formalize and test a full business-continuity plan to move A.5.30 from partially applied to fully applied.
- Continuous monitoring, annual DPIA updates, periodic security audits, and maintained policies/SoA are recommended to sustain audit readiness and regulatory assurance over time.

*Prepared by: Internal Audit Team — EuroPay Compliance Assessment (Ketaki Chavan)*

---

## 10.0 Conclusions & Recommendations

This assessment set out to demonstrate, through a realistic but self-contained exercise, how an organization operating a digital payment application would structure a combined ISO/IEC 27001:2022 and GDPR compliance programme — from risk identification through to a final report suitable for management review.

The exercise reinforced several practical lessons about GRC work in a financial-services context. First, risk scoring is only defensible when the scoring criteria are made explicit; a Medium/High label without a stated likelihood-impact rationale invites challenge from an assessor or auditor. Second, an honest Statement of Applicability — one that documents controls that are not applicable or only partially applied, rather than marking every control as fully implemented — is more credible than a table showing universal compliance. Third, a DPIA is materially strengthened by an explicit necessity-and-proportionality assessment rather than a risk-and-mitigation list alone.

Two concrete follow-up actions are carried forward from this assessment:

- Formalize and test a documented business-continuity plan covering full-service outage scenarios, closing the gap on ISO control A.5.30.
- Introduce a documented identity-verification step and a tracked log for data subject access requests, closing the identified GDPR process gap.

With these two actions closed, EuroPay's control environment would be considered fully aligned with the scope of controls selected in this assessment, subject to the standard annual review cycle.

---

**Disclaimer:** This report was produced as an independent, self-directed learning exercise and references publicly available versions of the above frameworks. EuroPay is a fictional entity created solely for the purposes of this project; no real organization, system, or individual's data is represented.
