# Vault Quickstart

Welcome. This guide gets you from zero to processing your first paper in one session.
For full architectural detail, see `Lab Vault System Architecture.md`.

---

## Step 1 — Required Software

Install these before anything else:

| Software               | Purpose                                                                         | Where to get it                                                                            |
| ---------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| **Obsidian**           | The note-taking application that runs this vault                                | [obsidian.md](https://obsidian.md/download)                                                |
| **Zotero**             | Reference manager — stores PDFs, metadata, and annotations                      | [zotero.org](https://www.zotero.org/download/)                                             |
| **Zotero Connector**   | Browser extension — saves papers to Zotero with one click                       | Bundled with Zotero; also available from [zotero.org](https://www.zotero.org/download/)    |
| **Better BibTeX**      | Zotero plugin that generates stable citekeys and powers the Obsidian connection | [retorque.re/zotero-better-bibtex](https://retorque.re/zotero-better-bibtex/installation/) |
| **Zotero Word Plugin** | Inserts citations into Word manuscripts directly from your Zotero library       | Zotero → Tools → Install MS Word Add-in                                                    |

---

## Step 2 — Set Up Zotero

### Install Better BibTeX in Zotero

1. Download the `.xpi` file from [retorque.re/zotero-better-bibtex/installation/](https://retorque.re/zotero-better-bibtex/installation/)
2. In Zotero: **Tools → Add-ons → gear icon → Install Add-on From File** → select the `.xpi`
3. Restart Zotero when prompted

### Configure the citekey format

All lab members must use the same citekey format so that keys are consistent across the shared library.

1. In Zotero: **Edit → Better BibTeX Preferences → Citation Keys**
2. Set the **Citation key format** to:
   ```
   auth.lower + year + shorttitle(2, 2)
   ```
   This produces keys like `kim2026InsoleDerivedPlantar`.

### Join the shared Zotero group library

1. Accept the group invitation sent to your email (or ask the lab admin to invite you at [zotero.org/groups](https://www.zotero.org/groups/))
2. In Zotero: **Edit → Settings → Sync** — sign in with your zotero.org account
3. Click **Sync** (circular arrow button in the top right corner) — the shared library will appear in the left panel under **Group Libraries**

Your local Zotero will now stay in sync with the lab's shared library. PDFs and metadata sync automatically.
Note: 300 MB is free. Annual fees apply for more (USD)
- 2 GB: $20 
- 6 GB: $60
- Unlimited: $120

---

## Step 3 — Clone the Repository

Follow the instructions in the `README.md` at the root of the repository to clone it using Sourcetree (or any Git client). When cloning is complete, come back here.

---

## Step 4 — Open the Vault in Obsidian

1. Open Obsidian
2. Click **Open folder as vault**
3. Navigate into the cloned repository and select the **`Obsidian Vault`** subfolder — not the root repository folder
4. Obsidian will prompt: *"This vault contains community plugins..."* — click **Trust author and enable plugins**

That's it. All required plugins (Zotero Integration, Templater, Dataview, Table Editor) are already installed and configured in the repository. You do not need to install or configure any plugins manually.

> **If Dataview tables appear empty:** Go to Settings → Community Plugins and confirm the toggle next to Dataview is on. Sometimes Obsidian's trust prompt doesn't enable all plugins on the first launch.

---

## Step 5 — Connect Zotero Integration to Your Zotero Library

The plugin is pre-configured, but it connects to your running Zotero instance over a local port. You just need Zotero open when you import.

**Test the connection:**
1. Open Zotero (must be running)
2. In Obsidian, open the Command Palette (`Ctrl+P`)
3. Search for **Zotero Integration: Create Paper Note**
4. A search box should appear — type a paper title or author from your Zotero library
5. Select a paper — a note should appear in `01_Papers/`

If the search box appears but returns no results, check that Zotero is open and the **Better BibTeX** plugin is installed in Zotero (required for citekey generation).

---

## Step 6 — Process Your First Paper

Expected time: **15–25 minutes** for a paper you have already read.

### In Zotero (while reading)

Use the built-in Zotero PDF reader. Highlight text using these colours — the template routes each colour into the correct section of the note automatically:

| Colour | What to highlight |
|---|---|
| Blue | The paper's purpose and hypothesis |
| Purple | Participant demographics |
| Magenta | Methods, equipment, statistics |
| Red | Key results |
| Yellow | Findings from this paper that you believe and could cite in a manuscript |
| Orange | Claims cited from other papers worth chasing — highlights a paper you should find and read | Follow-up Citations |

> **Before highlighting in Yellow, ask:** can I write a one-sentence declarative claim right now? If not, do not highlight. A well-processed paper yields 3–6 Yellow highlights — not 15. See `_setup_files/Highlighting Guidelines.md` for the full discipline framework, including what to do when you disagree with a paper's claim.

> **Tip for Yellow highlights:** After highlighting, right-click → Add comment and write your own framing of the claim in plain language — the sentence you would put in a manuscript. This comment imports directly into the note and becomes the draft for your insight note title.

### Import into Obsidian

1. Make sure Zotero is open
2. In Obsidian, open the Command Palette (`Ctrl+P`)
3. Run **Zotero Integration: Create Paper Note**
4. Search for and select your paper — a note is created in `01_Papers/`

### Fill in the Study Context fields

Open the new note. Sections filled from your highlights (Purpose, Demographics, Methods Details, Results, Key Insights) are already populated. Manually fill in the remaining structured fields using short wikilinks — no prose:

- **Population** — `[[Parkinsons Disease]]`
- **Sample Size** — `N=24 (12 PD, 12 controls)`
- **Activity** — `[[Straight-line Walking]]`
- **Protocol** — `10 m corridor, 5 laps, comfortable pace, no turn instructions`
- **Devices** — `[[IMU]]` (wikilinks to hardware/software ontology nodes)
- **Statistics** — `[[ICC]]`, `[[Bland-Altman]]`
- **Metrics Studied** — `[[Stride Time]]`, `[[Cadence]]` (wikilinks to metric ontology nodes)

Change `status: unread` to `status: reading` in the YAML frontmatter at the top of the note.

**That's the minimum — estimated 5 minutes.** The paper is now in the system.

### Name your insights (while the paper is fresh)

In the **Key Insights Extracted** section, write sentence-form wikilinks **at the top of the section**, above the raw highlight text:

```
- [[Stride velocity is reduced in early Parkinson's disease during straight-line walking]]
- [[IMU-derived cadence shows high ICC in Parkinson's disease]]

- (p. 4) raw highlight text from Zotero...
- (p. 5) another raw highlight...
```

> **The wikilinks must end up at the top — not left as `Note:` comments inside the highlight block.** Writing `[[]]` links in your Zotero comment is encouraged (see tip below), but after import you must move those wikilinks up to the top of the section. A wikilink left inside a `  - Note: [[...]]` line under a raw highlight will not register in the Processing Queue as a named insight awaiting a file.

The insight files do not exist yet — that is normal and expected. Obsidian tracks unresolved wikilinks automatically. You create the actual files later (see Creating an Insight Note below).

> **Tip for Zotero comments on Yellow highlights:** Write `[[Insight title]]` directly in the Zotero comment field while reading — this is the most efficient moment to name the claim. After importing, those wikilinks will appear as `- Note: [[...]]` inside the raw highlight block. **Move them to the top of Key Insights** as a post-import step, then remove the redundant Note comment. Two quick moves per insight, and all the naming was done at read time.

### Before closing the note — completion checklist

Run through this before setting `status: reading`:

- [ ] `status:` changed from `unread` to `reading` in YAML
- [ ] All manual Study Context fields filled (Population, Sample Size, Activity, Protocol, Devices, Statistics, Metrics Studied)
- [ ] `- [[]]` placeholder removed from Key Insights, Metrics Studied, and Reference Data Extracted
- [ ] Insight wikilinks written at the **top** of Key Insights, above the raw highlights
- [ ] Metrics Studied contains only **metric** wikilinks — not domain nodes (e.g. `[[Variability]]` is a domain; `[[Stride Time]]` is a metric)
- [ ] Follow-up Citations contains only genuine paper-to-chase entries with a `Find:` comment — no background statements, no insight titles from other papers
- [ ] Each persist block that was opened (`%% begin name %%`) has a matching close tag (`%% end name %%`)

### Create ontology nodes for new concepts

After filling Study Context, some wikilinks you wrote will be unresolved (shown in a different colour). If `[[Cadence]]` doesn't have a note yet:

1. Open Command Palette → **Templater: Create new note from template**
2. Choose `ontology_metric.md`
3. Name it `Cadence`
4. The file is automatically created and moved to `03_Ontology/metrics/`
5. Fill in the Definition, Equation, Domain, and Unit fields

> **Check the Processing Queue** (`00_Inbox/Processing Queue.md`) to see all missing ontology links across all notes — you don't need to hunt for them manually.

This step can be done at the time of the paper note or later by using `00_Inbox/Processing Queue.md`

---

## Key Navigation Points

| File | What it does |
|---|---|
| `00_Inbox/Processing Queue.md` | Papers pending insight extraction + missing ontology nodes |
| `00_Inbox/Insight Explorer.md` | Filter all insights by population, metric, method, or paper |
| `03_Ontology/ontology_map.md` | Live index of all defined ontology nodes by category |

---

## Creating an Insight Note

When you're ready to formalize an insight (immediately or in a batch session later):

1. Click the unresolved wikilink in the paper note
2. Obsidian creates a blank file — open Command Palette → **Templater: Create new note from template** → `insight_note.md`
3. The file auto-moves to `02_Insights/`
4. Fill the YAML frontmatter (population, metric, domain, property, method, citekey)
5. Write one sentence below the frontmatter — the claim, ready to paste into a manuscript

---

## Writing Manuscripts

Manuscript citations are managed through the **Zotero Word plugin**, not through Obsidian. In Word:
- Use the Zotero toolbar to insert citations from your library
- The vault's `citekey` fields match your Zotero library keys, so you can search by citekey in the Zotero Word plugin

To retrieve insights for writing, open `00_Inbox/Insight Explorer.md` and filter by population, metric, or property.

---

## Common Questions

**Q: The Dataview tables are empty.**
A: Go to Settings → Community Plugins and confirm the Dataview toggle is on.

**Q: Zotero Integration can't find my papers.**
A: Make sure Zotero is open and running in the background. The plugin connects to Zotero over a local port.

**Q: I created a note from a template but it stayed in the root folder.**
A: Use **Templater: Create new note from template** from the Command Palette. The auto-move runs when Templater processes the template — it does not run if you create a blank file by clicking an unresolved link.

**Q: A wikilink I typed is showing up in the Processing Queue as a missing ontology node.**
A: That's expected. Create the node using the matching template. If it's an insight title (7+ words), the queue filters it out automatically.

**Q: When should I create a new ontology node vs. just writing text?**
A: Create a node if you expect to reference this concept from 2+ papers. For one-off qualifiers, use plain text parentheticals in Study Context instead.
