<div align="center">

# Veritag
### Manufacturing Knowledge Hub

*Answers with evidence. Lessons that travel. Nothing guessed.*

**CALIBER 2026 · Case 1: Manufacturing Knowledge Hub (AI-Powered Knowledge Integration)**

**Team Anti Hero Department · Universitas Diponegoro**

**[Open the live prototype](https://narazla.github.io/Veritag-Caliber2026/)**

</div>

<br>

Veritag is a Knowledge Hub for chemical plant engineers. It connects the documents and work orders of each asset, answers questions with cited evidence, and finds lessons that exist in the maintenance history but have not yet protected the plant.

The prototype is built on the complete CALIBER 2026 casebook dataset: **8 assets, 96 documents, and 211 work orders**.

## Table of Contents

- [Quick Start for Judges](#quick-start-for-judges)
- [Problem Statement](#problem-statement)
- [Our Solution](#our-solution)
- [Answers to the Three Key Questions](#answers-to-the-three-key-questions)
- [Prototype Features](#prototype-features)
- [Business Impact](#business-impact)
- [Feasibility and Roadmap](#feasibility-and-roadmap)
- [What Is Real and What Is Simulated](#what-is-real-and-what-is-simulated)
- [Technology](#technology)
- [Repository Structure](#repository-structure)
- [Run Locally](#run-locally)
- [Known Limitations](#known-limitations)
- [Team](#team)

## Quick Start for Judges

1. Open the prototype: **https://narazla.github.io/Veritag-Caliber2026/**
2. No login, installation, or account is needed.
3. Use a desktop browser for the best view. The prototype also opens on mobile.

Suggested walkthrough (about 3 minutes):

| Step | Page | What to look at |
| --- | --- | --- |
| 1 | Home | The evidence strip: 8 assets, 96 documents, 211 work orders |
| 2 | Assistant | Ask about the vibration trip of GA-1201A. See the source, approval status, and confidence on the answer |
| 3 | Assistant | Ask about KC-4501. The answer shows two trips and one early warning |
| 4 | Gap Radar | Replay finding F1 (failure chain on GA-1201A) and F2 (gasket lesson across 4 assets) |
| 5 | Review Queue | See how a senior engineer reviews and approves a finding |
| 6 | Analytics | See the impact scenario and the test set result |

The prototype is a single HTML file. You can also download `index.html` and open it by double-click.

## Problem Statement

Plant knowledge exists. It is not connected, not verified, and not used to learn.

Engineers decide fast during start-up, troubleshooting, and maintenance. Their sources are scattered across datasheets, interlock logic, P&IDs, one-point lessons (OPLs), work orders, and live data. Tacit knowledge stays in people's heads. Trusted information is hard to find and hard to confirm. Operational data is not linked to documents.

The casebook data shows what this costs (8 LLDPE assets, June 2024 to December 2025):

- **31 breakdowns and 434 hours of downtime.** Corrective work is 25% of work orders but 56% of recorded cost.
- **A failure chain nobody connected.** GA-1201A had 3 alignment-related failures in 34 days. It failed again 149 days later.
- **A lesson that did not travel.** The same gasket failure appeared on 4 assets within 15 months. LV-6701 still has no procedure.
- **Documents that disagree.** 28 of 56 OPLs cite the wrong asset. 9 of 39 protection tags are not confirmed on the P&ID. 8 of 8 interlock documents state no approval status.
- **A label that misleads.** EA-5601 is marked "LOW CRITICAL" yet has the highest downtime (124 hours).

**Who is affected:** process engineers, maintenance and reliability engineers, operators and technicians, senior engineers, and HSE.

**Why now:** the CA-EDC plant is about 80% built (September 2026). Commercial operation is targeted for Q1 2027 with about 250 new operating jobs. A new plant with new people is when knowledge is needed most and lost most easily.

## Our Solution

Veritag works in five steps. Each step has a proof from the prototype.

| Step | What it does | Proof from the prototype |
| --- | --- | --- |
| 1. Connect | One parser per document type and one knowledge graph keyed by Equipment Tag. Links and data quality are checked automatically | 168 of 168 OPL problem rows linked to their work orders. 30 of 39 protection tags confirmed on the P&IDs |
| 2. Ask | The Assistant answers with evidence. Exact values come from the C&E matrix. Every answer shows its source, approval status, and confidence. Conflicts are shown. With no source, there is no answer | 21-question test set |
| 3. Detect | The Gap Radar reads maintenance history with four rules. It finds failure chains, lessons that did not travel, missing procedures, and data defects | 14 findings on the casebook data |
| 4. Validate | A senior engineer reviews every finding and draft, adds what only experience knows, and approves. Every action is logged | Review Queue |
| 5. Learn | Verified knowledge is used in the next answer. KPIs show whether the plant is learning | KPI baseline in Analytics |

**Design principle:** Rules decide the facts. AI explains them. Engineers approve them.

In a chemical plant, a confident wrong answer is dangerous. For this reason, exact values such as trip setpoints and voting logic are read by rules from structured data. A language model only explains retrieved evidence.

## Answers to the Three Key Questions

**Key Question 1. How can the Company build a structured Industrial Data Ops foundation to connect scattered plant knowledge sources?**
One parser per document type, one knowledge graph keyed by Equipment Tag, and automatic link and data-quality checks. Each type of information has one authority: EDMS for revision and status, the C&E matrix for trip settings, and AIMS for failures. This is Step 1 (Connect).

**Key Question 2. How can AI help engineers find trusted technical information faster and reduce the risk of improper execution?**
Rules decide the facts and AI explains them. Every answer shows source, approval status, and confidence. Conflicts are shown. The Hub refuses to answer when no source exists. This is Step 2 (Ask).

**Key Question 3. How can the Hub be integrated with operational systems to support reliability, troubleshooting, and continuous improvement?**
Read-only links to EDMS, AIMS, and the historian feed the Gap Radar and early warnings. Senior engineers validate the findings. Verified knowledge returns to the next answer. These are Steps 3 to 5 (Detect, Validate, Learn).

## Prototype Features

- **Home:** the evidence strip and the entry point to every page.
- **Assistant:** answers with source, approval status, and confidence. It shows conflicts between documents and refuses when no source exists.
- **Gap Radar:** four rules over the maintenance history. It includes a replay mode that compares its alerts with what actually happened.
- **Review Queue:** the full cycle from a Radar finding to a reviewed and verified OPL.
- **Live context:** one simulated vibration feed (VT-1201) with early warnings linked to limits, history, and OPLs.
- **Data quality:** metadata defects found in the documents, such as OPLs that cite the wrong asset.
- **Analytics:** baseline numbers, the impact scenario, KPIs, and the test set result.
- **Assets and Knowledge Graph:** a profile for each Equipment Tag and the links between assets, documents, and work orders.

## Business Impact

**Baseline (4 June 2024 to 6 December 2025):** 211 work orders, 31 breakdowns, 434 hours of downtime, and IDR 537.8 M of recorded cost. Corrective work is 25% of work orders and 56% of recorded cost.

**What earlier action could have addressed (a scenario, not a forecast):**

| Scenario | Events after the first signal | Downtime | Recorded cost |
| --- | --- | --- | --- |
| F1. Failure chain on GA-1201A, after the alert of 19 March 2025 | 2 | 6.5 h | IDR 12.6 M |
| F2. Gasket lesson across 4 assets, after the first case of 1 July 2024 | 3 | 22 h | IDR 35.2 M |
| **Total** | **5** | **28.5 h (6.6% of all downtime)** | **IDR 47.9 M (8.9% of recorded cost)** |

This is an upper bound in this sample. It is a hypothesis for engineers to test. Cost values in the casebook are dummy data. One of the five events has no cost recorded.

**KPIs and success metrics:**

| KPI | Baseline | Target |
| --- | --- | --- |
| Answers correct and cited (test set) | 21 of 21 on the rule layer of the prototype | About 85% in Phase 1 and 95% in Phase 2 for language-model answers |
| Time to find verified information | Measured in the first two weeks of the pilot | At least 50% shorter |
| Radar findings reviewed | 0 of 14 | 100% within 14 days |
| Open procedure gaps | 6 | 0, critical assets first |
| Work order data completeness | 88% | 98% or more |
| Documents with metadata defects | 28 OPLs, 9 P&ID tags, 8 interlock documents | 0 |

**How we will evaluate:**
1. Replay: run the Radar on history and compare its alerts with what happened.
2. Test set: 20 to 30 questions with known answers per unit.
3. Pilot: measure search time and first-time-right before and after.

## Feasibility and Roadmap

| Aspect | Approach |
| --- | --- |
| Technical | Parsers proven on all 96 casebook documents. Exact values by structured look-up. A private language model only explains retrieved evidence |
| Operational | Used in the browser with no change to core work. Approval follows the existing OPL pattern: supervisor reviews and manager approves |
| Legal | Data stays in company infrastructure. Personal names are protected under Indonesian Personal Data Protection Law No. 27/2022. Generated content is labelled and reviewed |
| Cybersecurity | Read-only. OT/IT segmentation, one-way historian replica, no write-back to DCS or safety systems, SSO and role-based access. In line with IEC 62443 zones and conduits |
| Data governance | One authority per information type. Missing data is shown and never estimated. Failure codes move to ISO 14224 |
| Organisational readiness | Reviewer role for senior engineers. Start with eight assets. KPIs reviewed in the reliability meeting |

**Roadmap with gates.** The next phase starts only after the gate is passed.

| Phase | Scope | Gate |
| --- | --- | --- |
| Phase 1 (months 1 to 3): Foundation and pilot | Eight LLDPE assets: parsers, knowledge graph, Assistant with a private language model, Radar rules, test set | About 85% of test questions correct and cited. The Radar reproduces the GA-1201A chain and the gasket lesson |
| Phase 2 (months 4 to 8): Expand and validate | More units by risk. Read-only connectors to EDMS and AIMS. Historian replica. ISO 14224 codes. Reviewer workflow live | 100% of findings reviewed within 14 days. Search time at least 50% shorter. Work order completeness at 98% |
| Phase 3 (months 9 to 12): Scale to a new plant | CA-EDC in its first operating year: capture commissioning and start-up lessons and onboard new staff with verified knowledge | New staff reach verified information in minutes. Zero open procedure gaps on critical assets |

**Top risks and mitigations:**
- A confident wrong answer: rules first, mandatory citation, refusal when no source exists, a test set, and a "Wrong" button that sends the answer to review.
- Fragile keyword rules: move to ISO 14224 failure codes.
- Reviewer workload: prioritised findings and structured drafts.

## What Is Real and What Is Simulated

We separate what is real, what is simulated, and what is planned.

| Status | Items |
| --- | --- |
| **Real** (computed from the casebook dataset) | 8 assets, 96 documents, 211 work orders. 39 C&E initiators with set points, voting, effects, and start permissives. 56 OPLs with steps, reviewer, and approver. All counts, links, and Radar findings |
| **Read once by a vision model, pending human check** | Instrument tags of the 8 P&ID images and their cross-check with the C&E matrix |
| **Simulated** | The live vibration values of VT-1201. Connections to EDMS, AIMS, and the historian |
| **Planned for the pilot** | Private language model, semantic retrieval, live connectors, SSO |

**Additional data source and its justification:** one simulated historian feed. The casebook asks for real-time operational data and Digital Twin integration, but the dataset contains none. The tag VT-1201, the 4.5 mm/s alarm, the 7.1 mm/s trip, and the weekly-rise rule all come from casebook documents.

## Technology

| Technology | Used for | Status |
| --- | --- | --- |
| Document AI (PDF parsers and a vision model for P&IDs) | Reading datasheets, C&E matrix, OPLs, GA drawings, and P&IDs | Prototype |
| Knowledge graph | Linking assets, documents, instruments, and work orders by Equipment Tag | Prototype |
| Rule engine | Gap Radar rules and trust rules of the Assistant | Prototype |
| Keyword retrieval | Finding records and documents | Prototype |
| Hybrid retrieval (keyword and embeddings) | Finding records when the wording differs, such as "weep" and "gasket relaxed" | Pilot |
| Private language model with RAG and citations | Writing explanations from retrieved evidence | Pilot |
| ISO 14224 failure codes | Replacing keyword-based failure families | Pilot |
| Read-only connectors, one-way DMZ | EDMS, AIMS, and historian | Pilot |

The prototype runs rules and keyword retrieval on the complete casebook dataset. It is a single self-contained HTML file.

## Repository Structure

```text
Veritag-Caliber2026/
├── index.html    # The full prototype (single file, no build step)
└── README.md     # This document
```

## Run Locally

No installation is needed.

1. Download `index.html` from this repository.
2. Open it in any modern browser (Chrome, Edge, Firefox, or Safari).

To clone the repository:

```bash
git clone https://github.com/narazla/Veritag-Caliber2026.git
cd Veritag-Caliber2026
```

Then open `index.html`.

## Known Limitations

- Cost values in the casebook are dummy data.
- The dataset is a small sample. Impact figures are a scenario and an upper bound, not a forecast.
- The Assistant in the prototype answers with rules and keyword retrieval. It does not answer free-form questions outside the casebook.
- Failure families are matched by keywords. ISO 14224 codes will replace them in the pilot.
- Radar findings are hypotheses for engineers to review.
- Connectors to EDMS, AIMS, and the historian are planned for the pilot. They are not connected in the prototype.
- The vibration feed of VT-1201 is simulated.
- P&ID tags were read once by a vision model and still need a human check.

## Team

**Team name:** Anti Hero Department
**University:** Universitas Diponegoro
**Supervisor:** Henri Tantyoko S.Kom., M.Kom.

| No. | Name | Major | Semester | Area of expertise | Contribution |
| --- | --- | --- | --- | --- | --- |
| 1 | Muhammad Helmi Abdulbaqi | Computer Science | 7 | Project Manager and Developer; rule-based systems | Built the interactive prototype (Assistant, Gap Radar, Review Queue); designed the system architecture and security approach. |
| 2 | Nazla Azzahra Hermana | Computer Science | 7 | Data analysis; research and concept design | Formulated the core concept and Gap Radar rules; analyzed the casebook data; defined KPIs and business impact. |
| 3 | Syahla Sandiani Assyifa Adam | Computer Science | 7 | Data storytelling; technical writing | Wrote the problem statement and pitch deck; researched and verified external sources; prepared the demo video narration. |

---

Built for **CALIBER 2026**, hosted by PT Chandra Asri Pacific Tbk.
