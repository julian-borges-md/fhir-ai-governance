[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![FHIR](https://img.shields.io/badge/standard-FHIR%20R4-success.svg)](https://www.hl7.org/fhir/)
[![Governance](https://img.shields.io/badge/focus-AI%20Governance-purple.svg)](#)
[![Reproducibility](https://img.shields.io/badge/reproducibility-simulation%20based-green.svg)](#reproducibility)
[![Status](https://img.shields.io/badge/status-research-lightgrey.svg)](#)

# FHIR Native AI Governance for Clinical Decision Support  
## A modular governance layer for audit aware model selection using real world EHR data

This repository implements a FHIR native governance layer for clinical decision support systems. The framework selects among pre validated clinical prediction models using patient context represented through FHIR resources. The core contribution is not a new predictive model. It is a deployment governance framework that enables adaptive model selection, systematic decision logging, and safety monitoring using standardized audit artifacts.

### Keywords: clinical AI governance, FHIR native infrastructure, clinical decision support, adaptive model selection, multi armed bandits, auditability, provenance, real world EHR data, interoperability, reproducible research

---

## Why this exists

Clinical AI systems rarely fail because accurate models cannot be constructed. They fail because deployment strategies are static.

In many production environments, a single model and a single threshold are applied uniformly across heterogeneous patients, care settings, and time periods. This project reframes deployment as a sequential decision problem and evaluates whether FHIR native clinical context can be used to govern model selection decisions while producing machine readable audit and provenance artifacts.

---

## Core idea

A governance policy engine that:

1. Receives patient context through FHIR resources  
2. Selects a model from a portfolio of frozen and independently validated models  
3. Applies explicit cost functions for clinical errors and resource utilization  
4. Logs each decision as FHIR Provenance and FHIR AuditEvent  
5. Supports post hoc reconstruction of decision pathways

---

## Architecture

The framework is organized into three layers.

### 1. Data layer  
FHIR resources serve as the canonical interface for patient context. Public synthetic FHIR datasets are included for reproducible demonstrations. Optional local mapping from MIMIC IV to FHIR supports research validation.

### 2. Governance layer  
A policy engine performs contextual and cost aware selection among models and emits standardized audit artifacts.

### 3. Execution layer  
Existing predictive models, clinical risk calculators, or rule based baselines are treated as interchangeable decision arms.

Additional details are provided in `docs/01_architecture.md` and `docs/03_audit_and_provenance.md`.

---

## Research questions

1. Can standardized FHIR resources provide sufficient contextual signal to support adaptive, real time AI deployment governance without bespoke feature engineering  
2. Does adaptive model selection reduce harmful clinical errors compared with static deployment policies  
3. Can audit artifacts be generated automatically using FHIR Provenance and FHIR AuditEvent  
4. Can safety and cost improvements be achieved without retraining predictive models

---

## Data strategy

### Public and shareable data  
Synthea generated FHIR datasets are used for examples, tests, and tutorial workflows.

### Research validation data  
Optional local experiments use MIMIC IV data mapped to FHIR. MIMIC IV data are not redistributed in this repository. Only aggregate and summary results are reported.

See `docs/04_data_sources_and_privacy.md` and `data/README.md` for details.

---

## Repository contents

- `docs/` Manuscript ready technical documentation and alignment statements  
- `fhir/ig/` FHIR profiles, value sets, and example resources used by the governance layer  
- `governance/` Policy design, cost models, model registry interfaces, and audit logging templates  
- `analysis/` Reproducible analysis pipelines in Python and R  
- `simulations/` Configuration driven experiments and outputs  
- `figures/` Manuscript ready plots and diagrams  
- `tests/` Unit tests for governance logic and audit completeness

---

## Quickstart

This repository supports two execution paths.

### Path A: Public demonstration with synthetic FHIR data  
1. Generate or download a Synthea FHIR bundle into `data/public/synthea/`  
2. Run cohort construction and context feature extraction  
3. Execute the governance simulation  
4. Generate figures and summary tables

### Path B: Research validation with MIMIC IV  
1. Obtain MIMIC IV access through PhysioNet  
2. Map required tables to FHIR resources locally  
3. Run the identical governance policy and evaluation pipeline  
4. Report aggregate results only

Detailed instructions are provided in `docs/00_overview.md` and `analysis/python/00_setup.py`.

---

## Evaluation plan

### Primary outcomes
- Safety weighted error measures under explicit cost functions  
- Resource utilization proxies where applicable  
- Policy regret relative to an oracle model selector  
- Stability of model selection across patient contexts

### Audit outcomes
- Completeness of decision logs  
- Reconstructability of decision pathways from FHIR artifacts

See `docs/05_evaluation_plan.md` for details.

---

## Reproducibility

This repository is designed for meaningful reuse and extension.

- Public synthetic datasets enable fully runnable examples  
- Configuration driven simulations support transparent evaluation  
- Deterministic pipelines are used where feasible  
- Shareable and non shareable data are explicitly separated

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
├── .gitignore
├── .github/
│   ├── workflows/
│   │   ├── ci.yml
│   │   └── lint.yml
│   └── ISSUE_TEMPLATE/
│       ├── bug_report.yml
│       ├── feature_request.yml
│       └── question.yml
├── docs/
│   ├── 00_overview.md
│   ├── 01_architecture.md
│   ├── 02_governance_design.md
│   ├── 03_audit_and_provenance.md
│   ├── 04_data_sources_and_privacy.md
│   ├── 05_evaluation_plan.md
│   ├── 06_NIH_AIM_AHEAD_alignment.md
│   └── 07_reproducibility.md
├── fhir/
│   ├── ig/
│   │   ├── README.md
│   │   ├── profiles/
│   │   ├── value-sets/
│   │   ├── examples/
│   │   └── terminology/
│   └── mapping/
│       ├── mimic_to_fhir.md
│       └── synthea_notes.md
├── governance/
│   ├── README.md
│   ├── policies/
│   │   ├── contextual_bandit.md
│   │   ├── cost_model.md
│   │   └── baselines.md
│   ├── logging/
│   │   ├── provenance.md
│   │   └── auditevent.md
│   └── interfaces/
│       ├── model_registry.md
│       └── fhir_context.md
├── data/
│   ├── README.md
│   ├── public/
│   │   └── synthea/
│   └── local/
│       └── mimic/
├── analysis/
│   ├── python/
│   │   ├── 00_setup.py
│   │   ├── 01_build_cohort.py
│   │   ├── 02_extract_context_features.py
│   │   ├── 03_register_models.py
│   │   ├── 04_run_governance_simulation.py
│   │   ├── 05_make_tables_figures.py
│   │   └── utils/
│   └── R/
│       ├── 00_setup.R
│       ├── 01_build_cohort.R
│       ├── 02_extract_context_features.R
│       ├── 03_register_models.R
│       ├── 04_run_governance_simulation.R
│       ├── 05_make_tables_figures.R
│       └── utils/
├── simulations/
│   ├── README.md
│   ├── configs/
│   ├── results/
│   └── notebooks/
├── figures/
│   └── README.md
└── tests/
    ├── test_governance_policy.py
    ├── test_audit_logging.py
    └── test_fhir_examples.py

## Citation

If you use this repository, please cite the software and the associated preprint when available.  
A `CITATION.cff` file is included to support GitHub native citation workflows.

## License

MIT License. See `LICENSE`.

## Contact author

Julian Borges, MD, MSc  
MS Health Informatics, Computer Science Department  
Boston University, Metropolitan College  
Email: jyborges@bu.edu

