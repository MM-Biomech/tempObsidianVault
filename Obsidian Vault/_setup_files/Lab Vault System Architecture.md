> **New to this vault?** Start with `_setup_files/QUICKSTART.md` — it covers software setup, plugin installation, and a step-by-step first paper walkthrough. Return here once you are up and running for full architectural detail.

> **Using an AI assistant?** See `_setup_files/LLM_CONTEXT.md` for a concise machine-readable summary of the vault's research domain, note types, and conventions.

---

## Purpose

This document defines the structure, rules, and intended use of the lab's Obsidian research vault.

The vault is designed to function as a **long-term research knowledge system**, not simply a literature note repository.

Primary goals:

- accumulate literature knowledge across projects and researchers
    
- support both **method development** and **clinical insight discovery**
    
- enable **fast manuscript writing** from reusable notes
    
- capture both **conceptual insights** and **quantitative evidence**
    
- scale across **hundreds of papers and many gait metrics**
    

The system separates **sources, insights, and numerical evidence** so knowledge remains reusable across projects.

---

# Core Design Principles

1. **One vault, not multiple vaults**
    
    Method papers, clinical papers, and project ideas belong in the same system.
    
2. **Organize knowledge, not manuscripts**
    
3. **Paper notes provide context, not summaries**
    
4. **Insight notes capture reusable scientific claims**
    
5. **Reference data notes capture numerical evidence**
    
6. **Ontology nodes define shared vocabulary**
    
7. **Use links aggressively**
    
8. **Extract minimally from papers**
    

Typical output from one paper:

1–5 insight notes  
0–2 reference data notes

---

# Relationship Between Zotero and Obsidian

Zotero and Obsidian serve different roles.

## Zotero

Zotero is the **bibliographic database** and should store:

- authors
- journal
- publication year
- DOI
- abstract
- keywords
- PDFs
- citation metadata

These should **not be duplicated inside Obsidian properties**.

---

## Obsidian

Obsidian stores:

- conceptual knowledge
- insights extracted from literature
- relationships between concepts
- numerical reference values

Obsidian functions as a **knowledge graph built on top of the literature database**.

---

## Required Zotero Plugin: Better BibTeX

**Better BibTeX (BBT)** is a Zotero plugin (not an Obsidian plugin) that must be installed for the Zotero Integration connection to work.

