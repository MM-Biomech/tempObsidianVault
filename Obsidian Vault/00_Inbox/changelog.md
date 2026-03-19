# Vault Changelog

---

## 2026-03-11 — Initial Vault Structure Review

### Added

- `03_Ontology/metric_domains/` folder with five domain notes: Pace, Rhythm, Variability, Asymmetry, Postural Control
- `03_Ontology/properties/` populated with six property notes: Reliability, Validation, Variability, Sensitivity, Detection, Clinical Association
- `_templates/paper_note.md` — canonical paper note structure using `{{citekey}}` and `{{year}}` variables to mirror the Citations plugin template
- `_templates/ontology_population.md`
- `_templates/ontology_activity.md`
- `_templates/ontology_method.md`
- `_templates/ontology_metric.md` — includes Equation field using built-in KaTeX math rendering
- `_templates/ontology_metric_domain.md`
- `_templates/ontology_property.md`

### Updated

- `_templates/insight_note.md` — added missing `domain:` field to frontmatter
- `_templates/reference_data.md` — added baseline table structure with note about adapting columns per study
- `03_Ontology/metrics/Stride Time.md` — updated to match metric template; added Definition, Equation, Domain, Unit
- `02_Insights/Impaired Dorsiflexion in Foot Drop.md` — added YAML frontmatter block; added title heading and claim statement
- `_setup_files/Lab Vault System Architecture.md` — updated to reflect all structural decisions made during initial review

### Moved

- `Design insights.md` → `_setup_files/Design insights.md`

### Deleted

- `01_Papers/.md` — blank file created by a failed template instantiation

### Decisions Recorded

- Ontology nodes do **not** use YAML frontmatter (overhead not justified; links serve the same purpose)
- Paper note frontmatter contains only `type`, `citekey`, `year`, `status` — bibliographic metadata stays in Zotero
- Citations plugin template is configured inline in plugin settings; `_templates/paper_note.md` mirrors it and must be kept in sync manually
- `Foot Drop` remains in `03_Ontology/populations/` despite being a clinical condition rather than a population — it functions as a study group label in the literature
- Obsidian has built-in KaTeX math rendering; no plugin required for equations

---

## 2026-03-11 — Paper Note Refinement (Soulard 2021 dry run)

### Added

- `03_Ontology/activities/Dual-task Walking.md` — new activity node
- `03_Ontology/metrics/Symmetry Index.md` — new metric node with SI equation, links to Asymmetry domain
- `03_Ontology/metrics/Symmetry Ratio.md` — new metric node with SR equation, links to Asymmetry domain
- `04_Reference_Data/soulard2021SpatiotemporalGait — Intra-session Reliability.md` — first reference data note; ICC, SEM, MDC for core spatiotemporal and symmetry metrics

### Updated

- `_templates/paper_note.md` — added `Statistics:` field to Study Context
- `01_Papers/soulard2021SpatiotemporalGait.md` — corrected Study Context (removed narrative prose), fixed metric links (Asymmetry → Symmetry Index + Symmetry Ratio), corrected activity links, removed citation from Notes, linked reference data note
- `_setup_files/Lab Vault System Architecture.md` — documented Study Context authoring rules; added Statistics field to paper note example

### Decisions Recorded

- Study Context uses wikilinks and brief parentheticals only — no full sentences. Sentence-level observations belong in insight notes.
- Unresolved wikilinks are acceptable temporarily; stub notes should be created promptly for any concept that will appear across multiple papers
- Asymmetry is a metric domain; Symmetry Index and Symmetry Ratio are the specific metrics that belong to it
- Statistical methods (ICC, SEM, MDC, etc.) are linked in the Statistics field and housed as ontology nodes in `03_Ontology/methods/`

---

## 2026-03-17 — Zotero Integration Workflow + Processing Queue

### Added

- `_templates/zotero_paper_notes.md` — canonical paper note template using Nunjucks syntax for Zotero Integration plugin; replaces `paper_note.md` as the primary template for creating paper notes
- `01_Papers/kim2026InsoleDerivedPlantar.md` — first paper note created via Zotero Integration; includes color-routed highlights and persist blocks
- `01_Papers/figures/kim2026InsoleDerivedPlantar/` — embedded figures extracted during import
- `04_Reference_Data/kim2026InsoleDerivedPlantar - Smart Insole Validation.md` — reference data note with reliability (ICC) and validation (Bland-Altman) tables for spatiotemporal metrics
- `00_Inbox/Processing Queue.md` — Dataview dashboard with three sections: papers pending insight extraction (`status: reading`), unresolved ontology references (short wikilinks with no corresponding file, sourced from paper and insight notes), and all papers by status

