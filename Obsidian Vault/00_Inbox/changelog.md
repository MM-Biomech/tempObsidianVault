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
