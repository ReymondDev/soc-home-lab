# 01 — Scope and Organisational Context

**Project:** ISO/IEC 27001:2022 Risk Assessment
**Organisation:** Thornbury Precision Engineering Ltd (fictional)
**Assessor:** Reymond
**Date:** August 2026
**Version:** 1.0

---

## 1. Purpose of this document

This document establishes the boundaries of the information security management system (ISMS) under assessment, identifies the parties with an interest in it, and records the legal, regulatory and contractual obligations that constrain it.

Under ISO/IEC 27001:2022, clauses 4.1 to 4.4 require an organisation to determine its context and define the ISMS scope before any risk assessment is performed. Scoping first is not administrative overhead — it decides which assets are assessed, which risks are considered relevant, and which controls the organisation will ultimately be audited against. A scope drawn too widely creates an unachievable certification programme; drawn too narrowly, it produces a certificate that reassures nobody.

---

## 2. Organisational context

Thornbury Precision Engineering Ltd is a privately owned contract manufacturer based near Corby, Northamptonshire. The company operates a single site combining a machine shop, a quality laboratory, and a small office function.

| | |
|---|---|
| Sector | Precision engineering / contract manufacturing |
| Employees | 60 (42 shop floor, 18 office and management) |
| Sites | One — Corby, Northamptonshire |
| Turnover | ~£8.4m |
| Customers | Tier-one automotive and aerospace suppliers; approx. 70% of revenue from four accounts |
| Existing certifications | ISO 9001, AS9100 (aerospace quality) |
| In-house IT | One IT Manager; infrastructure support outsourced to a regional MSP |

The company machines components to customer-supplied technical specifications. It does not design its own products. Its commercial position therefore rests on manufacturing capability and on customer trust that proprietary designs entrusted to it will not leak to competitors.

### 2.1 Business driver for the ISMS

In March 2026, Thornbury's largest aerospace customer notified suppliers that ISO/IEC 27001 certification would become a condition of contract renewal from Q3 2027. That account represents roughly 31% of revenue.

This matters for how the assessment is framed. The organisation is not pursuing certification out of general security ambition — it is protecting a specific revenue stream against a specific commercial deadline. Risk treatment recommendations are therefore evaluated against both security benefit and cost of delay, and the executive summary is written for a board whose primary concern is contract retention rather than security maturity.

### 2.2 Internal factors

- No dedicated security function. The IT Manager holds security responsibilities alongside a full infrastructure workload.
- A cyber-aware quality culture already exists through AS9100 — staff are accustomed to documented procedures, traceability and audit. This is a genuine asset and is treated as a mitigating factor in several risk ratings.
- Shop-floor staff have limited day-to-day computer use, which lowers phishing exposure but also means security awareness training has historically been directed only at office staff.
- Capital expenditure is constrained; several CNC machines run vendor-supplied controllers that cannot be patched without invalidating machine warranties.

### 2.3 External factors

- Manufacturing has been among the most targeted sectors for ransomware in recent years, driven by low downtime tolerance and typically weaker OT segmentation.
- Customer-mandated security requirements are cascading down UK aerospace and automotive supply chains, and are increasingly contractual rather than advisory.
- Aerospace technical data may attract UK export control obligations depending on the specific components involved.

---

## 3. Scope statement

> The ISMS covers the information assets, systems, personnel and processes supporting the manufacture of precision-machined components at Thornbury Precision Engineering Ltd's Corby site, including the receipt, storage, processing and return of customer technical data and the corporate information systems supporting that activity.

### 3.1 In scope

**Information**
- Customer technical drawings, CAD/CAM models and manufacturing specifications
- Customer contract, pricing and commercial terms
- Quality and traceability records supporting AS9100
- Employee personal data (payroll, HR, right-to-work documentation)
- Supplier and subcontractor records

**Systems**
- Microsoft 365 tenant and Microsoft Entra ID
- Cloud-hosted ERP and production planning system
- CAD/CAM file storage
- Shop-floor data collection terminals
- Networked CNC machine controllers *(see 3.3)*
- Corporate LAN, Wi-Fi and internet gateway
- Backup infrastructure (on-site NAS and cloud replication)
- End-user laptops and mobile devices

