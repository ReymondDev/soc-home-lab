# 02 — Asset Inventory and Classification

**Project:** ISO/IEC 27001:2022 Risk Assessment
**Organisation:** Thornbury Precision Engineering Ltd (fictional)
**Assessor:** Reymond Guntner
**Date:** August 2026
**Version:** 1.0

---

## 1. Purpose and approach

Risk cannot be assessed against assets that have not been identified. This inventory establishes what is in scope, who owns it, and how badly the organisation would be harmed by a loss of confidentiality, integrity or availability for each.

Assets are grouped as information, systems, infrastructure and physical. Information assets are listed separately from the systems that hold them, because they frequently move between systems — a customer drawing exists in the CAD store, in an email attachment, on a shop-floor terminal, and in a backup, and each location carries a different exposure. Inventorying only systems is the most common way an SME assessment misses its own crown jewels.

Ownership is recorded by role rather than by individual, so the inventory survives staff turnover. Note that owner is not the same as custodian: the Operations Director owns customer technical data, but the MSP has custody of the infrastructure holding it. Where those diverge, the risk of misplaced accountability is itself worth recording.

### 1.1 Classification scale

Each asset is rated High, Medium or Low against each of the three security properties. The rating describes **the consequence of failure**, not the likelihood of it, and not the strength of current controls. Existing controls are accounted for later, at the residual risk stage.

| Rating | Confidentiality — impact of unauthorised disclosure | Integrity — impact of unauthorised or accidental alteration | Availability — impact of loss of access |
|---|---|---|---|
| **High** | Contract loss, regulatory action, or legal liability | Defective product reaching a customer, failed audit, or unsound financial reporting | Production stops, or the business cannot trade, within 24 hours |
| **Medium** | Commercial disadvantage or reputational damage, recoverable | Significant rework, delay or manual correction required | Disruption tolerable for 1–3 days with workarounds |
| **Low** | Minimal consequence if disclosed | Errors detectable and correctable in normal operation | Tolerable for more than 3 days |

---

## 2. Information assets

| ID | Asset | Owner | C | I | A | Business justification |
|---|---|---|---|---|---|---|
| **INF-01** | Customer technical drawings, CAD/CAM models and machining specifications | Operations Director | **H** | **H** | **H** | The organisation's principal confidentiality obligation. Disclosure breaches customer NDAs with direct liability and probable contract loss; some aerospace data may additionally fall under export control. Corrupted geometry produces out-of-tolerance parts that may not be caught until customer inspection. Nothing can be machined without it. |
| **INF-02** | Customer contracts, pricing and commercial terms | Managing Director | **H** | **H** | M | Pricing disclosure to a competitor in a tender process is directly and immediately damaging in a market where four accounts carry 70% of revenue. Altered terms create disputes and revenue leakage. Short-term unavailability is inconvenient rather than critical. |
| **INF-03** | Quality and traceability records (AS9100) | Quality Manager | L | **H** | **H** | Integrity is paramount: these records evidence that a part meets specification, and in aerospace they may be retained for decades and called upon after an incident. Falsified or corrupted records could make parts unsaleable and threaten AS9100 certification. Their content is not commercially sensitive. |
| **INF-04** | Employee personal data — payroll, HR, right-to-work | HR Manager | **H** | M | M | Special category and financial data attracting UK GDPR Article 32 obligations and 72-hour breach notification. Volume is small; regulatory and trust consequences are not proportionate to volume. |
| **INF-05** | Supplier and subcontractor records | Procurement Lead | M | M | M | Includes subcontractor capability and pricing. Commercially useful to a competitor but not contractually protected. Short outages absorbed by existing relationships. |
| **INF-06** | Production schedules and shop-floor job data | Operations Director | L | **H** | **H** | Wrong data means the wrong parts are machined — scrap, delay and possible customer escalation. Loss of access halts the shop floor immediately. Of little value to anyone outside the business. |

---

## 3. System assets

