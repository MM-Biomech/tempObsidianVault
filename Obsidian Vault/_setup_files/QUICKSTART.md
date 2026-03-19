# Vault Quickstart

Welcome. This guide gets you from zero to processing your first paper in one session.
For full architectural detail, see `Lab Vault System Architecture.md`.

---

## Step 1 — Required Software

Install these first:

| Software             | Purpose                                                    | Where to get it                                                                |
| -------------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------ |
| **Obsidian**         | The note-taking application that runs this vault           | [Download - Obsidian](https://obsidian.md/download)                            |
| **Zotero**           | Reference manager — stores PDFs, metadata, and annotations | [Zotero \| Your personal research assistant](https://www.zotero.org/download/) |
| **Zotero Connector** | Browser extension — saves papers to Zotero with one click  | [Zotero \| Your personal research assistant](https://www.zotero.org/download/) |

---

## Step 2 — Clone Git Repo

1. Open Obsidian
2. Click **Open folder as vault**
3. Navigate to and select the `Obsidian Vault/` folder in this project directory
4. Obsidian will load the vault

## Step 2 — Open the Vault in Obsidian

5. Open Obsidian
6. Click **Open folder as vault**
7. Navigate to and select the `Obsidian Vault/` folder in this project directory
8. Obsidian will load the vault

---

## Step 3 — Install Required Plugins

All plugins below are **Community Plugins** and must be individually installed inside Obsidian.

Go to: **Settings → Community Plugins → Browse**

Install and enable each of the following:

| Plugin | Why you need it |
|---|---|
| **Dataview** | Powers all live query tables (Processing Queue, Insight Explorer, Referenced In sections) |
| **Templater** | Creates notes from templates with auto-move to correct folder |
| **Zotero Integration** | Imports highlights and annotations from Zotero into paper notes |
| **Citations** | Manages `.bib` file and citekey resolution for pandoc citations |

> **Important:** After installing, also **enable** each plugin with the toggle on the same screen. Dataview tables will show as empty until the plugin is active.

---

## Step 4 — Configure Zotero Integration

1. In Obsidian: **Settings → Zotero Integration**
2. Set the **Note Import Location** to `01_Papers/`
3. Under **Import Formats**, add an entry and point it to `_templates/zotero_paper_notes.md`
4. Test: open the Command Palette (`Ctrl+P`), search "Zotero Integration: Import", select a Zotero item — a paper note should appear in `01_Papers/`

---

## Step 5 — Configure Templater

1. In Obsidian: **Settings → Templater**
2. Set **Template folder location** to `_templates`
3. Enable **Trigger Templater on new file creation** (optional but helpful)
4. Folder templates can be set so that new files in specific folders auto-apply their template — see `Lab Vault System Architecture.md` for details

---

## Step 6 — Process Your First Paper

This is the complete first-paper walkthrough. Expected time: **15–25 minutes** for a new paper you have already read.

### In Zotero (while reading the PDF)

Use the built-in Zotero PDF reader. Highlight text using these colors:

| Color | What to highlight |
|---|---|
| Blue | The paper's purpose and hypothesis |
| Purple | Participant demographics |
| Magenta | Methods, equipment, statistics |
| Red | Key results |
| Yellow | Insightful statements worth extracting as claims |

> **Tip for Yellow highlights:** After highlighting, add a **Zotero comment** (right-click the highlight → Add comment) with your own framing of the insight in plain language. This comment imports directly into the note and saves you rewriting it later.

### Import into Obsidian

1. In Obsidian, open the Command Palette (`Ctrl+P`)
2. Run **Zotero Integration: Import notes** (exact name depends on your setup)
3. Search for and select your paper — a note is created in `01_Papers/`

### Fill in Study Context fields

Open the new note. You will see sections already filled from your highlights (Purpose, Demographics, Methods Details, Results, Key Insights). Manually fill in the remaining structured fields:

- **Population** — `[[Parkinsons Disease]]` (use wikilinks to ontology nodes)
- **Sample Size** — plain text is fine: `N=24 (12 PD, 12 controls)`
- **Activity** — `[[Straight-line walking]]`
- **Methods** — `[[IMU]]`, `[[Bland-Altman]]`
- **Statistics** — `[[ICC]]`
- **Metrics Studied** — `[[Stride Time]]`, `[[Cadence]]`

> **Rule:** Use short wikilinks only — no full sentences in Study Context. If a thought requires a verb, it belongs in an insight note.

Change `status: unread` to `status: reading` in the YAML frontmatter.

**That's the minimum.** The note is now in the system. Estimated time: **5–10 minutes**.

### Name your insights (while the paper is fresh)

In the **Key Insights Extracted** section, write sentence-form wikilinks for claims worth keeping:

```
- [[Stride velocity is reduced in early Parkinson's disease during straight-line walking]]
- [[IMU-derived cadence shows high ICC in Parkinson's disease]]
```

These files do not need to exist yet. Obsidian tracks them as unresolved links. You create the actual files later.

### Create ontology nodes for missing concepts

After filling Study Context, some wikilinks you wrote will be unresolved (shown in orange or dashed in Obsidian). If `[[Cadence]]` doesn't have a note yet, create it:

1. Open Command Palette → **Templater: Create new note from template**
2. Choose `ontology_metric.md`
3. Name it `Cadence`
4. The file is automatically created and moved to `03_Ontology/metrics/`
5. Fill in the Definition, Equation, Domain, Unit fields

> **Check the Processing Queue** (`00_Inbox/Processing Queue.md`) to see all missing ontology links across all notes — you don't need to hunt for them manually.

---

## Step 7 — Know the Key Navigation Points

| File | What it does |
|---|---|
| `00_Inbox/Processing Queue.md` | Shows papers pending insight extraction and missing ontology nodes |
| `00_Inbox/Insight Explorer.md` | Filter all insights by population, metric, method, or paper |
| `03_Ontology/ontology_map.md` | Live index of all defined ontology nodes by category |

---

## Step 8 — Creating an Insight Note

When you're ready to formalize an insight (either immediately or in a batch session later):

1. Click the unresolved wikilink in the paper note (e.g. `[[Stride velocity is reduced in early Parkinson's disease]]`)
2. Obsidian creates a blank file — apply the insight template via Command Palette → **Templater: Create new note from template** → `insight_note.md`
3. The file auto-moves to `02_Insights/`
4. Fill the YAML frontmatter fields (population, metric, domain, property, method, citekey)
5. Write one sentence below the frontmatter — this is the claim, written to be paste-able directly into a manuscript

Example of a finished insight note:

```yaml
---
type: insight
population: Parkinsons Disease
activity: Straight-line walking
metric: Stride Velocity
domain: Pace
property: Clinical Association
method: IMU
citekey: smithValidationInsoles2024
---
```

```
Stride velocity is reduced in people with early-stage Parkinson's disease 
relative to age-matched healthy controls during self-paced straight-line walking.

Evidence:
Group difference was statistically significant (p < 0.01); effect size d = 0.82.

Reference Data:
- [[smithValidationInsoles2024 — Spatiotemporal Agreement]]
```

---

## Common Questions

**Q: The Dataview tables are empty.**
A: The Dataview plugin must be installed and enabled in Community Plugins. See Step 3.

**Q: I created a note from a template but it stayed in the root folder.**
A: Make sure Templater is installed and enabled, and that you used **Templater: Create new note from template** from the Command Palette rather than clicking an unresolved link. The auto-move only runs when Templater processes the template.

**Q: A wikilink I typed is showing up in the Processing Queue as a missing ontology node.**
A: That's expected and correct. Create the ontology note for it using the matching template. If it's an insight title (long sentence), it will not appear in the queue — the query filters those out by word count.

**Q: When should I create a new ontology node vs. just writing text?**
A: Create a node if you expect to reference this concept from 2+ papers. For one-off qualifiers (e.g. "moderate disease severity"), use plain text parentheticals in Study Context instead.

**Q: I want to search all insights about a particular metric.**
A: Open `00_Inbox/Insight Explorer.md` and edit the WHERE clause in the "Filter by Metric" query.
