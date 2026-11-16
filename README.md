
# Cross-Domain Railway Assurance Consistency Analysis

## Overview

This repository provides supplementary evaluation artefacts for a research study on evidence-aware cross-domain assurance consistency analysis in railway cyber-physical systems.

The study examines how documented dependencies among functional safety, cybersecurity, and AI assurance records affect the support of assurance claims.

A deterministic consistency-checking method is evaluated using 30 controlled scenarios based on an illustrative AI-assisted railway infrastructure-monitoring application. The evaluation concerns the consistency of documented assurance information, not the operational performance of the AI model.

## Repository Contents

| File / Directory | Description |
|---|---|
| `reference_model.json` | Reference assurance graph containing seven records and five directed relationships across safety, cybersecurity, and AI viewpoints. |
| `cases/` | JSON input files for 30 controlled evaluation scenarios. |
| `case_manifest.json` | Scenario identifiers, categories, input references, and descriptions of the introduced conditions. |
| `oracle.json` | Pre-specified reference outcomes, including expected claim-support statuses, diagnostic categories, and affected records. |
| `results.csv` | Recorded evaluation results for the domain-local and cross-domain configurations. |

## Assurance Reference Model

The illustrative application uses sensor measurements to support railway infrastructure maintenance and diagnostic decisions. It does not directly control train movements.

The reference graph contains five assurance record types:

- **CLAIM:** Proposition requiring documented assurance support.
- **ASSUMPTION:** Condition necessary for supporting an assurance claim.
- **REQUIREMENT:** Expected system property or behaviour.
- **CONTROL:** Measure addressing a requirement.
- **EVIDENCE:** Information used to evaluate an assurance condition.

The graph defines four relationship types:

- `REQUIRES_ASSUMPTION`: Identifies a required assumption.
- `SUPPORTED_BY`: Connects an assurance record to supporting evidence.
- `DEPENDS_ON`: Represents a necessary dependency.
- `ADDRESSES_REQUIREMENT`: Provides structural traceability between a control and a requirement.

The last relationship does not propagate claim-support status.

The analysis uses three support statuses:

- **T — Established:** All applicable mandatory support obligations are satisfied.
- **F — Violated:** A modelled condition or mandatory support obligation is established as violated.
- **U — Unresolved:** Available information does not establish support or a violation, including cases involving missing, inapplicable, or conflicting evidence.

These statuses describe documented assurance support. They are not safety classifications or certification decisions.

## Evaluation Scenarios

The dataset comprises 30 controlled scenarios organised into five categories.

| Category | Scenario IDs | Cases |
|---|---|---:|
| Intact and negative controls | I-01–I-06 | 6 |
| Missing or unresolved support | M-01–M-06 | 6 |
| Contradictory evidence | C-01–C-06 | 6 |
| Evidence applicability | A-01–A-06 | 6 |
| Cross-domain dependencies | X-01–X-06 | 6 |
| **Total** | | **30** |

The scenarios examine missing support, contradictory evidence, evidence applicability, necessary dependency propagation, alternative support paths, and preservation of unrelated claim statuses.

The six intact or negative-control scenarios are distinguished from the 24 scenarios containing deliberately introduced assurance defects.

## Evaluation Configurations

Each scenario is evaluated under two configurations of the same consistency-checking method.

### B0 — Domain-Local Analysis

Relationships connecting records from different assurance viewpoints are excluded. Local evidence evaluation, applicability assessment, and contradiction checking remain available.

### B1 — Cross-Domain Analysis

The complete assurance graph is evaluated, including declared relationships between safety, cybersecurity, and AI assurance records.

Both configurations use the same reasoning semantics and evidence inputs. Only the available relationships differ.

B0 is an information-ablation configuration, not an independent competing algorithm. Both configurations are compared against the same pre-specified reference outcomes derived from the complete assurance graph.

## Reference Outcomes and Results

The `oracle.json` file contains reference outcomes specified from the defined assurance semantics before checker execution. These outcomes were maintained separately from the checker implementation.

The `results.csv` file contains 60 evaluation records, corresponding to 30 scenarios evaluated under B0 and B1.

The evaluation compares:

- Claim-support status agreement.
- Diagnostic finding-category agreement.
- Affected-record agreement.
- Case-level precision and recall.

Agreement requires the recorded output to match the corresponding pre-specified reference outcome.

### Principal Results

| Measure | B0 | B1 |
|---|---:|---:|
| Claim-status agreement, defective scenarios | 19/24 | 24/24 |
| Claim-status agreement, intact controls | 1/6 | 6/6 |
| Finding-category agreement, defective scenarios | 22/24 | 24/24 |
| Affected-record agreement, defective scenarios | 22/24 | 24/24 |
| Case-level precision | 24/29 | 24/24 |
| Case-level recall | 24/24 | 24/24 |

A scenario is classified as positive when its principal claim has status F or U, or when a diagnostic finding is reported.

Both configurations classified all 24 defective scenarios as positive. However, B0 also classified five intact controls as positive because their principal claims remained unresolved.

The results illustrate the effect of excluding cross-domain dependency information. They do not demonstrate general algorithmic superiority over other assurance methods.

## Inspecting the Evaluation

The evaluation data can be inspected as follows:

1. Open `reference_model.json` to examine the reference assurance graph.
2. Consult `case_manifest.json` to identify each scenario and its intended modification.
3. Examine the corresponding JSON file in `cases/`.
4. Compare the expected outcomes recorded in `oracle.json`.
5. Inspect `results.csv` to compare the B0 and B1 outputs.

The repository provides evaluation inputs, pre-specified expected outcomes, and recorded results.

The executable consistency checker and automated experiment runner are not included. Consequently, the repository supports inspection and independent analysis of the evaluation data but does not provide a complete executable reproduction package.

## Scope and Limitations

The evaluation uses constructed assurance scenarios based on an illustrative advisory railway infrastructure-monitoring application.

The scenarios test the defined assurance representation and consistency semantics under controlled conditions. The reference outcomes are derived from those semantics rather than independently observed industrial ground truth.

The evaluation does not assess:

- Operational AI-model performance.
- Complete execution of the BPMN-based assurance workflow.
- Integration with Jira or other workflow management systems.
- Industrial-scale assurance models.
- Actual railway safety or regulatory compliance.

The consistency analysis is intended to support engineering assessment, change-impact analysis, and assurance reviews. Final safety and certification judgments remain the responsibility of qualified assessors.

## Supplementary Research Artefacts

These materials are provided to support transparency, inspection of the experimental design, and assessment of the reported results.