### Updated

- `_setup_files/Lab Vault System Architecture.md`:
  - Added Plugin Roles section: Citations handles citekeys/.bib; Zotero Integration creates paper notes
  - Added Zotero Integration: How It Works section explaining import, re-import, and persist block behavior
  - Added Zotero Highlight Color Scheme table (Blue/Purple/Magenta/Red/Yellow) with section routing
  - Replaced old minimal workflow with three-phase model: In Zotero → Import + fast fill → Deferred extraction
  - Documented Processing Queue pattern and two triggers for creating insight files (on-demand vs. batch)
  - Updated Paper Notes example to reflect actual Zotero Integration template output with persist markers and auto-filled vs. manually filled fields annotated
  - Updated templates table to list `zotero_paper_notes.md` as canonical and `citations_paper_note.md` as legacy
  - Clarified `status` semantics: `reading` = imported, insight files not yet created; `processed` = all insight files created
- `04_Reference_Data/kim2026InsoleDerivedPlantar - Smart Insole Validation.md` — fixed incomplete `Citation: @` field

### Decisions Recorded

- Citations plugin and Zotero Integration coexist with distinct roles; paper notes are now created via Zotero Integration, not Citations
- Highlight color scheme: Blue = purpose/hypothesis, Purple = demographics, Magenta = methods, Red = results, Yellow = insights
- Persist blocks (`%% begin ... %%` / `%% end ... %%`) protect manually edited sections from re-import overwrite; once edited, content is permanently preserved by subsequent imports
- Insight files in `02_Insights/` should be named at reading time as wikilinks in the paper note but created later — either on-demand when cited in a manuscript, or in a batch session using the Processing Queue
- Unresolved insight wikilinks are surfaced by Obsidian's Outgoing Links panel and graph view; no separate tracking needed
- Dataview plugin required for Processing Queue queries; must be installed from Community Plugins
- Unresolved ontology references are tracked via a DataviewJS query that scans `01_Papers/` and `02_Insights/` for short wikilinks (< 7 words) with no corresponding file; insight-style sentence links are excluded by the word-count filter

---

## 2026-03-17 — Template Overhaul

### Added

- `_templates/ontology_statistic.md` — new template for statistical methods (ICC, Bland-Altman, Pearson, ANOVA, etc.); auto-moves to `03_Ontology/methods/`

### Updated

- All ontology templates now include `tp.file.move()` to auto-place files in the correct `03_Ontology/` subfolder on creation via Templater
- `_templates/insight_note.md` — removed duplicate body fields (Population, Activity, Metric, Property, Source were repeated from YAML); streamlined body to claim + Evidence + Reference Data; removed redundant `source:` field; added auto-move to `02_Insights/`
- `_templates/reference_data.md` — added auto-move to `04_Reference_Data/`; clarified `[[citekey]]` placeholder
- `_templates/ontology_metric.md` — added `Interpretation:` field (higher/lower values)
- `_templates/ontology_activity.md` — added `Common populations studied:` field
- `_templates/ontology_method.md` — added `Key specifications:` field (sampling rate, sensor type)
- `_templates/ontology_property.md` — added `Common statistics:` field
- `_templates/ontology_metric_domain.md` — added `Clinical significance:` field
- `_templates/citations_paper_note.md` — added deprecation notice; no longer in active use
- `_setup_files/Lab Vault System Architecture.md` — updated templates table with auto-move destinations; added `ontology_statistic.md`
- `00_Inbox/Processing Queue.md` — added Type → Template → Destination lookup table in Unresolved Ontology References section; fixed type detection for `## Metrics Studied` heading (was bleeding Statistics label into Metrics section)

### Decisions Recorded

- Statistics (ICC, Bland-Altman, etc.) use `ontology_statistic.md` and live in `03_Ontology/methods/` alongside measurement methods
- All templates use `tp.file.move()` so "Create new note from template" always places files in the correct folder with no manual move required
- `insight_note.md` body contains only the claim, Evidence, and Reference Data — YAML frontmatter carries all structured metadata; body duplication removed
- All ontology templates include a `## Referenced In` DataviewJS section showing papers (with year and status) and insights that link to the node; this is partially redundant with Obsidian's native Backlinks panel but adds value by filtering to papers/insights only, showing metadata, and being visible in the note body without opening the sidebar

---

## 2026-03-17 — Clinical Measure Template

### Added

