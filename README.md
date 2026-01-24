[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![FHIR](https://img.shields.io/badge/standard-FHIR%20R4-success.svg)](https://www.hl7.org/fhir/)
[![Governance](https://img.shields.io/badge/focus-AI%20Governance-purple.svg)](#)
[![Reproducibility](https://img.shields.io/badge/reproducibility-fixed--seed%20simulation-green.svg)](#reproducibility)
[![Release](https://img.shields.io/badge/release-v1.0--manuscript-blueviolet.svg)](#release)
[![Status](https://img.shields.io/badge/status-research-lightgrey.svg)](#)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.18356747.svg)](https://doi.org/10.5281/zenodo.18356747)


# Adaptive FHIR-Native AI Governance for Clinical Decision Support  
## A modular, auditable deployment framework for real-world clinical AI

This repository implements a **FHIR-native governance layer** for clinical decision support systems.  
The framework governs **how predictive models are deployed**, not how they are trained.

Rather than introducing new predictive models, this project provides **deployment governance infrastructure** that enables:

- Adaptive model selection across heterogeneous clinical contexts  
- Explicit encoding of safety and resource tradeoffs  
- Machine-readable audit and provenance generation  
- Deterministic reconstruction of deployment decisions  

The core contribution is **governance**, not prediction.

> Research use only. This codebase is intended for methodological evaluation and does not constitute a clinical decision support system.

---

## Release

This repository is maintained with manuscript-anchored releases.  
The manuscript-associated snapshot is tagged as:

- `v1.0-manuscript`

---

## Keywords

Clinical AI governance; FHIR-native infrastructure; clinical decision support; deployment quality control; adaptive model selection; auditability; provenance; interoperability; reproducible research

---

## Why this exists

Clinical AI systems rarely fail because accurate models cannot be built.  
They fail because **deployment strategies are static, opaque, and ungoverned**.

In many production environments, a single model and threshold are applied uniformly across heterogeneous patients, care settings, and time periods. This repository reframes deployment as a **sequential decision problem** and evaluates whether standardized FHIR context can be used to govern model selection while producing **auditable, interoperable accountability artifacts**.

---

## Core concept

A deployment governance engine that:

1. Receives patient and encounter context via HL7 FHIR resources  
2. Selects a model from a portfolio of frozen, independently validated models  
3. Applies explicit cost functions reflecting safety and resource sensitivity  
4. Logs each deployment decision as FHIR Provenance and FHIR AuditEvent resources  
5. Enables deterministic post hoc reconstruction of decision pathways  

No model retraining.  
No feature learning.  
No vendor lock-in.

---

## System architecture

The framework is organized into **three strictly separated layers**.

### 1. Data layer
- HL7 FHIR R4 resources serve as the canonical representation of clinical context  
- Synthetic FHIR datasets support public, reproducible demonstrations  
- Optional local mapping from restricted-access clinical data supports validation  
- Context derivation is deterministic and rule based

### 2. Governance layer
- Policy engine performs contextual, cost-aware selection among models  
- Policies update internal state but never modify model parameters  
- Governance logic is evaluated independently of model internals  
- Standardized audit and provenance artifacts are emitted automatically

### 3. Execution layer
- Existing predictive models, clinical risk calculators, or rule-based systems are treated as interchangeable decision arms  
- Model internals are opaque to governance logic

Detailed specifications are provided in:
- `docs/01_architecture.md`
- `docs/02_governance_design.md`
- `docs/03_audit_and_provenance.md`

---

## Research questions

1. Can standardized FHIR resources provide sufficient contextual signal for adaptive deployment governance without bespoke feature engineering  
2. Does adaptive model selection reduce safety-relevant error compared with static deployment strategies  
3. Can audit and provenance artifacts be generated automatically using native FHIR resources  
4. Can safety and cost tradeoffs be governed without retraining predictive models  

---

## Data strategy

### Public, shareable data
- Synthetic FHIR datasets generated with Synthea  
- Used for tutorials, tests, and all reproducible analyses  

### Restricted research data
- Optional local validation using MIMIC-IV mapped to FHIR  
- No patient-level data are redistributed  
- Only aggregate outputs are reported  

See:
- `docs/04_data_sources_and_privacy.md`
- `data/README.md`

---

## Sequential computation framework

All analyses follow a **numbered, fixed-seed execution pipeline**.  
This structure ensures that **every figure and table is traceable to a specific step**.

| Step | Description |
|-----:|------------|
| Step 0 | Define global configuration (policies, costs, horizon, seed) |
| Step 1 | Build deterministic clinical context from FHIR |
| Step 2 | Simulate sequential deployment decisions |
| Step 3 | Compute safety-weighted error metrics |
| Step 4 | Compute cumulative policy regret |
| Step 5 | Generate FHIR AuditEvent and Provenance artifacts |
| Step 6 | Validate audit completeness and reconstructability |
| Step 7 | Generate execution manifest and metadata |
| Step 8 | Produce publication-ready figures and tables |

See `docs/07_reproducibility.md` for full details.

---

## Repository contents

- `docs/` Manuscript-aligned documentation, governance rationale, policy alignment  
- `fhir/ig/` FHIR profiles, value sets, and example resources  
- `governance/` Policy definitions, cost models, model registry interfaces, audit logging templates  
- `analysis/` Scripted pipelines implementing Steps 0–8  
- `simulations/` Configuration-driven experiments and outputs  
- `figures/` Manuscript-ready diagrams and plots  
- `tests/` Unit tests for governance logic, audit completeness, and FHIR validity  

---

## Quickstart

### Path A: Public demonstration using synthetic FHIR data
1. Place Synthea FHIR bundles in `data/public/synthea/`  
2. Run context construction (Step 1)  
3. Execute governance simulation (Step 2)  
4. Compute metrics and generate figures and tables (Steps 3–8)  

### Path B: Optional local validation using restricted data
1. Obtain authorized access to MIMIC-IV through PhysioNet  
2. Map required tables to FHIR resources locally  
3. Execute the identical governance pipeline  
4. Report aggregate results only  

Detailed instructions:
- `docs/00_overview.md`

---

## Evaluation plan

### Governance performance outcomes
- Cumulative safety-weighted error  
- Policy regret relative to an oracle selector  
- Stability of model selection across contexts  

### Accountability outcomes
- Audit completeness  
- Deterministic reconstructability from FHIR artifacts  

See `docs/05_evaluation_plan.md`.

---

## Reproducibility

This repository is designed for meaningful reuse and extension.

- Fixed-seed, deterministic simulation runs  
- Explicit separation of shareable and restricted data  
- Configuration-driven experiments  
- Manifest-based provenance for all outputs  

All reported results can be regenerated from source using the numbered steps.  
See `docs/07_reproducibility.md`.

---

## Repository structure

```text
fhir-ai-governance/
├── CITATION.cff
├── LICENSE
├── README.md
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── SECURITY.md
├── .github/
│   └── workflows/
├── docs/
├── fhir/
├── governance/
├── data/
├── analysis/
├── simulations/
├── figures/
└── tests/
---

## Repository details

See the full directory tree in the repository for implementation details.

---

## Citation

If you use this repository in academic, clinical, or policy-facing work, please cite the software and the associated manuscript or preprint when available.

A `CITATION.cff` file is included to support GitHub-native citation workflows and standardized software citation.

---

## License

This project is released under the MIT License.  
See the `LICENSE` file for full terms.

---

## Contact

**Julian Borges, MD, MSc**  
MS Health Informatics, Computer Science  
Boston University Metropolitan College  
Email: jyborges@bu.edu