Install it from: [retorque.re/zotero-better-bibtex/installation/](https://retorque.re/zotero-better-bibtex/installation/)

What it does:
- Generates stable, unique **citekeys** for every item in your library (e.g. `kim2026InsoleDerivedPlantar`)
- Exposes a **local JSON-RPC API** that the Zotero Integration Obsidian plugin uses to search your library and retrieve metadata and annotations on import
- Optionally auto-exports a `.bib` file (not needed for this vault — manuscripts use the Zotero Word plugin)

**Citekey format:** All lab members must use the same BBT citekey format to ensure citekeys are consistent across the shared library. The recommended format is:

```
[auth:lower][year][title:select:1:1:capitalize][title:select:2:2:capitalize][title:select:3:3:capitalize]
```

This produces keys like `kim2026InsoleDerivedPlantar`. Configure this in Zotero → Better BibTeX → Open Better BibTeX Preferences → Citation Keys.

**Pin citekeys after creation:** Once a paper note has been created with a citekey, that key should not change. Right-click any Zotero item → Better BibTeX → Pin BibTeX key. This prevents the key from regenerating if BBT settings change.

---

## Team Literature Sharing

The lab uses **Zotero Groups** for shared literature — this is the Zotero equivalent of Mendeley's shared libraries.

### How it works

1. A group library is created on [zotero.org](https://www.zotero.org/groups/)
2. All lab members join the group (invite by email)
3. Papers added to the group library automatically sync to all members' Zotero clients
4. PDFs sync through Zotero's servers (subject to storage limits — see below)
5. Each member's BBT generates the same citekey for each paper (if configured identically)

**What syncs through Zotero (not Git):**
- Paper metadata (authors, title, journal, year, DOI, abstract)
- PDFs and other attachments
- Zotero annotations and highlights (the raw source for Zotero Integration imports)
- Tags and collections

**What syncs through Git (this repo):**
- Obsidian paper notes, insight notes, reference data, ontology nodes
- Templates, dashboards, architecture documentation
- Plugin code and settings

PDFs and `.bib` files are **not stored in this Git repository**. Git is not suited for large binary files, and Zotero is already handling PDF sync.

### Storage limits

| Plan | Storage | Cost |
|---|---|---|
| Free | 300 MB | — |
| 2 GB | 2 GB | $20/year |
| 6 GB | 6 GB | $60/year |
| Unlimited | Unlimited | $120/year |

Storage applies to file attachments (PDFs). Metadata syncs for free regardless of plan. For a shared group library with many PDFs, the 2 GB or 6 GB plan is recommended.

**Alternative (free unlimited PDF storage):** Use **WebDAV** to store attachments on your own server or a supported cloud service (Koofr offers free WebDAV). Configure this in Zotero → Preferences → Sync → File Syncing → WebDAV.

---

## Obsidian Plugin Roles

The Zotero Integration plugin handles the full connection between Zotero and Obsidian.

| Plugin | Role |
|---|---|
| **Zotero Integration** | Importing highlights, annotations, and metadata into paper notes |

Citation management for manuscripts (Word) is handled directly through the **Zotero Word plugin** — not through any Obsidian plugin.

---

## Zotero Integration: How It Works

The Zotero Integration plugin uses a **Nunjucks template** (`_templates/zotero_paper_notes.md`) to render a paper note from a Zotero item.

On import, it:

- pulls bibliographic metadata (`citekey`, `year`, etc.)
- pulls all PDF annotations and routes them by highlight color into the correct section of the note

On **re-import** (after adding new highlights in Zotero):

- updates the imported content
- preserves any sections you have manually edited in Obsidian, using `%% begin ... %%` / `%% end ... %%` persist markers

**Persist marker behavior:**
- Sections wrapped in persist markers are protected from re-import overwrite
- Once you have edited content inside a persist block, that content is permanently preserved by subsequent imports
- If a persist block is messy, edit it directly in Obsidian — re-import will not fix it

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
    Clinical Measure/
04_Reference_Data/  
05_Projects/  
06_Manuscripts/  
_setup_files/  
_templates/

---

# Folder Roles

## 00_Inbox

Temporary location for incomplete or unprocessed notes.

Also contains `changelog.md` — a running log of structural changes to the vault.

---

## 01_Papers

One note per literature source.

Paper notes serve as **navigation hubs linking insights and extracted data**.

Paper notes are created using the **Zotero Integration plugin**, which imports highlights, annotations, and metadata directly from Zotero. See `_templates/zotero_paper_notes.md` for the canonical structure.

Citation management for manuscripts is handled via the **Zotero Word plugin** outside Obsidian.

---

## 02_Insights

Atomic scientific claims extracted from literature.

Insight notes are the **primary reusable knowledge unit**.

---

## 03_Ontology

Controlled vocabulary used across the vault.

These notes define concepts such as:

- populations
    
- activities
    
- methods
    
- metrics
    
- metric domains
    
- properties
    

**Ontology nodes do not use YAML frontmatter.** All structure is expressed through body text and wikilinks. This keeps creation overhead low.

All ontology node templates include a **Referenced In** section at the bottom — a live DataviewJS query that automatically lists every paper and insight note that links to this node. This makes each ontology note a knowledge hub: definition + literature coverage + derived insights, all in one place. No manual maintenance required.

**Exception:** Property nodes (`02_Insights/` YAML uses `property:` as plain text, not a wikilink) do not include a Referenced In query as it would return no results.

All ontology templates use `# <% tp.file.title %>` as the heading line. When a note is created via **Templater: Create new note from template**, this is replaced with the filename automatically. Do not manually type the title into the heading — the filename is the title.

---

## 04_Reference_Data

Structured numerical results extracted from papers.

These support insights with **quantitative evidence**.

---

## 05_Projects

Notes linking literature knowledge to active research projects.

---

## 06_Manuscripts

Working notes used when assembling papers or reports.

---

## _setup_files

Vault documentation and configuration reference files.

Contains this architecture document, design notes, and exported Zotero library files.

---

## _templates

Templates used when creating standardized notes.

| Template | Purpose | Auto-moves to |
|---|---|---|
| `zotero_paper_notes.md` | Canonical paper note template; used by Zotero Integration plugin | `01_Papers/` |
| `insight_note.md` | Insight note with YAML frontmatter | `02_Insights/` |
| `reference_data.md` | Reference data tables (reliability, agreement, group comparison) | `04_Reference_Data/` |
| `ontology_population.md` | Population ontology node | `03_Ontology/populations/` |
| `ontology_activity.md` | Activity ontology node | `03_Ontology/activities/` |
| `ontology_method.md` | Measurement method ontology node | `03_Ontology/methods/` |
| `ontology_statistic.md` | Statistical method ontology node | `03_Ontology/methods/` |
| `ontology_metric.md` | Metric ontology node with equation and interpretation fields | `03_Ontology/metrics/` |
| `ontology_metric_domain.md` | Metric domain ontology node | `03_Ontology/metric_domains/` |
| `ontology_property.md` | Property ontology node | `03_Ontology/properties/` |
| `ontology_clinical_measure.md` | Clinical measure, scale, or performance test | `03_Ontology/Clinical Measure/` |
| `project_note.md` | Active research project with linked insights and papers | `05_Projects/` |

---

# Knowledge Model

Knowledge in the vault is structured around the conceptual relationship:

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

Ontology nodes define the conceptual vocabulary used across the vault.

Ontology nodes use body text and wikilinks only — no YAML frontmatter.

## Populations

Examples:

- Multiple Sclerosis
    
- Parkinson's Disease
    
- Healthy Adults
    
- CIDP
    

Note: Clinical conditions that are not populations per se (e.g. Foot Drop) may also be housed in `populations/` when they function as a study group label in the literature.

---

## Activities

Examples:

- Straight-line Walking
- Turning
- Dual-task Walking
- Stairs Up
- Stairs Down
- Free-living Walking

Note: Performance tests that involve walking (e.g. TUG, 10MWT, 6MWT) are housed in `Clinical Measure/` rather than `activities/`, because they are standardised clinical tools with defined scoring and interpretation rather than pure movement tasks.

---

## Methods

Examples:

- Instrumented Insoles
- IMU
- Motion Capture
- Force Plates
- Activity Recognition

Note: Statistical methods (ICC, Bland-Altman, Pearson Correlation, etc.) are also housed in `methods/` and use `ontology_statistic.md` as their template.

---

## Clinical Measures

Examples:

- Hoehn and Yahr
- EDSS
- TUG
- 10MWT
- Stroop Word Test
- UPDRS

Clinical measures include disease severity scales, standardised performance tests, cognitive assessments, and patient-reported outcomes. They are housed in `03_Ontology/Clinical Measure/` and use the `ontology_clinical_measure.md` template.

The template includes: Purpose, Administration (clinician-administered / self-report / performance-based), Score range, Interpretation, optional Equation, MDC, MCID, Relevant populations, and Referenced In query.

Note: Clinical measures referenced inside the `Population:` section of a paper note (e.g. `[[Hoehn and Yahr]] stage ≤ 2`) may be typed as "Population" by the Processing Queue's unresolved link detector. Correct manually using the Type column.

---

# Metric Domains

Metric domains organize gait metrics into clinically meaningful categories.

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

Example relationships:

Stride Time → Rhythm  
Stride Length → Pace  
Stride Velocity → Pace  
Stride Time Variability → Variability  
Stride Time Asymmetry → Asymmetry  
Double Support Time → Postural Control

Domains provide a conceptual grouping of metrics and allow queries such as:

- all variability findings in MS
    
- all pace-related metrics studied in Parkinson's disease
    

---

# Metrics

Examples:

- Stride Time
    
- Stride Length
    
- Stride Velocity
    
- Cadence
    
- Double Support Time
    

Metrics should link to their domain.

Obsidian has **built-in math rendering** (KaTeX). Use `$$...$$` for block equations and `$...$` for inline. No plugin required.

Example metric note:

# Stride Time

Type: Metric

Definition:
Time between [[Foot Strikes]] of the same foot.

Equation:
$$
\text{Stride Time} = t_{\text{heel strike}_2} - t_{\text{heel strike}_1}
$$

Domain: [[Rhythm]]

Unit: seconds (s)

---

# Properties

Properties describe the **type of relationship being studied**.

Examples:

- Reliability
    
- Validation
    
- Variability
    
- Sensitivity
    
- Detection
    
- Clinical Association
    

---

# Use of Properties (Frontmatter)

Properties should be used **sparingly and intentionally**.

The purpose of properties is to enable **knowledge queries**, not to recreate Zotero metadata.

---

# Paper Note Properties

Paper notes require only minimal metadata. The **Zotero Integration plugin** auto-fills `citekey` and `year` from Zotero when creating a note.

Example frontmatter:

---  
type: paper  
citekey: smithValidationInsoles2024  
year: 2024  
status: unread  
---

`status` is optional and may be: `unread` / `reading` / `processed`

All conceptual information should appear **inside the note body as links**.

Example:

Population:  
[[Multiple Sclerosis]]  
  
Activity:  
[[Straight-line Walking]]  
  
Method:  
[[Instrumented Insoles]]

This prevents duplication with Zotero.

---

# Insight Note Properties

Insight notes represent relationships between concepts and therefore benefit from structured properties.

Recommended structure:

---  
type: insight  
population: Parkinsons Disease  
activity: Straight-line walking  
metric: Stride Time  
domain: Rhythm  
property: Sensitivity  
method: IMU  
citekey: authorYearKeyword  
---

**All YAML values must be plain text — no wikilinks `[[...]]`.** Dataview reads YAML as raw strings; wikilinks in YAML break all Insight Explorer and Processing Queue queries.

Valid `domain` values: `Pace` / `Rhythm` / `Variability` / `Asymmetry` / `Postural Control`  
Valid `property` values: `Reliability` / `Validation` / `Clinical Association` / `Sensitivity` / `Detection` / `Variability`

These properties allow insights to be queried using:

- Obsidian Bases
    
- Dataview
    
- graph exploration
    

---

# Paper Notes (01_Papers)

Paper notes act as **navigation hubs**, not full summaries.

Below is the structure produced by the Zotero Integration template. Imported sections are filled automatically from highlight colors; manually filled fields are noted inline.

---
type: paper
citekey: smithValidationInsoles2024
year: 2024
status: unread
---

## Study Context
%% begin study-context %%
Population:                          (fill manually)
- [[Healthy Adults]] (N=20)
- [[Multiple Sclerosis]] (N=18)

Sample Size:                         (fill manually)
- Healthy: 20, PwMS: 18

Activity:                            (fill manually)
- [[Straight-line Walking]] (10MWT, comfortable speed)

Methods:                             (fill manually)
- [[Instrumented Insoles]]
- [[Motion Capture]]

Statistics:                          (fill manually)
- [[ICC]]
- [[Bland-Altman]]

Purpose / Hypothesis:                (auto-filled from Blue highlights)
- (p. 1) To validate insole-derived gait metrics against motion capture in healthy adults.

Participant Demographics:            (auto-filled from Purple highlights)
- (p. 2) 20 healthy adults (10M/10F), age 28 +/- 4 years.

Methods Details:                     (auto-filled from Magenta highlights)
- (p. 2) Insoles sampled at 100 Hz; motion capture at 200 Hz.
%% end study-context %%

---

## Metrics Studied
%% begin metrics-studied %%
- [[Stride Time]]                    (fill manually)
- [[Stride Length]]
- [[Stride Velocity]]
%% end metrics-studied %%

---

## Results
%% begin results %%
- (p. 4) ICC for stride velocity was 0.95 (95% CI: 0.91-0.98).   (auto-filled from Red highlights)
%% end results %%

---

## Key Insights Extracted
%% begin key-insights %%
- [[Instrumented insoles show small bias relative to motion capture]]   (wikilinks written manually)
- [[Stride velocity differs between MS and healthy adults]]

- (p. 5) Bias was <2% for all spatiotemporal metrics.   (auto-filled from Yellow highlights)
%% end key-insights %%

---

## Reference Data Extracted
%% begin reference-data %%
- [[smithValidationStudy2024 - Agreement Metrics]]   (fill manually after creating the reference data note)
%% end reference-data %%

---

## Notes
%% begin notes %%

%% end notes %%

%% Import Date: 2026-03-17T15:32:03.312-04:00 %%

---

**Study Context rules:**
- Use wikilinks and brief parenthetical clarifiers only - no full sentences
- Brief notes in parentheses are fine to disambiguate (e.g. device model, protocol variant)
- If a thought requires a verb, it belongs in an insight note, not here

**Key Insights Extracted has two zones:**
- Wikilinks to completed insight files at the top - written manually (e.g. [[Insight title here]])
- Raw Yellow highlight excerpts below - auto-filled by Zotero Integration, serve as draft material

The yellow excerpts are raw material, not finished insights. Once you create an insight file, the raw excerpt can be removed or moved to Notes.

%% begin ... %% / %% end ... %% markers are persist blocks. They protect manually edited content from being overwritten on re-import. Do not remove them.

%% Import Date: ... %% at the bottom records when the last import occurred. Expected and should not be removed.
# Insight Notes (02_Insights)

Insight notes capture **one reusable scientific claim**.

Example structure:

---  
type: insight  
population: Multiple Sclerosis  
activity: Straight-line Walking  
metric: Stride Velocity  
domain: Pace  
property: Clinical Association  
method: IMU  
citekey: smithValidationInsoles2024  
---  
  
Stride velocity is reduced in people with MS relative to healthy adults and correlates with EDSS.  
  
Evidence:  
Brief explanation of the finding.  
  
Reference Data:  
Links to supporting numerical tables if applicable.

Example title:

Stride velocity decreases with EDSS in multiple sclerosis

Insight notes are designed to be **directly reusable in manuscripts**.

---

# Reference Data Notes (04_Reference_Data)

Reference data notes store **numerical results extracted from papers**.

These usually correspond to:

- one table
    
- one dataset
    
- one group of related numerical results
    

Note naming convention:

`citekey — Description` (e.g. `smithValidationStudy2024 — Agreement Metrics`)

The baseline table structure is:

| Metric | Population | Group | N | Mean | SD |
|--------|------------|-------|---|------|----|
| [[Stride Time]] | [[Healthy Adults]] | | | | |

**Column structure will vary by study.** Adapt columns to match the paper's reported values (e.g. replace SD with SEM, LoA, ICC, etc.). The `Metric` and `Population` columns should always use wikilinks to ontology nodes — this enables retrieval via backlinks.

Example (agreement study):

Source: [[smithValidationStudy2024]]  
Citation: @smithValidationStudy2024  
  
| Metric | Population | Mean | Bias | LoA Upper | LoA Lower |  
|------|------|------|------|------|------|  
| [[Stride Time]] | [[Healthy Adults]] | 1.151 | -0.016 | 0.021 | -0.053 |  
| [[Stride Time]] | [[Multiple Sclerosis]] | 1.375 | -0.019 | 0.034 | -0.072 |

---

# Query Strategy

The system relies on **link-based querying** rather than rigid databases.

**Ontology backlink query:**

Search: Stride Time  
↓  
Open Stride Time ontology page  
↓  
View `## Referenced In` section (live query)  
↓  
See all papers and insights mentioning this metric

**Insight retrieval for manuscript writing:**

Open `00_Inbox/Insight Explorer.md`  
↓  
Filter by population, metric, domain, property, or method  
↓  
Click insight links to open full notes  
↓  
Copy claim sentences directly into manuscript draft

This approach scales naturally as the vault grows.

---

# Sub-population Handling

The vault uses **broad population nodes** as the canonical ontology unit. Sub-population specificity is encoded in three other places without creating extra nodes:

1. **Insight title** — `[[Heel pressure variability is elevated in early Parkinson's disease]]` — the qualifier is in the sentence
2. **Insight YAML `population:` field** — plain text, e.g. `population: Early Stage Parkinsons Disease` — searchable via Dataview
3. **Paper note Study Context** — qualifier in parentheses next to the broad wikilink, e.g. `[[Parkinsons Disease]] — Early Stage (H&Y ≤ 2)`

**Rule for creating a sub-population node:**
Create a dedicated node when you have **3 or more insights** that share the same specific sub-population qualifier. Until that threshold is reached, use the broad node for wikilinks and record specificity as text.

**Established sub-population nodes:**

| Node | Parent | Rationale |
|---|---|---|
| `Healthy Older Adults` | `Healthy Adults` | Genuinely different normative gait values; appears frequently as an age-matched control group |

**Do not pre-create** nodes for sub-populations you have not yet encountered in the literature. Add them when the threshold is reached.

---

# Minimal Workflow for Processing a Paper

## Phase 1 — In Zotero (while reading)

1. Read the PDF in Zotero.
    
2. Highlight text using the color scheme below. Add Zotero comments on Yellow highlights to pre-draft insight framing in plain language — this carries directly into the note.

**Zotero Highlight Color Scheme:**

| Color | Meaning | Maps to section |
|---|---|---|
| Blue | Purpose and hypothesis | Purpose / Hypothesis |
| Purple | Participant demographics | Participant Demographics |
| Magenta | Methods, stats, equipment, metrics | Methods Details |
| Red | Results | Results |
| Yellow | Insightful text, intro/discussion arguments | Key Insights Extracted |

The template routes highlights into the correct section by color automatically.

---

## Phase 2 — Import into Obsidian

3. Run the **Zotero Integration import** command on the Zotero item.
    
    This auto-populates: Purpose / Hypothesis, Participant Demographics, Methods Details, Results, and Key Insights raw highlights.
    

4. Manually fill in the remaining Study Context fields (short wikilink lists only, no prose):
    - Population
    - Sample Size
    - Activity
    - Methods (device names and systems)
    - Statistics
    - Metrics Studied
    
5. Update `status:` from `unread` to `reading`. (`reading` = imported and reviewed, insight files not yet created in `02_Insights/`. `processed` = all insight files created.)
    

Typical time for steps 3–5: **5–10 minutes**.

---

## Phase 3 — Extract knowledge (can be deferred)

6. In `Key Insights Extracted`: name each insight worth extracting as a wikilink (sentence-form title, e.g. `[[Heel pressure variability is elevated in early Parkinson's disease]]`). This naming is the hard cognitive work — do it while the paper is fresh.

7. Create **reference data notes** in `04_Reference_Data` if the paper contains numerical values worth citing later. Link the note in the `Reference Data Extracted` section of the paper note.

8. Create the actual **insight note files** in `02_Insights`. This step can be deferred or batched. The yellow highlights in `Key Insights Extracted` serve as the body-text draft. Fill the YAML frontmatter and write one sentence body.

9. Link insights and reference data to ontology nodes in `03_Ontology`.
    

**Time-minimization rule:** Do not create insight files at reading time. Name them in the paper note (step 6) and create the files in one of two ways:
- **On demand:** when writing a manuscript and needing to cite this insight, create the file at that moment
- **Batch session:** periodically open the Processing Queue (see below) and work through all `status: reading` papers

**How deferred insights stay findable:**

Obsidian surfaces unresolved wikilinks automatically. Every insight name you wrote in step 6 without a corresponding file appears as an unresolved link in:
- The **Outgoing Links panel** of that paper note (right sidebar)
- The **graph view** as an orphaned node (a dot with no connected note)

You do not need to remember which papers have pending insights. The paper note carries that information, and the `status: reading` field makes it queryable.

**Processing Queue** — `00_Inbox/Processing Queue.md` contains three live Dataview queries:

1. **Papers pending insight extraction** — all `status: reading` paper notes
2. **Unresolved ontology references** — short wikilinks (< 7 words) used in paper or insight notes that have no corresponding file yet; these are likely populations, activities, methods, metrics, or statistics nodes that need to be created in `03_Ontology/`; the table shows which note(s) referenced each missing item
3. **All papers by status** — full overview of the pipeline

The unresolved ontology query uses a word-count heuristic to separate ontology-type links (short noun phrases) from insight-type links (sentence-form titles). The threshold is 7 words.

To use the Processing Queue:

- Papers in the first table are ready for insight extraction — open each one and use the **Outgoing Links panel** (right sidebar) to see which insight wikilinks are still unresolved
- Missing ontology items in the second table can be created via **Templater: Create new note from template** — choose the template matching the Type column; the file will auto-move to the correct ontology subfolder
- Set `status: processed` on a paper note when all its insight files have been created

---

## Updating a Note After New Highlights

1. Add new highlights or Zotero notes to the item in Zotero.
    
2. Return to Obsidian and run the Zotero Integration import command again on the same item.
    
3. The import will update the imported content while preserving your manually edited sections (protected by `%% begin ... %%` / `%% end ... %%` persist markers).
    

**Caution:** Once a persisted block contains content you have manually edited, it will not be overwritten — even if it was messy to begin with. If the block is significantly wrong, edit it directly in Obsidian rather than expecting a re-import to fix it. When testing a heavily revised template, test on a fresh paper rather than a previously imported one.

---

# Manuscript Writing Workflow

The vault is designed so that manuscripts can be assembled from existing notes rather than written from scratch.

## Introduction / Discussion
1. Open `00_Inbox/Insight Explorer.md`
2. Filter by the relevant population, domain, or property
3. Open each insight note — the claim sentence is manuscript-ready prose
4. Cross-reference the paper note for context (Methods Details, Purpose/Hypothesis)

## Methods Section
1. Open the relevant ontology method nodes (e.g. `[[IMU]]`, `[[Bland-Altman]]`)
2. `## Referenced In` shows which papers used this method — use these as citations
3. Paper note `Methods Details` section contains the verbatim method descriptions from papers

## Results Section
1. Reference data notes contain structured numerical tables ready to adapt into manuscript tables
2. Use `00_Inbox/Insight Explorer.md` filtered by `property = "Validation"` or `"Reliability"` to find the relevant claims

## Building a Reference List
Use the Insight Explorer to find all insights on a topic, note their `citekey` fields, then retrieve the full citation from Zotero.

---

# Collaboration Rules

1. The vault is **shared research infrastructure**.
    
2. Prefer linking existing ontology nodes rather than creating new ones.
    
3. Insight notes should remain short and reusable.
    
4. Reference data notes should capture only **numbers likely to be cited later**.
    
5. Avoid long narrative summaries of papers.
    

---

# Conceptual Model of the Vault

Knowledge flows through three layers:

Paper → Insight → Reference Data

Paper notes provide context.

Insight notes capture reusable scientific claims.

Reference data notes capture supporting numerical evidence.

Ontology nodes provide the conceptual framework connecting everything.
