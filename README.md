# AI Drug Discovery Multi-Agent Panel

A Claude Code-powered multi-specialist consultation system for AI-driven drug development proposals and pipeline planning.

## Overview

This system provides a panel of **18 domain specialists** coordinated by an orchestrator whose primary objective is:

**Maximize evidence gathered and de-risking per unit of time and money spent.**

Designed for:
- RFP/proposal development for AI drug discovery initiatives
- Multi-agent AI architecture planning
- Pipeline decision support (prioritizing high-value experiments)
- Preclinical-clinical translation strategy
- Kill-early/fail-fast program management

## Specialist Panel (17 Experts)

### Biology & Target Discovery
| Specialist | Focus | Key Capabilities |
|------------|-------|------------------|
| **Systems Biologist** | Target ID, pathways | Multi-omics integration, network biology, causal inference |
| **Structural Biologist** | Protein structure | AlphaFold, binding sites, druggability assessment |

### Chemistry
| Specialist | Focus | Key Capabilities |
|------------|-------|------------------|
| **Computational Chemist** | Virtual screening | ADMET prediction, molecular simulation, generative chemistry |
| **Medicinal Chemist** | Lead optimization | SAR, drug-likeness, multi-parameter optimization |

### Preclinical Development
| Specialist | Focus | Key Capabilities |
|------------|-------|------------------|
| **Pharmacologist** | PK/PD | Efficacy models, dose prediction, therapeutic index |
| **Toxicologist** | Safety | IND-enabling studies, risk assessment, safety margins |
| **Translational Scientist** | Validation | Organoids, PDX, closed-loop AI validation |

### Data & AI
| Specialist | Focus | Key Capabilities |
|------------|-------|------------------|
| **Bioinformatician** | AI/ML architecture | Multi-agent systems, foundation models, data pipelines |
| **AI Scientist** | Model training | Closed-loop learning, evaluation, uncertainty quantification |
| **Functional Genomics Specialist** | Perturbation biology | CRISPR screens, drug response profiling, DepMap integration |
| **Clinical Data Scientist** | EMR/RWE | Korean healthcare data (HIRA, NHIS), outcomes research |
| **Biomarker Specialist** | CDx development | Companion diagnostics, liquid biopsy, patient selection |

### Drug Development
| Specialist | Focus | Key Capabilities |
|------------|-------|------------------|
| **CMC Specialist** | Manufacturing | Formulation, scale-up, quality by design |
| **Regulatory Specialist** | Strategy | IND/NDA, FDA/MFDS/EMA, expedited programs |

### Clinical
| Specialist | Focus | Key Capabilities |
|------------|-------|------------------|
| **Clinical Pharmacologist** | FIH design | Starting dose, escalation, human PK/PD |
| **Oncologist** | Disease expertise | Trial design, biomarker-driven development, combinations |

### Disease Area Experts
| Specialist | Focus | Key Capabilities |
|------------|-------|------------------|
| **Sarcoma Specialist** | Rare tumors | 70+ subtypes, fusion-driven sarcomas, orphan pathways |
| **Virologist** | BK virus | Polyomavirus biology, transplant populations, antivirals |

## Data Asset Mapping

For projects with clinical EMR + organoids + matched omics + perturbation data:

| Data Asset | Primary Specialists | Supporting |
|------------|---------------------|------------|
| **Clinical EMR** | Clinical Data Scientist | Oncologist, Biomarker Specialist |
| **Patient-Derived Organoids** | Translational Scientist | Functional Genomics, Oncologist |
| **Matched Multi-omics** | Systems Biologist, Bioinformatician | Biomarker Specialist |
| **Perturbation Readouts** | Functional Genomics Specialist | Computational Chemist, Systems Biologist |
| **EMR-Organoid-Omics Linkage** | Clinical Data Scientist + Bioinformatician | All above |

## Workflow Diagrams

See **[docs/workflow-diagram.md](docs/workflow-diagram.md)** for detailed Mermaid diagrams showing:
- Organic pipeline flow (with backtracking and iteration)
- Specialist team deployment patterns
- Decision gates and iteration cycles
- Closed-loop learning detail
- Backtracking triggers table
- Cross-stage consultation patterns

## Closed-Loop Architecture

The panel supports the agentic AI closed-loop system described in the RFP:

```
┌─────────────────────────────────────────────────────────────────┐
│  AI PREDICTION                                                  │
│  Systems Biologist + Computational Chemist + Bioinformatician   │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  EXPERIMENTAL VALIDATION                                        │
│  Translational Scientist + Functional Genomics Specialist       │
│  (Organoids, PDX, CRISPR screens, drug response)                │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ├───► Ground Truth Data ───┐
                              │                          │
                              ▼                          ▼
┌─────────────────────────────────────────────────────────────────┐
│  CLINICAL CORRELATION                                           │
│  Clinical Data Scientist + Oncologist + Biomarker Specialist    │
│  (EMR outcomes, patient stratification, real-world evidence)    │
└─────────────────────────────────────────────────────────────────┘
                              │                          │
                              └───► Outcome Labels ──────┤
                                                         │
                                                         ▼
                              ┌───────────────────────────────────┐
                              │  MODEL RETRAINING                 │
                              │  AI Scientist                     │
                              │  (continuous learning, evaluation,│
                              │   uncertainty quantification)     │
                              └───────────────────────────────────┘
                                                         │
                                                         ▼
                                            ┌────────────────────┐
                                            │  Improved Models   │
                                            │  → AI PREDICTION   │
                                            └────────────────────┘
```

## Pipeline Stage Coverage

```
Target Discovery ──► Hit Generation ──► Lead Optimization ──► Preclinical ──► IND ──► Clinical
      │                    │                   │                  │           │          │
Systems Biologist    Computational      Medicinal           Pharmacologist  Regulatory  Clinical
Structural Biologist    Chemist          Chemist            Toxicologist   Specialist  Pharmacologist
                    Functional Genomics                   Translational               Oncologist
                                                           Scientist                  Biomarker
                                                                                      Specialist
```

## Directory Structure

```
prompts/
├── orchestrator.md                   # Pipeline orchestrator
└── specialists/
    ├── systems_biologist.md
    ├── structural_biologist.md
    ├── computational_chemist.md
    ├── medicinal_chemist.md
    ├── pharmacologist.md
    ├── toxicologist.md
    ├── translational_scientist.md
    ├── bioinformatician.md
    ├── functional_genomics_specialist.md
    ├── clinical_data_scientist.md
    ├── ai_scientist.md
    ├── biomarker_specialist.md
    ├── cmc_specialist.md
    ├── regulatory_specialist.md
    ├── clinical_pharmacologist.md
    ├── oncologist.md
    ├── sarcoma_specialist.md
    └── virologist.md
```

## Specialist Prompt Structure

Each specialist includes:
- **Background & Expertise** - Domain knowledge and experience
- **Technical Frameworks** - Methods, tools, databases, terminology
- **Critical Questions** - What they always ask when consulted
- **Analytical Approach** - Systematic methodology
- **Communication Style** - How they present findings
- **Perspective** - Strengths and blind spots
- **Role in Pipeline** - Specific contributions

## Usage

Specialists can be invoked for:
1. **RFP/Proposal Writing** - Technical content generation
2. **Pipeline Review** - Multi-perspective assessment
3. **Decision Support** - Go/no-go recommendations
4. **Architecture Planning** - Multi-agent AI system design

## RFP Context

This panel was designed for the **2026 차세대바이오 AI Medicine 신약개발 전주기 멀티 Agent** proposal, addressing:

- Eroom's Law and drug development inefficiency
- Valley of Death (preclinical-clinical translation gap)
- Agentic AI vs. generative AI paradigm shift
- 2nd generation agent AI requirements (explainability, simulation-in-the-loop)
- Closed-loop learning with patient-derived models
- Korean clinical data infrastructure advantages (HIRA, NHIS, top cancer centers)
- First-in-Class drug development strategy

## Key Concepts

**Multi-Agent System Benefits:**
- Specialized expertise per domain
- Cross-validation between agents
- Reduced hallucination through adversarial collaboration
- Human-in-the-loop at critical decisions
- Simulation-in-the-loop for prediction verification

**Closed-Loop Learning:**
- AI predictions validated by wet lab experiments
- Patient-derived organoids provide ground truth
- Clinical outcomes feed back to model retraining
- Continuous improvement cycle

**Model-Agnostic Architecture:**
- Not dependent on specific LLM
- Swappable components as better models emerge
- Avoids vendor lock-in
