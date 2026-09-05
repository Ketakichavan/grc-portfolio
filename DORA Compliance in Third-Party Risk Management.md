# DORA Compliance in Third-Party Risk Management

**A GRC Framework for Outsourced IT Contractors**

![Framework](https://img.shields.io/badge/Framework-DORA%20%2F%20ISO%2027001-blue)
![Domain](https://img.shields.io/badge/Domain-GRC%20%2F%20TPRM-informational)
![Status](https://img.shields.io/badge/Status-Student%20Project-yellow)
![License](https://img.shields.io/badge/Use-Portfolio%20Demo-lightgrey)

Aligned with **DORA** (Regulation (EU) 2022/2554), Articles 28–30, and **ISO/IEC 27001:2022 Annex A**

> *Simulated enterprise project — for portfolio and demonstration purposes only.*

---

## 1. Executive Summary

Financial entities routinely outsource software development and IT support to external vendors. This transfers day-to-day technical work off the books, but not the risk: under DORA and ISO/IEC 27001, the financial entity remains fully accountable for cybersecurity and operational risks introduced by outsourced personnel.

This project builds a working **Third-Party Risk Management (TPRM)** framework focused specifically on **third-party people risk** — the risk that comes from external staff being granted access to internal systems, source code, and sensitive data, rather than from the vendor's technology itself.

It demonstrates, end to end, how a GRC/TPRM analyst would identify, assess, approve, monitor, and eventually offboard vendor-supplied personnel, while keeping a documented, audit-ready evidence trail mapped directly to DORA Articles 28–30 and ISO/IEC 27001 Annex A.

### What this report contains

- A realistic scenario with two vendors of different risk tiers (not a single idealized case)
- A defined risk-scoring methodology, not just unexplained High/Medium/Low labels
- Seven working registers, each with 10+ entries and a mix of open and closed items
- Explicit mapping to DORA Articles 28, 29, and 30, and to ISO/IEC 27001 Annex A controls
- A Joiner–Mover–Leaver (JML) process with visual process flow
- Honest findings: four open governance gaps that a first-pass TPRM assessment would realistically surface

---

## 2. Project Objective, Assumptions & Scope

### 2.1 Objective

To design and operate an end-to-end framework for managing the risk of vendor-supplied IT personnel who have access to source code, CI/CD pipelines, test environments, and limited production systems — covering onboarding, ongoing monitoring, incident handling, and offboarding — in a way that is defensible in a DORA/ISO 27001 audit.

### 2.2 Key Assumptions

- The organization is a European financial institution and a DORA in-scope "financial entity"
- IT services are partially outsourced to external vendors; vendor staff are embedded within internal teams rather than working purely offsite
- Vendor-provided staff require access to source code repositories, test environments, CI/CD pipelines, and limited production data
- Outsourced personnel introduce operational, security, and compliance risk that the organization cannot delegate away
- The organization remains accountable for third-party actions under DORA Article 28, regardless of contractual outsourcing
- This is a simulated enterprise project created for learning and portfolio demonstration; all names, IDs, and dates are fictional

### 2.3 Scope and Deliverables

The project delivers the practical artifacts a GRC/TPRM team would maintain, rather than a policy narrative alone:

- Vendor and outsourced-resource registers for visibility of external staff
- A risk register identifying people-related third-party risks and mitigation actions
- Access control and due-diligence records governing approvals and reviews
- Training, incident, and monitoring registers supporting ongoing oversight
- An exit-strategy register defining triggers and actions for vendor termination
- Control mappings demonstrating alignment with DORA (Art. 28–30) and ISO/IEC 27001 Annex A

### 2.4 Role Performed

**GRC / Third-Party Risk Management Analyst (Student Project)** — responsible for identifying third-party people risks, maintaining governance registers, reviewing access controls, and supporting regulatory alignment.

---

## 3. Vendor Overview

Two vendors are modelled with deliberately different risk profiles, to show that TPRM controls scale with risk tier rather than being applied uniformly to every engagement.

### 3.1 Vendor A — ABC Technologies (High / Critical tier)

| Field | Detail |
|---|---|
| **Vendor profile** | External IT staffing and software services provider supplying developers and application support engineers |
| **Engagement type** | Resource outsourcing — vendor staff embedded within internal teams, performing day-to-day operational and development work under organizational direction |
| **Services provided** | Software development support; application and system support services |
| **Systems accessed** | Source code repositories, CI/CD pipelines, test environments, limited production systems |
| **Geographical location** | EU and offshore locations — raises data residency, regulatory, and oversight considerations |
| **Data sensitivity** | Customer-related and financial information |
| **Risk tier** | **High / Critical** — due to direct access to sensitive systems, reliance on outsourced personnel for key activities, and non-transferable regulatory accountability under DORA |

### 3.2 Vendor B — QA Solutions Ltd. (Low tier, for contrast)

| Field | Detail |
|---|---|
| **Vendor profile** | EU-only QA and testing services provider supplying test engineers |
| **Engagement type** | Task-based outsourcing — fixed-scope QA cycles, no embedded long-term staff |
| **Services provided** | Functional and regression testing in non-production test environments only |
| **Systems accessed** | Test environments only — no source code write access, no production access |
| **Geographical location** | EU only — no cross-border data residency concern |
| **Data sensitivity** | None — test environments use synthetic data only |
| **Risk tier** | **Low** — minimal access scope, single jurisdiction, no sensitive data exposure |

### 3.3 Regulatory Context

Under DORA and ISO/IEC 27001, the organization remains responsible for managing risks introduced by third-party vendors regardless of risk tier. The vendor overview above supports regulatory expectations by documenting vendor criticality, risk exposure, and the differentiated level of continuous oversight each engagement requires.

---

## 4. TPRM Lifecycle

The lifecycle below governs outsourced IT contractors end to end — from vendor identification through periodic reassessment and eventual exit. Stage 8 (re-assessment) feeds back into stage 2 (risk assessment) as an ongoing loop, not a one-time gate.

> 🖼️ *See `media/` for the original TPRM lifecycle diagram exported from the source report.*

### 4.1 Stage Descriptions

**1. Vendor Identification**
- Identify vendors providing IT human resources (developers, support engineers, QA, admin staff)
- Capture vendor profile, geographical location, and criticality in the Vendor Overview

**2. Vendor & Resource Risk Assessment**
- Assess risks tied to outsourced personnel: system access, sensitive data, operational impact, insider threat
- Record findings in the Vendor Risk Register and Outsourced Resource Register

**3. Due Diligence & Compliance Checks**
- Perform background checks; verify training programmes, regulatory awareness, and access governance
- Track assessments in the Due Diligence Register and Training Register

**4. Risk Treatment Planning**
- Define mitigation measures: access control, MFA, JML processes, security training, incident reporting, monitoring
- Document plans in the Access Control, Incident, and Monitoring Registers

**5. Management Approval**
- Obtain sign-off from IT Security, GRC, and relevant managers for access grants and risk-mitigation plans

**6. Contractual Enforcement (DORA Art. 30)**
- Ensure SLAs, exit triggers, audit rights, and subcontracting-notification clauses are written into vendor contracts

**7. Onboarding & Ongoing Monitoring**
- Implement the Joiner–Mover–Leaver process for vendor staff
- Monitor access, training completion, incidents, and compliance continuously via the Monitoring Register

**8. Re-Assessment & Continuous Improvement**
- Reassess vendor risk periodically (quarterly/semi-annual) or upon staff, system, or regulatory change

**9. Exit / Offboarding**
- Trigger exit procedures on high unresolved risk, repeated incidents, non-compliance, contract expiry, or vendor insolvency
- Execute access revocation, data retrieval, and work transfer, recorded in the Exit Strategy Register

---

## 5. Risk Assessment Methodology

Every risk rating used in the registers that follow is derived from this matrix, rather than being an unexplained label.

**Risk Level = Impact × Likelihood**, each scored on a 3-point scale.

| Impact ↓ / Likelihood → | Low | Medium | High |
|---|---|---|---|
| **High** | Medium | High | Critical |
| **Medium** | Low | Medium | High |
| **Low** | Low | Low | Medium |

### 5.1 Definitions

- **Impact** — severity to the organization if the risk materializes (data exposure, service disruption, regulatory breach)
- **Likelihood** — probability of occurrence given current controls (access scope, monitoring maturity, vendor track record)

### 5.2 Review Cadence by Risk Level

| Risk Level | Review Cadence | Ownership |
|---|---|---|
| **Critical** | Monthly | Named executive (CISO / Head of GRC) |
| **High** | Quarterly | GRC / IT Security lead |
| **Medium** | Quarterly | IT Security |
| **Low** | Annual | Vendor manager |

---

## 6. Registers

### 6.1 Outsourced Resource Register

*Purpose: provides visibility into all external personnel (contractors) supplied by vendors who are working on internal systems, supporting access tracking, risk monitoring, and compliance with DORA and ISO/IEC 27001.*

| ID | Role | Vendor | Access Level | Systems Accessed | Data Type | Location | Risk |
|---|---|---|---|---|---|---|---|
| OR-01 | Developer | ABC Technologies | High | Source code, CI/CD | Customer data | Offshore | High |
| OR-02 | Support Engineer | ABC Technologies | Medium | Logs, Prod (read-only) | Financial data | EU | Medium |
| OR-03 | QA Engineer | ABC Technologies | Medium | Test environments | None | EU | Low |
| OR-04 | Admin Staff | ABC Technologies | High | CI/CD, monitoring tools | Operational data | Offshore | High |
| OR-05 | Developer | ABC Technologies | High | Source code, CI/CD | Customer data | EU | Medium |
| OR-06 | Support Engineer | ABC Technologies | Medium | Logs (read-only) | Financial data | Offshore | High |
| OR-07 | QA Engineer | QA Solutions Ltd. | Low | Test environments only | None (synthetic) | EU | Low |
| OR-08 | QA Engineer | QA Solutions Ltd. | Low | Test environments only | None (synthetic) | EU | Low |
| OR-09 | Developer | ABC Technologies | High | Source code, CI/CD | Customer data | Offshore | High |
| OR-10 | Admin Staff | ABC Technologies | High | CI/CD, monitoring tools | Operational data | EU | Medium |

**Key considerations:**
- Role identifies the function of the outsourced staff member
- Systems Accessed highlights which internal systems each resource can reach
- Data Type tracks the sensitivity of accessible data
- Location informs data residency and regulatory implications (DORA Art. 29 concentration risk)
- Risk Level assesses potential impact based on access and operational criticality

### 6.2 Vendor Risk Register

*Purpose: tracks and manages risks associated with external vendors supplying IT contractors, ensuring appropriate mitigating controls and actions are in place and owned.*

| ID | Risk Description | Impact | Likelihood | Level | Control in Place | Action Required | Status |
|---|---|---|---|---|---|---|---|
| VR-01 | Misuse of access by outsourced developer | High | Medium | High | RBAC, MFA | Quarterly access review | Open |
| VR-02 | Delay in access removal after exit | High | Medium | High | Manual offboarding | Automate JML process | Open |
| VR-03 | Lack of mandatory security training | Medium | Medium | Medium | NDA only | Implement mandatory training | Closed |
| VR-04 | Offshore data residency exposure | High | Low | High | Contractual data-location clause | Confirm annual attestation | Open |
| VR-05 | Single-vendor concentration (Art. 29) | High | Low | High | None dedicated | Assess alternative vendor viability | Open |
| VR-06 | Undisclosed subcontracting | Medium | Medium | Medium | Contract clause only | Require disclosure per Art. 30(2)(a) | Open |
| VR-07 | Excessive standing access (no periodic revalidation) | Medium | Medium | Medium | Quarterly review (partial coverage) | Extend review to all resource IDs | Open |
| VR-08 | QA test data leakage risk | Low | Low | Low | Synthetic data only | None — monitor only | Closed |
| VR-09 | Insufficient incident visibility from vendor side | Medium | Medium | Medium | Manual vendor reporting | Integrate vendor into SIEM alerting | Open |
| VR-10 | Vendor staff turnover disrupts continuity | Medium | High | High | None formal | Add handover clause to contract | Open |

### 6.3 Access Control Register — Outsourced Vendor Staff

*Purpose: tracks and governs human access for outsourced IT resources, ensuring access is approved, MFA-enforced, and reviewed on a defined cadence.*

| User Type | Access Type | Approval Required | MFA | Review Frequency | Risk | Notes |
|---|---|---|---|---|---|---|
| Vendor Developer | Source code & CI/CD | Manager + IT Security | Yes | Quarterly | High | Access critical to development; monitored for insider threat |
| Vendor Support | Production logs (read-only) | IT Security only | Yes | Quarterly | Medium | Limited read-only access to support operations |
| Vendor QA Engineer | Test environments | Manager + IT Security | Yes | Quarterly | Medium | Access limited to QA tasks, no production access |
| Vendor Admin Staff | CI/CD & monitoring tools | Manager + IT Security | Yes | Quarterly | High | Access to deployment pipelines; sensitive operational data |
| Vendor QA (Vendor B) | Test environments only | IT Security only | Yes | Semi-annual | Low | Synthetic data only; lowest-risk access tier |
| Vendor Developer (secondary) | Source code (read-only branch) | Manager only | Yes | Quarterly | Medium | Read-only for code review contributions |

### 6.4 Due Diligence Register — Vendor HR & Security Controls

*Purpose: tracks the organization's assessment of vendor human-resource and security practices, ensuring vendor staff are properly vetted, trained, and governed.*

| Control Area | Question | Vendor Response | Status | Comments / Actions Required |
|---|---|---|---|---|
| Background Checks | Are checks performed on vendor staff? | Yes | ✅ OK | Checks performed annually; documented evidence available |
| Security Training | Is mandatory cybersecurity & operational training provided? | No | ⚠️ Gap | Implement training programme; track completion in Training Register |
| Access Management | Are individual user accounts assigned to vendor staff? | Yes | ✅ OK | Enforce RBAC and MFA; reviewed quarterly |
| Exit Process | Are access-removal SLAs defined for leavers? | No | ⚠️ Gap | Define SLA and integrate with JML process; high risk if delayed |
| Regulatory Awareness | Are vendor staff aware of DORA/ISO 27001 requirements? | Partial | ⚠️ Gap | Provide awareness sessions; monitor completion |
| Incident Reporting | Is there a clear procedure for vendor staff to report incidents? | Yes | ✅ OK | Escalation path aligns with Incident Register |
| Subcontracting Disclosure | Are subcontractors disclosed and vetted? | Partial | ⚠️ Gap | Require disclosure and vetting per Art. 30(2)(a) |
| Data Handling Training | Are staff trained on data classification and handling? | No | ⚠️ Gap | Add module to onboarding training track |

### 6.5 Incident Register — Vendor Human Resource Incidents

*Purpose: tracks human-related security and operational incidents involving outsourced vendor staff, ensuring documentation, escalation, and resolution in line with DORA and ISO/IEC 27001 A.16.*

| ID | Role Involved | Description | Impact | Action Taken | Status | Escalation Path |
|---|---|---|---|---|---|---|
| INC-01 | Developer | Access not removed after exit | Medium | Access revoked | Closed | IT Security / GRC |
| INC-02 | Support Engineer | Unauthorized read of production logs | High | User debriefed, access restricted | Closed | IT Security + Manager |
| INC-03 | QA Engineer | Test environment misconfiguration | Medium | Config reverted; team retrained | Closed | Team Lead + IT Security |
| INC-04 | Vendor Admin Staff | Deployment pipeline error caused downtime | High | Incident resolved; pipeline access reviewed | Closed | IT Ops + GRC |
| INC-05 | Developer | Failed regulatory awareness training completion | Medium | Scheduled training; completion tracked | Open | GRC / HR |
| INC-06 | Developer | Shared credentials used for source-code access | High | Credentials rotated; individual accounts enforced | Closed | IT Security |
| INC-07 | Support Engineer | Delayed reporting of a suspicious login | Medium | Reporting SLA reinforced with vendor | Open | IT Security |

### 6.6 Monitoring Register — Outsourced Vendor Staff

*Purpose: tracks ongoing oversight of vendor personnel — access, training, incidents, and compliance — in line with DORA continuous-monitoring expectations.*

| Monitoring Item | What Is Checked | Frequency | Owner | Status / Notes |
|---|---|---|---|---|
| Access Review | Vendor staff access to systems (source code, CI/CD, test, production) | Quarterly | IT Security | Ongoing; linked to Access Control Register |
| Training Review | Completion of mandatory cybersecurity & regulatory training | Annual | GRC | Planned; gaps tracked via Training Register |
| Incident Review | Human-related incidents; remediation and lessons learned | As needed | GRC | Ongoing; references Incident Register |
| Compliance Review | Vendor activity compliance with DORA & ISO/IEC 27001 | Semi-Annual | GRC / Risk Team | Planned; linked to Due Diligence & Vendor Risk Registers |
| JML Process Verification | Timely Joiner–Mover–Leaver execution | Quarterly | IT Security + HR | Ongoing; cross-checked with Access & Exit Registers |
| Exit Strategy Monitoring | Exit actions completed for unresolved-risk vendors | As triggered | GRC / IT Security | Ongoing; ensures access revocation and handover |
| Concentration Risk Review | Single-vendor dependency assessment (Art. 29) | Annual | GRC / Procurement | Open item — first formal review pending |

### 6.7 Exit Strategy Register — Outsourced Vendor Staff

*Purpose: defines triggers, actions, and governance for the exit of vendor personnel or termination of vendor contracts, ensuring access is revoked and data secured.*

| Exit Trigger | Description | Action Required | Owner | Notes |
|---|---|---|---|---|
| High Unresolved Risk | Vendor fails to remediate identified high/critical risks | Terminate contract; revoke all access; secure data | GRC / IT Security | Exit plan defined in vendor agreement |
| Repeated Incidents | Multiple human-related incidents (access misuse, errors) | Switch vendor or reassign resources; review incidents | IT Security / Ops | Root-cause analysis before onboarding replacement staff |
| Regulatory Non-Compliance | Vendor fails to meet DORA / ISO/IEC 27001 requirements | Immediate exit; revoke access; ensure data retrieval | GRC / Compliance | Cross-check with Due Diligence Register |
| Contract Expiry | Vendor contract ends or project completes | Offboard staff; revoke access; transfer work | IT Security + HR | JML process completed; registers updated |
| Vendor Insolvency | Vendor unable to continue services | Exit vendor; reassign or procure new vendor | GRC / Procurement | Contingency plan and backup vendors validated in advance |

---

## 7. Joiner–Mover–Leaver (JML) Process

The JML process governs the full lifecycle of vendor personnel access — onboarding, role change, and departure — and is the single control most directly tied to the two highest-rated open risks in the Vendor Risk Register (**VR-01, VR-02**).

> 🖼️ *See `media/` for the original JML process flow diagram exported from the source report.*

### 7.1 Joiner (Onboarding Vendor Staff)

- **Access Approval** — Manager + IT Security approve access based on role (RBAC applied)
- **Account Creation** — individual user accounts created for internal systems
- **Training Completion** — mandatory cybersecurity, operational resilience, and regulatory awareness training tracked in the Training Register
- **Documentation** — recorded in Access Control, Outsourced Resource, and Due Diligence Registers
- **Compliance Check** — confirm vendor staff understand DORA and ISO 27001 obligations

### 7.2 Mover (Role / Access Changes)

- **Access Review** — validate current system access against the new role
- **Role Updates** — adjust permissions in line with new responsibilities; ensure RBAC/MFA compliance
- **Approval Recorded** — Manager + IT Security approve the change
- **Training Updates** — verify completion of any new role-specific training
- **Register Updates** — Access Control, Outsourced Resource, and Monitoring Registers updated

### 7.3 Leaver (Offboarding Vendor Staff)

- **Access Removal** — immediately remove system access (source code, CI/CD, test, production)
- **Account Deactivation** — disable individual accounts and MFA
- **Data Retrieval / Deletion** — ensure all company data is returned or securely deleted; documented in the Exit Strategy Register
- **Work Transfer** — reassign ongoing tasks to internal teams or an alternative vendor
- **Documentation & Audit** — log exit in Access Control, Monitoring, Vendor Risk, and Incident Registers
- **Lessons Learned** — record preventive measures to reduce recurrence

---

## 8. DORA Control Mapping (Chapter V, Articles 28–30)

DORA's third-party risk pillar (Chapter V, Section I) rests on three core articles, in force since 17 January 2025. The mapping below ties each requirement to the specific register that evidences it — the level of specificity an auditor or interviewer would expect, rather than a generic "aligned with DORA" claim.

| DORA Article | Requirement | Mapped Evidence | Notes / Alignment |
|---|---|---|---|
| **Art. 28** — General principles | ICT third-party risk strategy; due diligence before contracting; suitability assessment of providers | Due Diligence Register, Vendor Overview | Financial entity retains full accountability; obligations cannot be delegated to the provider |
| **Art. 28(3)** — Register of Information | Maintain and submit a register of all ICT third-party contractual arrangements to the competent authority | Outsourced Resource Register, Vendor Overview | Captures provider identity, service, criticality, location, and subcontracting status |
| **Art. 29** — Concentration risk | Assess dependency on providers that are not easily substitutable, or multiple arrangements with the same provider | Vendor Risk Register (VR-05), Monitoring Register | Single-vendor reliance on ABC Technologies flagged as an open risk requiring annual review |
| **Art. 30** — Key contractual provisions | Mandatory clauses: description of services, audit rights, termination rights, subcontracting notification, data location | Vendor Overview, Exit Strategy Register, VR-06 | Subcontracting disclosure gap (VR-06) identified as an open action against this article |
| **Ongoing monitoring & exit strategies** | Continuous oversight of arrangements; documented exit triggers and actions | Monitoring Register, Exit Strategy Register | JML verification runs quarterly; five distinct exit triggers defined by scenario |

---

## 9. ISO/IEC 27001 Annex A Control Mapping

| Annex A Control | Mapped Evidence | Notes / Alignment |
|---|---|---|
| **A.5** Supplier Relationships | Vendor Overview, Vendor Risk Register | Vendor profiling, risk tiering, and ongoing oversight for both vendor tiers |
| **A.6** Access Control | Access Control Register, Outsourced Resource Register | Role-based access, MFA enforcement, quarterly reviews of vendor staff access |
| **A.7** Human Resource Security | Due Diligence Register, Training Register | Background checks, onboarding, security/regulatory training, exit procedures |
| **A.8** Incident Management | Incident Register, Monitoring Register | Escalation paths, impact assessment, and lessons learned for human-related incidents |
| **A.9** Operational Procedures | Monitoring Register, Exit Strategy Register | Continuous monitoring of access, incidents, training, and JML verification |
| **A.12** Cryptography & Data Protection | Exit Strategy Register, Access Control Register | Sensitive data retrieved, returned, or securely deleted upon vendor exit |
| **A.18** Compliance | Due Diligence Register, Vendor Risk Register, DORA Mapping | Demonstrates regulatory alignment and audit readiness for outsourced human resources |

---

## 10. Key Findings & Gaps Identified

A first-pass TPRM assessment realistically surfaces open gaps rather than a fully clean bill of health. The Due Diligence Register identified four such gaps, each carried forward into the Vendor Risk Register as an owned, actioned item:

- ⚠️ No mandatory security training programme currently exists for vendor staff (Due Diligence: Gap)
- ⚠️ No defined SLA for access removal on exit — the single largest driver of insider-risk incidents observed (INC-01, INC-05, and underlying VR-02)
- ⚠️ Regulatory awareness of DORA/ISO 27001 obligations among vendor personnel is only partial
- ⚠️ No formal subcontracting-disclosure process exists, creating a blind spot against DORA Art. 30(2)(a)

None of these gaps is treated as closed by writing a policy about it — each has a named action, an owner, and a review cadence in the Vendor Risk Register (see Section 6.2, VR-02, VR-06).

---

## 11. Results & Impact

Applying this framework, the (simulated) organization is able to:

- Maintain documented visibility of every outsourced individual with system access, across two differently-scoped vendor engagements
- Reduce risk from excessive access, insider threat, and delayed offboarding through a defined JML process
- Apply consistent, auditable controls across joiners, movers, and leavers
- Evidence DORA Art. 28–30 compliance and ISO/IEC 27001 Annex A alignment with register-level, traceable proof rather than narrative claims
- Track open governance gaps explicitly, rather than assuming full maturity on day one

---

## 12. Lessons Learned & Recommendations

- Manual JML and offboarding tracking is the single weakest control observed — automating the Leaver trigger (linking contract-end dates to an access-revocation workflow) would close the largest open risk in the register (VR-02)
- Concentration risk under Art. 29 deserves a recurring, not one-time, review — single-vendor dependency for critical functions is precisely the scenario the article targets (VR-05)
- Subcontracting disclosure should be a standing contractual requirement, not a point-in-time due-diligence question (VR-06)
- Traceability between registers — incident → risk → monitoring → exit — is what makes the framework audit-ready, more than any individual register on its own
- **Next iteration:** extend the framework to a third vendor with a different jurisdiction (non-EU, no adequacy decision) to test data-transfer control mapping

---

## 13. Conclusion

This project provides a practical, end-to-end framework for managing outsourced IT personnel risk in a financial organization. By integrating vendor oversight, access governance, training, incident management, monitoring, and exit strategies — and by mapping each artifact explicitly to DORA Articles 28–30 and ISO/IEC 27001 Annex A — it demonstrates the kind of evidence a real GRC/TPRM function would need to produce under audit.

Rather than presenting a fully resolved compliance picture, the framework deliberately surfaces open risks and gaps — reflecting how a first-pass third-party risk assessment actually looks in practice, and how it would be tracked toward closure over time.

---

**Disclaimer:** This is a simulated student project created for learning and portfolio purposes. All vendor names, IDs, incidents, and dates are fictional and do not represent any real organization.
