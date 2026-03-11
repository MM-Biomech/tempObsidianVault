## Purpose

This document defines the structure, rules, and intended use of the lab's Obsidian research vault.

Primary goals:

- accumulate literature knowledge across projects and researchers
    
- support both **method development** and **clinical insight discovery**
    
- enable **fast manuscript writing** from reusable knowledge
    
- capture both **conceptual insights** and **quantitative evidence**
    
- scale across **hundreds of papers and many gait metrics**
    

The vault is designed to function as a **long-term research knowledge system**, not simply a literature note repository.

---

# Core Design Principles

1. **One vault, not multiple vaults**  
    Method papers, clinical papers, and project ideas belong in the same system.
    
2. **Organize knowledge, not manuscripts**
    
3. **Paper notes provide context, not summaries**
    
4. **Insight notes capture reusable scientific claims**
    
5. **Reference data notes capture numerical evidence**
    
6. **Ontology nodes provide controlled vocabulary**
    
7. **Use links heavily to connect concepts**
    
8. **Extract minimally from papers**
    

Most papers should produce:

1–5 insight notes  
0–2 reference data notes

---

# Top-Level Folder Structure

00_Inbox/  
01_Papers/  
02_Insights/  
03_Ontology/  
    populations/  
    activities/  
    methods/  
    metrics/  
    metric_domains/  
    properties/  
04_Reference_Data/  
05_Projects/  
06_Manuscripts/  
_templates/

---

# Folder Roles

## 00_Inbox

Temporary location for incomplete or unprocessed notes.

---

## 01_Papers

One note per paper.

Paper notes serve as **navigation hubs linking insights and extracted data**.

---

## 02_Insights

Atomic scientific claims extracted from literature.

Insight notes are **the primary reusable knowledge unit**.

---

## 03_Ontology

Controlled vocabulary defining concepts used throughout the vault.

These provide the conceptual structure for linking knowledge.

---

## 04_Reference_Data

Structured numerical results extracted from papers.

These support insight notes with **quantitative evidence**.

---

## 05_Projects

Notes connecting literature knowledge to active research projects.

---

## 06_Manuscripts

Notes used to assemble manuscripts or sections of papers.

---

## _templates

Templates for creating standardized notes.

---

# Knowledge Model

The vault organizes research knowledge around the following conceptual structure:

Population × Activity × Metric × Property × Method

Example:

Multiple Sclerosis  
× Turning  
× Turn Duration  
× Reliability  
× Instrumented Insoles

This framework allows flexible connections between studies and findings.

---

# Ontology Structure

## Populations

Examples:

- Multiple Sclerosis
    
- Parkinson's Disease
    
- Healthy Adults
    
- CIDP
    

---

## Activities

Examples:

- Straight-line Walking
    
- Turning
    
- Stairs Up
    
- Stairs Down
    
- Free-living Walking
    

---

## Methods

Examples:

- Instrumented Insoles
    
- IMU
    
- Motion Capture
    
- Force Plates
    
- Activity Recognition
    

---

# Metric Domains

Metric domains organize large sets of gait variables into clinically meaningful categories.

The vault adopts the widely used gait framework consisting of the following domains:

- **Pace**
    
- **Rhythm**
    
- **Variability**
    
- **Asymmetry**
    
- **Postural Control**
    

Folder structure:

03_Ontology/  
    metric_domains/  
        Pace  
        Rhythm  
        Variability  
        Asymmetry  
        Postural Control

Metric nodes should link to their domain.

Example:

Stride Time  
Domain: [[Rhythm]]

Example relationships:

Stride Time → [[Rhythm]]  
Stride Length → [[Pace]]  
Stride Velocity → [[Pace]]  
Stride Time Variability → [[Variability]]  
Stride Time Asymmetry → [[Asymmetry]]  
Double Support Time → [[Postural Control]]

Domains allow retrieval of knowledge at multiple conceptual levels.

For example:

Metric level → Stride Time  
Domain level → Variability  
Conceptual level → gait asymmetry in multiple sclerosis

---

# Metrics

Examples:

- Stride Time
    
- Stride Length
    
- Stride Velocity
    
- Double Support Time
    
- Cadence
    

Metrics should link to their domain.

Example metric node:

# Stride Time  
  
