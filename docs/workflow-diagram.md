# AI Drug Discovery Pipeline - Orchestrator Workflow

## Core Objective

**Maximize evidence gathered and de-risking per unit of time and money spent.**

The orchestrator continuously asks:
- What's the highest-value question to answer next?
- What's the cheapest experiment that could kill this program?
- What can we run in parallel vs. what must be sequential?
- Are we learning fast enough for the resources deployed?

## Organic Pipeline Flow

The orchestrator manages a non-linear, iterative workflow where stages can cycle, backtrack, or jump based on experimental outcomes and strategic decisions.

```mermaid
flowchart TB
    O[ORCHESTRATOR]

    subgraph TARGET[Target Discovery]
        T1[Hypothesis] --> T2[Validation] --> T3[Assessment]
    end

    subgraph HIT[Hit Generation]
        H1[Virtual Screen] --> H2[Exp Hits] --> H3[Prioritize]
    end

    subgraph LEAD[Lead Optimization]
        L1[SAR] --> L2[Optimize] --> L3[Candidate]
    end

    subgraph PRECLIN[Preclinical]
        P1[Efficacy] --> P2[Safety] --> P3[IND Package]
    end

    subgraph CLINICAL[Clinical]
        C1[FIH] --> C2[Dose Esc] --> C3[Expansion]
    end

    O --> TARGET --> HIT --> LEAD --> PRECLIN --> CLINICAL

    H3 -.->|no hits| T1
    L3 -.->|props fail| H1
    P2 -.->|safety| L1
    P1 -.->|efficacy gap| T1
    C2 -.->|PK issue| L2
```

## Closed-Loop Learning

```mermaid
flowchart LR
    subgraph PREDICT[AI Predictions]
        P1[Target pred]
        P2[Property pred]
        P3[Response pred]
    end

    subgraph VALIDATE[Validation]
        V1[Organoids]
        V2[CRISPR]
        V3[Clinical]
    end

    subgraph LEARN[Retraining]
        L1[Compare]
        L2[Analyze]
        L3[Retrain]
    end

    P1 --> V2
    P2 --> V1
    P3 --> V3

    V1 --> L1
    V2 --> L1
    V3 --> L1

    L1 --> L2 --> L3
    L3 --> P1
    L3 --> P2
    L3 --> P3
```

## Specialist Teams

```mermaid
flowchart LR
    O[Orchestrator]

    subgraph BIO[Biology]
        B1[Systems Bio]
        B2[Structural Bio]
        B3[Func Genomics]
    end

    subgraph CHEM[Chemistry]
        C1[Comp Chem]
        C2[Med Chem]
    end

    subgraph PRE[Preclinical]
        R1[Pharmacologist]
        R2[Toxicologist]
        R3[Translational]
    end

    subgraph DATA[Data/AI]
        D1[Bioinfortic]
        D2[AI Scientist]
        D3[Clinical Data]
        D4[Biomarker]
    end

    subgraph DEV[Development]
        E1[CMC]
        E2[Regulatory]
    end

    subgraph CLIN[Clinical]
        F1[Clin Pharm]
        F2[Oncologist]
        F3[Disease Expert]
    end

    O --> BIO
    O --> CHEM
    O --> PRE
    O --> DATA
    O --> DEV
    O --> CLIN
```

## Kill Early Funnel

```mermaid
flowchart LR
    subgraph CHEAP[Cheap - Do First]
        C1[Literature]
        C2[In silico]
        C3[Cell assays]
        C4[Organoids]
    end

    subgraph MED[Medium Cost]
        M1[SAR]
        M2[PK]
        M3[Pilot tox]
    end

    subgraph EXP[Expensive - Do Last]
        X1[GLP tox]
        X2[Scale-up]
        X3[Clinical]
    end

    C1 --> C2 --> C3 --> C4 --> M1 --> M2 --> M3 --> X1 --> X2 --> X3

    C1 -.-> STOP((X))
    C2 -.-> STOP
    C3 -.-> STOP
    C4 -.-> STOP
    M1 -.-> STOP
```

## De-Risking Prioritization

```mermaid
flowchart TB
    Q1[List uncertainties] --> Q2[Estimate impact]
    Q2 --> Q3[Estimate cost]
    Q3 --> Q4[Calculate value/cost]
    Q4 --> Q5[Prioritize]

    Q5 --> E1[HIGH value: Organoid validation]
    Q5 --> E2[MED value: Selectivity panel]
    Q5 --> E3[LOW value: Full PK study]

    E1 -->|do first| E2 -->|do second| E3
```

## Backtracking Triggers

| Current Stage | Backtrack To | Trigger | Specialists |
|---------------|--------------|---------|-------------|
| Hit Gen | Target | No druggable chemotypes | Struct Bio → Systems Bio |
| Lead Opt | Hit Gen | SAR flat | Med Chem → Comp Chem |
| Lead Opt | Target | Mechanism invalid | Pharm → Systems Bio |
| Preclinical | Lead Opt | Safety margins | Tox → Med Chem |
| Preclinical | Target | Efficacy gap | Translational → Systems Bio |
| Clinical | Lead Opt | Human PK differs | Clin Pharm → Med Chem |
| Clinical | Target | Biomarker fails | Biomarker → Systems Bio |

## Decision: Parallel vs Sequential

**Run in Parallel when:**
- Experiments are independent
- Both answers needed anyway
- Time is the main constraint

**Run Sequentially when:**
- Result A determines if B is worth doing
- Resources are limited
- One experiment could kill program

| Parallel OK | Sequential Required |
|-------------|---------------------|
| Multiple compound synthesis | Target validation → then screening |
| Target validation + hit screening | Hit confirmation → then optimization |
| PK study + efficacy study | Safety → then IND filing |
| Different tumor organoid types | FIH results → then expansion design |
