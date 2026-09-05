# ISO/IEC 27001:2022 + GDPR Compliance Assessment — EuroPay

A self-driven Governance, Risk & Compliance (GRC) assessment of **EuroPay**, a fictional digital payment application, conducted against ISO/IEC 27001:2022 and the EU GDPR. The goal is to demonstrate, in an audit-ready format, how information security and data protection compliance are implemented, evidenced, and reported in a fintech environment.

## Overview

The assessment identifies **10 information security risks** spanning authentication, application security, insider threat, cloud configuration, supplier dependency, operational resilience, and AI/ML fraud-detection risk. After applying the recommended treatments, residual risk is reduced to **Medium or lower** across all identified risks — acceptable for the scope of this exercise, provided ongoing monitoring, periodic reassessment, and an annual DPIA review are maintained.

Two follow-up actions are recommended:
- Formalize a tested business-continuity plan (ISO control A.5.30).
- Strengthen the documented process for handling data subject access requests.

## Project Objectives

- Perform a structured ISO/IEC 27001:2022 risk assessment focused on payment-related threats (account compromise, transaction manipulation, fraud, AI/ML-assisted fraud detection risks).
- Map identified risks to ISO/IEC 27001:2022 Annex A controls.
- Build a GDPR data inventory for personal and transaction data, with lawful basis, retention periods, and storage locations.
- Conduct a Data Protection Impact Assessment (DPIA) for high-risk financial processing, including AI/ML fairness and automated-decision considerations.
- Draft foundational Information Security and Data Protection policies.
- Prepare a Statement of Applicability (SoA) covering applied, partially applied, and not-applicable controls.

## Deliverables

- System overview describing e-wallet and transaction workflows
- ISO/IEC 27001 risk register with payment-specific threats and scoring methodology
- GDPR data mapping and retention schedule
- Data Protection Impact Assessment (DPIA)
- Information Security Policy
- Data Protection Policy
- Statement of Applicability
- Final compliance assessment report

## System Overview

EuroPay is a digital payment application offering e-wallet functionality, secure authentication, balance management, and transaction history.

**Functional capabilities:** account sign-up/login with optional MFA, adding funds, peer-to-peer payments, transaction history, and notifications.

**High-level data flow:** client → TLS → API gateway (rate-limiting) → Node.js REST API → business logic + AI/ML fraud-detection scoring → PostgreSQL → notification service. Security/access logs stream to a centralized logging service.

**Data processed:** name, email, phone number, password hash (bcrypt), transaction data (amount, timestamp, sender/receiver ID), IP address and device metadata.

**Technical environment:**
- Backend: Node.js REST API
- Database: PostgreSQL with column-level encryption
- Infrastructure: EU-region cloud, shared-responsibility model
- Security: TLS 1.2+, IAM roles, AES-256 at rest, API rate-limiting, secure SDLC, AI/ML fraud detection with human review

**AI/ML fraud detection:** treated as decision-support rather than fully autonomous — outputs get a reason code and human review where a flag/block could significantly affect a user. Training data requires provenance checks, retraining requires documented approval, and performance is monitored for drift and disparities.

## ISO/IEC 27001:2022 Risk Assessment

**Methodology:** identify assets → identify threats/vulnerabilities → estimate likelihood & impact → map Annex A controls → apply risk treatment.

Likelihood and impact are each rated Low/Medium/High and combined via a risk matrix to produce inherent and residual risk ratings.

### Risk Register Summary

| ID | Risk | Inherent | Residual | Key Controls |
|----|------|----------|----------|---------------|
| R1 | Unauthorized wallet/account access (weak/reused passwords) | High | Medium | A.5.17, A.8.2 — MFA, password policy, lockouts |
| R2 | API abuse / transaction manipulation | High | Medium | A.8.12, A.5.7 — TLS, HMAC signing, throttling |
| R3 | SQL injection exposing payment DB | Medium | Medium | A.8.8, A.5.20 — parameterized queries, WAF |
| R4 | Insider misuse / excessive privileges | Medium | Low | A.8.2, A.8.16 — RBAC, privilege reviews |
| R5 | Data leakage via misconfigured cloud storage | Medium | Low | A.5.20, A.8.12 — private buckets, encryption |
| R6 | Third-party/supplier risk | Medium | Low | A.5.10, A.5.19 — contracts, SOC 2 review |
| R7 | Loss of transaction data availability | Medium | Low | A.5.23, A.8.16 — backups, DR plan |
| R8 | Adversarial manipulation of fraud model | High | Medium | A.5.7, A.8.8, A.8.16 — adversarial testing |
| R9 | Training data poisoning | Medium | Medium | A.5.17, A.8.16, A.8.8 — provenance checks |
| R10 | Model drift / silent degradation | High | Medium | A.8.16, A.5.7 — performance monitoring |