- `_templates/ontology_clinical_measure.md` — new template for clinical measures, performance tests, and severity scales (e.g. Hoehn & Yahr, EDSS, TUG, Stroop, 10MWT); fields include Purpose, Administration, Score range, Interpretation, Equation (optional), MDC, MCID, Relevant populations, and Referenced In query; auto-moves to `03_Ontology/Clinical Measure/`

### Updated

- `_setup_files/Lab Vault System Architecture.md` — added `Clinical Measure/` to folder structure and templates table
- `00_Inbox/Processing Queue.md` — added Clinical Measure row to Type → Template lookup table

### Decisions Recorded

- Clinical measures live in `03_Ontology/Clinical Measure/` (already established by existing `Stroop Word Test.md`)
- Clinical measures appearing in paper notes (e.g. `[[Hoehn and Yahr]]` inside a Population entry) may be typed as "Population" by the Processing Queue's section-detection heuristic; this is a known limitation — correct manually using the Type column
- Property files do not include a Referenced In query — properties are used as plain-text YAML frontmatter fields in insight notes, not as wikilinks, so backlink queries would return no results

---

## 2026-03-17 — Ontology File Backfill

### Updated

All existing ontology files updated to match current templates:

**Populations** (`cidp.md`, `Multiple Sclerosis.md`, `Healthy Adults.md`, `Foot Drop.md`, `Parkinsons Disease.md`):
- Added `Description:` field to all
- Renamed `Clinical scale:` → `Clinical scales:` for consistency
- Fixed list formatting (added `-` bullet style)
- Added `## Referenced In` DataviewJS query to all

**Activities** (`Straight-line walking.md`, `Dual-task Walking.md`, `Turning.md`, `Foot Strikes.md`):
- Added `Common populations studied:` field to all
- Added `Description:` where missing
- Restructured `Dual-task Walking.md` to match template (was using non-standard `Related metrics:` label; added `Common secondary tasks:` as a retained extra field)
- Updated `Foot Strikes.md` from a bare definition note to full activity template structure
- Added `## Referenced In` DataviewJS query to all

**Methods** (`IMU.md`):
- Fixed heading from `# [IMU]` to `# IMU`

**Metrics** (`Stride Time.md`, `Symmetry Index.md`, `Symmetry Ratio.md`):
- Added `Interpretation:` field to all
- Moved inline interpretation notes from `Unit:` field into `Interpretation:` for SI and SR
- Added `## Referenced In` DataviewJS query to all

**Metric Domains** (`Rhythm.md`, `Pace.md`, `Variability.md`, `Asymmetry.md`, `Postural Control.md`):
- Added `Description:` field to all
- Added `Clinical significance:` field to all
- Updated `Asymmetry.md` metrics list to include `[[Symmetry Index]]` and `[[Symmetry Ratio]]`
- Added `## Referenced In` DataviewJS query to all

**Properties** (`Reliability.md`, `Validation.md`, `Detection.md`, `Clinical Association.md`, `Sensitivity.md`, `Variability.md`):
- Added `Common statistics:` field with relevant wikilinked statistics to all
- Referenced In query omitted — properties are stored as plain-text YAML in insight notes, not as wikilinks

**Clinical Measures** (`Stroop Word Test.md`):
- Fully restructured to `ontology_clinical_measure.md` template
- Added: Purpose, Administration, Score range, Interpretation, Conditions description, Relevant populations, Referenced In query

---

## 2026-03-17 — Template Heading Convention + TUG Moved

### Updated

- All ontology templates (`ontology_population.md`, `ontology_activity.md`, `ontology_method.md`, `ontology_statistic.md`, `ontology_metric.md`, `ontology_metric_domain.md`, `ontology_property.md`, `ontology_clinical_measure.md`) — replaced static placeholder headings (e.g. `# [Metric Name]`) with `# <% tp.file.title %>` so the heading is filled automatically from the filename on note creation; no manual heading edit required
- `_setup_files/Lab Vault System Architecture.md` — added Clinical Measures section to Ontology Structure; added note clarifying TUG and similar performance tests belong in `Clinical Measure/` not `activities/`; added note on Statistical methods living in `methods/`; documented `# <% tp.file.title %>` heading convention; added Referenced In exception for property nodes

### Moved

- `03_Ontology/activities/TUG.md` → `03_Ontology/Clinical Measure/TUG.md` — TUG is a standardised clinical performance test with defined scoring; belongs in Clinical Measure rather than activities

### Decisions Recorded

- All ontology template headings use `# <% tp.file.title %>` — the heading is always derived from the filename; do not type the title manually into the heading
- Performance tests with defined clinical scoring (TUG, 10MWT, 6MWT, etc.) belong in `Clinical Measure/`, not `activities/`; activities are movement task types, clinical measures are scored instruments

---