Domain: [[Rhythm]]

---

# Properties

Properties describe the type of relationship being studied.

Examples:

- Reliability
    
- Variability
    
- Validation
    
- Sensitivity
    
- Detection
    
- Clinical Association
    

---

# Paper Notes (01_Papers)

Paper notes act as **navigation hubs**, not full summaries.

Most information remains in **Zotero or the PDF**.

Example structure:

---  
type: paper  
citekey: smithValidationInsoles2024  
year: 2024  
---  
  
# Smith et al. — Validation of Instrumented Insoles  
  
## Study Context  
  
Population:  
- [[Healthy Adults]]  
- [[Multiple Sclerosis]]  
- [[Parkinson's Disease]]  
  
Activity:  
- [[Straight-line Walking]]  
  
Methods:  
- [[Instrumented Insoles]]  
- [[Motion Capture]]  
  
Sample Size:  
Healthy: 20  
PwMS: 18  
PwPD: 15  
  
---  
  
## Metrics Studied  
  
- [[Stride Time]]  
- [[Stance Time]]  
- [[Swing Time]]  
- [[Stride Length]]  
- [[Cadence]]  
- [[Stride Velocity]]  
  
---  
  
## Key Insights Extracted  
  
- [[Instrumented insoles show small bias relative to motion capture]]  
- [[Stride velocity differs between MS and healthy adults]]  
  
---  
  
## Reference Data Extracted  
  
- [[smithValidationStudy2024 — Agreement Metrics]]  
- [[smithValidationStudy2024 — Group Differences]]  
  
---  
  
## Notes (Optional)  
  
Observations that may later become insights.

Paper notes should generally remain **short (100–200 words)**.

---

# Insight Notes (02_Insights)

Insight notes store **one reusable scientific claim**.

Example structure:

---  
type: insight  
population:  
activity:  
metric:  
property:  
source:  
citekey:  
---  
  
Claim statement.  
  
Evidence:  
Brief explanation of the finding.  
  
Reference Data:  
Links to supporting numerical tables if applicable.

Example title:

Stride velocity decreases with EDSS in multiple sclerosis

Insight notes are designed to be **directly reusable when writing manuscripts**.

---

# Reference Data Notes (04_Reference_Data)

Reference data notes store **numerical results extracted from papers**.

Typically:

- one table
    
- one dataset
    
- one group of numerical findings
    

Example note:

smithValidationStudy2024 — Agreement Metrics

Tables from papers may be pasted directly with minimal formatting.

Example:

Source: [[smithValidationStudy2024]]  
Citation: @smithValidationStudy2024  
  
| Metric | Population | Mean | Bias | LoA Upper | LoA Lower |  
|------|------|------|------|------|------|  
| [[Stride Time]] | [[Healthy Adults]] | 1.151 | -0.016 | 0.021 | -0.053 |  
| [[Stride Time]] | [[Multiple Sclerosis]] | 1.375 | -0.019 | 0.034 | -0.072 |

Metric names should be **linked to ontology nodes**.

This allows retrieval through backlinks.

---

# Query Strategy

The system relies on **links rather than rigid databases**.

Example workflow:

Search: Stride Time  
↓  
Open the Stride Time ontology page  
↓  
View backlinks  
↓  
See all insights and reference data mentioning this metric

This approach scales naturally as the vault grows.

---

# Minimal Workflow for Processing a Paper

1. Import paper into Zotero.
    
2. Create paper note in `01_Papers`.
    
3. Extract **1–5 insight notes**.
    
4. Extract **reference data notes if numerical values are important**.
    
5. Link insights and reference data to ontology nodes.
    

Typical processing time:

~5 minutes per paper

---

# Collaboration Rules

1. The vault is **shared knowledge infrastructure**.
    
2. Prefer linking existing ontology nodes rather than creating new ones.
    
3. Insight notes should remain short and reusable.
    
4. Reference data notes should capture only **numbers likely to be cited later**.
    
5. Avoid long summaries of papers.
    

---

# Conceptual Model of the Vault

Knowledge flows through three layers:

Paper → Insight → Reference Data

Paper notes provide context.

Insight notes capture reusable scientific claims.

Reference data notes capture supporting numerical evidence.

Ontology nodes provide the conceptual framework connecting everything.