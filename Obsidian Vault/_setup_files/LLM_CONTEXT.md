# LLM Context — Lab Research Vault

This file provides structured context for AI assistants (e.g. Cursor, Claude, GPT) operating on this vault.
Read this file before helping with any vault task.

---

## Research Domain

This is a **biomechanics and rehabilitation engineering lab** focused on:

- **Wearable sensor-based gait analysis** — primarily using inertial measurement units (IMUs) and instrumented insoles with logical and machine learning algorithms
- **Neurological populations** — Parkinson's disease, Multiple Sclerosis (MS), Chronic Inflammatory Demyelinating Polyneuropathy (CIDP), Foot Drop
- **Validation and clinical translation** — establishing whether wearable-derived gait metrics agree with lab-grade reference systems (e.g. motion capture, force plates) and correlate with clinical outcomes
- **Method development** — algorithms for gait event detection, spatiotemporal parameter estimation, ambulatory monitoring

Key vocabulary:
- **Spatiotemporal gait parameters** — stride time, stride length, stride velocity, cadence, double support time, stance time, swing time
- **Gait domains** — Pace, Rhythm, Variability, Asymmetry, Postural Control (standard clinical framework)
- **Common clinical scales** — EDSS (MS severity), Hoehn and Yahr (PD severity), UPDRS (PD motor function), TUG (Timed Up and Go), MCID (minimum clinically important difference), MDC (minimal detectable change)
- **Common statistics** — ICC (intraclass correlation coefficient), Bland-Altman (method agreement), Pearson correlation, SEM (standard error of measurement)



---

## Vault Purpose

The vault is a **long-term research knowledge system** that accumulates insights across papers, projects, and researchers.

It is NOT a simple literature note repository. Its design separates three distinct knowledge layers:

1. **Paper notes** — context and navigation hubs (what did this paper study, what did it find)
2. **Insight notes** — atomic, reusable scientific claims (directly citable in manuscripts)
3. **Reference data notes** — structured numerical results (tables of means, SD, ICC, LoA, etc.)

These are linked through a shared **ontology** (controlled vocabulary) of populations, activities, methods, metrics, metric domains, properties, and clinical measures.

---

## Folder Structure

```
00_Inbox/           Temporary + dashboards (Processing Queue, Insight Explorer, changelog)
01_Papers/          One note per paper; created by Zotero Integration plugin
02_Insights/        Atomic scientific claims; one sentence claim + YAML frontmatter
03_Ontology/        Controlled vocabulary nodes
    populations/    e.g. Parkinsons Disease, Multiple Sclerosis, Healthy Adults
    activities/     e.g. Straight-line walking, Turning, Dual-task Walking
    methods/        e.g. IMU, Instrumented Insoles, Motion Capture + statistical methods
    metrics/        e.g. Stride Time, Cadence, Foot Pitch Angle
    metric_domains/ Pace, Rhythm, Variability, Asymmetry, Postural Control
    properties/     Reliability, Validation, Sensitivity, Detection, Clinical Association, Variability
    Clinical Measure/ e.g. TUG, Hoehn and Yahr, EDSS, Stroop Word Test
04_Reference_Data/  Numerical results tables extracted from papers
05_Projects/        Active research project notes linking literature to project goals
06_Manuscripts/     Working notes during manuscript writing
_setup_files/       This file, QUICKSTART.md, Lab Vault System Architecture.md
_templates/         Templater/Nunjucks templates for each note type
```

---

## Note Type Specifications

### Paper Note (`01_Papers/`)
**Created by:** Zotero Integration plugin using `_templates/zotero_paper_notes.md`  
**YAML frontmatter:**
```yaml
type: paper
citekey: authorYearKeyword
year: 2024
status: unread | reading | processed
```
**Body sections (auto-filled from Zotero highlights by color):**
- `## Study Context` — Population, Sample Size, Activity, Methods, Statistics (manual wikilinks) + Purpose/Hypothesis (Blue), Participant Demographics (Purple), Methods Details (Magenta) — all wrapped in `%% begin study-context %% / %% end study-context %%` persist blocks
- `## Metrics Studied` — wikilinks to metric nodes (manual)
- `## Results` — auto-filled from Red highlights
- `## Key Insights Extracted` — sentence-form wikilinks to insight files (manual) + Yellow highlight excerpts (auto)
- `## Reference Data Extracted` — links to reference data notes (manual)
- `## Notes` — free text

**Persist blocks** (`%% begin name %% / %% end name %%`) protect manually edited sections from being overwritten on Zotero re-import.

---

### Insight Note (`02_Insights/`)
**Created by:** Templater using `_templates/insight_note.md`  
**YAML frontmatter:**
```yaml
type: insight
population: Parkinsons Disease       # plain text — NO wikilinks [[...]] in YAML
activity: Straight-line walking      # plain text
metric: Stride Velocity              # plain text
domain: Pace                         # Pace | Rhythm | Variability | Asymmetry | Postural Control
property: Clinical Association       # Reliability | Validation | Clinical Association | Sensitivity | Detection | Variability
method: IMU                          # plain text (optional)
citekey: authorYearKeyword           # plain text
```

**Critical rule: all YAML values are plain text.** Wikilinks (`[[...]]`) in YAML fields break all Dataview queries — the Insight Explorer and Processing Queue will silently return no results for that note.
**Body:** One sentence claim (manuscript-ready) + Evidence paragraph + optional Reference Data links