**Overall posture:** inherent risk predominantly High-to-Medium; residual risk reduced to Medium/Low across all ten risks with ongoing monitoring and annual reassessment.

## GDPR Data Mapping

- **Controller:** EuroPay. **Processor:** EU-region cloud provider (under a DPA).
- **Purposes:** account management, authentication, payment execution, fraud detection (incl. AI/ML), regulatory record-keeping.
- **Lawful basis:** Art. 6(1)(b) contractual necessity (accounts, payments); Art. 6(1)(f) legitimate interest (fraud detection, security monitoring, AI/ML analysis).
- **Retention:** account data — account lifetime; transaction data — 5 years; security logs/IP data — 30 days.
- **Storage:** EU-based cloud infrastructure only (avoids GDPR Chapter V third-country transfer issues); AES-256 at rest, TLS 1.2+ in transit, RBAC, MFA for privileged access.
- **Data subject rights:** access, rectification, erasure (subject to statutory retention), restriction, portability — all actioned within 30 days. Automated AI/ML decisions get human review and a contest mechanism where Article 22 applies.

## Data Protection Impact Assessment (DPIA)

Covers necessity/proportionality, consultation, and identified risks to individuals: unauthorized account access, identity misuse, fraud/transaction manipulation, behavioural profiling, adversarial model evasion, training data poisoning, and automated-decision/unfair flagging.

**Mitigations:** MFA, RBAC/least privilege, AES-256 + TLS encryption, centralized logging/monitoring, secure SDLC, AI/ML governance (adversarial testing, provenance checks, human approval for retraining, drift monitoring, reason codes, fairness checks), backups and DR testing.

**Residual risk:** Medium — acceptable for project scope, subject to continuous monitoring and annual DPIA review.

## Policies

- **Information Security Policy** — access control (RBAC/MFA), authentication (bcrypt, brute-force protection), encryption (AES-256, TLS 1.2+), logging & monitoring, secure SDLC, backup & recovery, AI/ML model governance, incident management (24h classification, 72h breach notification), compliance & training.
- **Data Protection Policy** — GDPR principles (lawfulness, minimization, purpose limitation, accuracy, storage limitation, integrity/confidentiality), data subject rights, retention schedule, security measures, roles & responsibilities.

## Statement of Applicability (SoA)

10 Annex A controls applied (A.5.7, A.5.10, A.5.17, A.5.19, A.5.20, A.5.23, A.8.2, A.8.8, A.8.12, A.8.16), 1 partially applied (A.5.30 — business continuity plan not yet fully documented), and 2 marked not applicable with justification (A.7 Physical Security controls, A.8.23 Web Filtering) since EuroPay is fully cloud-hosted with no physical premises or corporate web-browsing risk surface.

## Conclusions & Recommendations

This exercise reinforced that: risk scoring is only defensible with explicit criteria behind each rating; an honest SoA (documenting partial/not-applicable controls rather than claiming full compliance everywhere) is more credible; and a DPIA is strengthened by an explicit necessity-and-proportionality analysis.

**Follow-up actions:**
1. Formalize and test a documented business-continuity plan (closes ISO control A.5.30).
2. Introduce a documented identity-verification step and tracked log for data subject access requests.
3. Formalize AI/ML model governance before production use — versioning, approved retraining, drift/fairness monitoring, reason codes, and human review/contest mechanisms for Article 22-covered decisions.

With these actions closed, EuroPay's control environment would be considered fully aligned with the scope of controls selected in this assessment, subject to standard annual review.