| ID | Asset | Owner | C | I | A | Business justification |
|---|---|---|---|---|---|---|
| **SYS-01** | Microsoft Entra ID (identity and access) | IT Manager | **H** | **H** | **H** | Compromise of the identity layer grants access to everything downstream, which is why it is rated High across all three rather than assessed on its own data content. Loss of authentication locks every user out of every system simultaneously. |
| **SYS-02** | Microsoft 365 tenant — Exchange, SharePoint, Teams | IT Manager | **H** | M | **H** | Customer drawings and commercial data routinely traverse email and SharePoint regardless of policy. Email is also the primary channel for customer communication and the primary route for phishing and invoice fraud. |
| **SYS-03** | Cloud-hosted ERP and production planning system | Operations Director | M | **H** | **H** | The operational spine — orders, scheduling, stock, dispatch. Corrupted data misdirects production; unavailability stops planning and despatch within a shift. |
| **SYS-04** | CAD/CAM file store | Operations Director | **H** | **H** | **H** | Inherits the classification of INF-01. Listed separately because the store is the concentration point where every customer's data sits together — a single compromise exposes all customers at once, not just one. |
| **SYS-05** | Networked CNC machine controllers | Production Manager | M | **H** | **H** | Hold machining programs derived from customer data. Altered tool paths produce defective parts, potentially undetected until inspection. Unavailability stops production directly. Several run vendor-locked firmware that cannot be patched without invalidating warranty — recorded here, addressed in the register. |
| **SYS-06** | Shop-floor data collection terminals | Production Manager | L | M | M | Job booking and time recording. Shared-account use is common on the shop floor, undermining accountability. Manual fallback exists for short outages. |
| **SYS-07** | Backup infrastructure — on-site NAS and cloud replication | IT Manager | **H** | **H** | **H** | Contains a copy of everything else, so it inherits the highest classification of any asset it protects. Also the primary target in a ransomware event: backups that are reachable from the production network are frequently encrypted alongside it. Availability is High because backups are the recovery path of last resort. |

---

## 4. Infrastructure assets

| ID | Asset | Owner | C | I | A | Business justification |
|---|---|---|---|---|---|---|
| **INFRA-01** | Corporate LAN, Wi-Fi and switching | IT Manager | M | **H** | **H** | Currently a flat network with no segmentation between office systems and CNC controllers. This means the network's own integrity is a High rating, because a compromise anywhere reaches everything. |
| **INFRA-02** | Firewall and internet gateway | IT Manager (MSP-managed) | **H** | **H** | **H** | The perimeter control on which most other technical controls depend. Misconfiguration exposes internal systems directly; failure severs cloud ERP and M365 access entirely. |
| **INFRA-03** | End-user laptops and mobile devices | IT Manager | **H** | M | M | Mobile copies of customer data outside the office. Physical loss is the realistic threat, and encryption status is currently inconsistent across the estate. |
| **INFRA-04** | MSP remote administration access | IT Manager | **H** | **H** | **H** | Privileged third-party access to the whole estate. Rated on the access it confers, not on any data it holds. Represents concentrated supply-chain risk and is the least directly observable asset in the inventory. |

---

## 5. Physical assets

| ID | Asset | Owner | C | I | A | Business justification |
|---|---|---|---|---|---|---|
| **PHY-01** | Server room and comms cabinet | IT Manager | M | M | **H** | Houses on-site infrastructure including the backup NAS. Physical access defeats most logical controls. Currently shares space with general storage and is not access-logged. |
| **PHY-02** | CCTV and door access control system | Facilities Manager | M | M | M | Generates personal data through the recording of identifiable individuals, bringing it into UK GDPR scope — frequently overlooked in SME inventories. Supports investigation of physical incidents. |

---

## 6. Observations arising from the inventory

Several points emerged during identification that shape the risk assessment that follows. They are recorded here rather than left implicit, because the act of inventorying often surfaces more than the inventory itself shows.

1. **Fifteen assets, and eight rate High for confidentiality.** That concentration is not padding — it reflects a business whose commercial value rests almost entirely on holding other organisations' intellectual property. Confidentiality controls should therefore be weighted ahead of general hardening in the treatment plan.

2. **The backup infrastructure is the single most consequential asset.** It inherits every other asset's classification while being the most likely target in the most likely serious incident. It warrants disproportionate attention.

3. **Identity is the real perimeter.** SYS-01 rates High across all three properties despite holding almost no business data of its own, because everything else depends on it. Any treatment plan that funds endpoint tooling before it funds identity hardening has misread the inventory.

4. **The flat network converts localised risks into organisation-wide ones.** INFRA-01's High integrity and availability ratings are a direct consequence of an architectural decision rather than of the network's intrinsic importance. Segmentation would materially reduce ratings across SYS-05, SYS-06 and SYS-07.

5. **MSP access (INFRA-04) is the least visible High-rated asset.** It holds no data, appears on no diagram, and would be missed by an inventory built from a systems list. It is the clearest argument for inventorying access relationships alongside systems.

6. **Two assets are classified High for integrity but Low for confidentiality** (INF-03, INF-06). This is a useful corrective: security investment that treats confidentiality as the default concern would underprotect the records that actually determine whether a part is airworthy.

---

## 7. Next document

`03-methodology.md` — risk scoring scale, risk appetite, and treatment criteria.