**Naming convention:** Sentence-form title describing the finding, e.g.:
`Stride velocity is reduced in early Parkinson's disease relative to healthy older adults`

---

### Ontology Node (`03_Ontology/*/`)
**Created by:** Templater using type-specific template  
**No YAML frontmatter** — structure expressed in body text and wikilinks only  
**Always includes** at the bottom:
- `## Referenced In` — DataviewJS query listing all papers (with outgoing link to this node) and all insights (with outgoing link OR YAML field matching this node's filename)

**Sub-population rule:** Only create a specific sub-population node when 3+ insights share that qualifier. Until then, use the broad parent node for wikilinks and encode specificity as:
1. Insight title text
2. YAML `population:` plain text value
3. Parenthetical in paper note Study Context

---

### Reference Data Note (`04_Reference_Data/`)
**Naming:** `citekey — Description` (e.g. `kim2026InsoleDerivedPlantar — Smart Insole Validation`)  
**Structure:** `Source: [[citekey]]`, `Citation: @citekey`, then a markdown table  
**Always use wikilinks** in Metric and Population columns to enable backlink retrieval

---

## Plugin Architecture

### Zotero plugins (installed in Zotero, not Obsidian)

| Plugin | Role |
|---|---|
| **Better BibTeX** | Generates stable citekeys (e.g. `kim2026InsoleDerivedPlantar`); exposes a local JSON-RPC API that Zotero Integration uses to connect to Zotero |
| **Zotero Word Plugin** | Inserts citations into Word manuscripts from the Zotero library; not used within Obsidian |

### Obsidian plugins (pre-installed in this repository)

| Plugin | Role |
|---|---|
| **Zotero Integration** | Imports paper notes from Zotero using Nunjucks template; routes highlights by colour into correct sections |
| **Dataview** | Powers all live query tables (Processing Queue, Insight Explorer, Referenced In) |
| **Templater** | Note creation from templates with `tp.file.move()` auto-routing to correct folder |
| **Table Editor** | Markdown table formatting convenience |

### What is NOT in Obsidian

- Citation management is handled by the Zotero Word plugin in Word
- There is no `.bib` file in this repository — it is not needed
- PDFs are stored and synced through Zotero, not Git

---

## Key Dashboard Files

| File | Purpose |
|---|---|
| `00_Inbox/Processing Queue.md` | Papers with `status: reading` + unresolved ontology wikilinks (missing nodes) |
| `00_Inbox/Insight Explorer.md` | Query insights by population, metric, domain, property, method, or citekey |
| `03_Ontology/ontology_map.md` | Live index of all ontology nodes by category |
| `00_Inbox/changelog.md` | Running log of structural changes to the vault |

---

## Conventions and Rules

**Wikilink naming:** Always match the exact filename of the ontology node. Ontology node filenames are the canonical name (e.g. `Parkinsons Disease`, not `Parkinson's Disease` — check the actual file).

**Insight YAML fields:** All plain text (no wikilinks). Values should match ontology node filenames so Dataview can filter by them. The `Referenced In` query in each ontology node now also checks YAML fields, so even if there's no body wikilink, the insight will appear.

**No YAML on ontology nodes.** Structure is expressed through body text only. Queries work via outgoing links and insight YAML, not via ontology node frontmatter.

**Status lifecycle for papers:**
- `unread` → paper is in Zotero but not yet imported to Obsidian
- `reading` → imported, Study Context filled, but insight files not yet created
- `processed` → all insight files created

**Word count heuristic in Processing Queue:** Links with fewer than 7 words are treated as ontology-type nodes (to be created in `03_Ontology/`). Links with 7+ words are treated as insight titles. This separates short concept names from sentence-form claims.

**Highlight color scheme (Zotero → Obsidian):**

| Color | Meaning | Destination section |
|---|---|---|
| Blue | Purpose / hypothesis | Purpose / Hypothesis |
| Purple | Participant demographics | Participant Demographics |
| Magenta | Methods, stats, equipment | Methods Details |
| Red | Results | Results |
| Yellow | Insightful claims, intro/discussion arguments | Key Insights Extracted |

---

## What an AI Assistant Should Help With

- Creating or editing ontology nodes, insight notes, reference data notes — following the templates exactly
- Writing DataviewJS or Dataview queries using the correct folder paths and frontmatter field names
- Editing `zotero_paper_notes.md` (Nunjucks template) — use `annotation.colorCategory` to route highlights; use `{%-` / `-%}` for whitespace control in loops; use normal `%%` (not trimmed) for persist block markers
- Updating `Lab Vault System Architecture.md` and `changelog.md` when structural changes are made
- Suggesting ontology nodes to create based on paper Study Context content
- Helping write manuscript sections by retrieving and organizing insight claims

---

## What an AI Assistant Should NOT Do

- Duplicate Zotero metadata (authors, journal, abstract, keywords) inside Obsidian note bodies
- Create YAML frontmatter on ontology nodes
- Create long narrative summaries of papers — paper notes are navigation hubs, not summaries
- Pre-create ontology sub-population nodes before the 3-insight threshold is reached
- Remove or modify `%% begin ... %% / %% end ... %%` persist blocks in paper notes