**People and processes**
- All permanent staff, contractors and agency workers at the Corby site
- The outsourced MSP, in respect of its access to Thornbury systems
- Onboarding, offboarding, access management and incident response processes

### 3.2 Out of scope, with justification

| Excluded | Justification |
|---|---|
| Customer-owned systems and networks | Not under Thornbury's control. Interfaces to them are in scope; the systems themselves are not. |
| Physical machining process and product quality | Governed by ISO 9001 and AS9100. Included only where information integrity affects product conformity. |
| Employees' personal devices | No BYOD permitted for business data. This is asserted by policy but not technically enforced — recorded as a risk rather than accepted as a control. |
| Subcontractors' internal environments | Addressed through supplier assurance clauses (A.5.19–A.5.22), not through direct assessment. |

### 3.3 Scope decision requiring explicit note

Networked CNC controllers have been included despite being operational technology rather than IT.

Excluding them would have been defensible and simpler: they are not general-purpose computers, they hold no personal data, and several cannot be patched. However, they hold copies of customer-derived machining programs, they sit on the same flat network as office systems, and a ransomware event reaching them would halt production entirely. Excluding the assets most likely to cause the loss the ISMS exists to prevent would produce a scope that satisfies an auditor but not the customer who demanded certification.

The inclusion is therefore deliberate and its cost is acknowledged: it introduces controls the organisation cannot currently implement, which appear in the gap analysis as accepted risks with compensating measures rather than as closed findings.

---

## 4. Interested parties and their requirements

| Party | Requirement | Type |
|---|---|---|
| Aerospace customer (largest account) | ISO 27001 certification by Q3 2027; protection of technical data under NDA | Contractual |
| Automotive customers | Evidence of supply-chain security assurance; Cyber Essentials Plus expected | Contractual |
| Board / owners | Contract retention; proportionate spend; no production disruption | Commercial |
| Employees | Lawful and secure handling of personal data | Legal |
| Information Commissioner's Office | Compliance with UK GDPR and the Data Protection Act 2018 | Regulatory |
| Insurers | Demonstrable controls to maintain cyber cover and premium levels | Commercial |
| MSP | Clear division of security responsibility | Contractual |

---

## 5. Legal, regulatory and contractual obligations

| Obligation | Relevance |
|---|---|
| UK GDPR / Data Protection Act 2018 | Employee and contact personal data; breach notification within 72 hours; Article 32 security of processing |
| Computer Misuse Act 1990 | Framing of unauthorised access; relevant to acceptable use policy and monitoring |
| Export control (Export Control Order 2008) | Potentially applicable to certain aerospace technical data — flagged for legal confirmation, not assumed |
| Customer NDAs | Contractual confidentiality obligations over technical data, with liability exposure |
| AS9100 / ISO 9001 | Existing certifications requiring record integrity and traceability |
| Cyber Essentials Plus | Expected by automotive customers; overlaps substantially with Annex A technical controls |

---

## 6. Assumptions and limitations

Recording these is not a disclaimer — an assessment whose limits are undocumented cannot be relied upon or repeated.

1. **This is a fictional scenario** built to demonstrate assessment methodology. The organisation, systems and findings are constructed, though modelled on configurations typical of UK precision engineering SMEs.
2. **The assessment is document-based.** No technical testing, vulnerability scanning or configuration review was performed. Control effectiveness is stated as designed, not as verified — a real engagement would validate this and ratings could shift materially as a result.
3. **Export control applicability is flagged, not determined.** That is a legal question outside the assessor's competence.
4. **Threat likelihood draws on general sector patterns**, not on Thornbury-specific incident history or threat intelligence.
5. **The MSP's own security posture is assumed adequate but unverified.** In practice this would be a significant open question and is carried as a risk in the register.

---

## 7. Next steps

| Document | Content |
|---|---|
| `02-asset-inventory.md` | Identification and CIA classification of in-scope assets |
| `03-methodology.md` | Risk scoring scale, appetite and treatment criteria |
| `registers/risk-register.md` | Identified risks with inherent and residual ratings |
| `04-control-gap-analysis.md` | Mapping to ISO 27001:2022 Annex A controls |
| `05-executive-summary.md` | Board-level summary of findings and recommendations |