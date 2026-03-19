# Literature Vault

A structured Obsidian research vault for wearable-sensor gait analysis literature.
Designed for labs working with neurological populations (Parkinson's disease, MS, CIDP, Foot Drop) who need to accumulate knowledge across papers and rapidly retrieve it for manuscript writing.

Built on **Obsidian** + **Zotero**, with Dataview, Templater, and Zotero Integration plugins.

---

## What's in this vault

- A folder system separating **paper notes**, **insight notes**, **reference data**, and an **ontology** (controlled vocabulary of populations, activities, methods, metrics, and clinical measures)
- Zotero Integration template that routes PDF highlights by colour into the correct note section automatically
- Live Dataview dashboards for tracking processing progress and retrieving insights for writing
- Templates for every note type with auto-move to the correct folder

---

## Prerequisites

Install these before cloning:

| Software | Purpose | Download |
|---|---|---|
| [Sourcetree](https://www.sourcetreeapp.com/) | Git client used to clone and sync this repo | sourcetreeapp.com |
| [Obsidian](https://obsidian.md/) | The application that runs the vault | obsidian.md |
| [Zotero](https://www.zotero.org/) | Reference manager — stores PDFs, metadata, and your annotations | zotero.org |

---

## Cloning the Repository with Sourcetree

### Step 1 — Open Sourcetree and start a new clone

Launch Sourcetree. On the main window, click the **Clone** button (or go to **File → Clone / New**).

![Sourcetree new tab](https://www.sourcetreeapp.com/dam/jcr:87d7e1fb-c820-413c-98ac-8d9f3c8d2c1e/hero-mac-screenshot.png)

---

### Step 2 — Enter the repository URL

In the **Source Path / URL** field, paste:

```
https://github.com/MM-Biomech/literatureVault.git
```

---

### Step 3 — Set the destination

In the **Destination Path** field, choose where on your computer the vault will live.

> **Recommendation:** Choose a location that is **not** inside a cloud-synced folder (OneDrive, Dropbox, iCloud). Cloud sync and Git version control on the same folder can conflict. If you want cloud backup, use Git (this repo) as your backup instead.

Example destination: `C:\Users\YourName\Documents\Research\literatureVault`

Leave the **Name** field as `literatureVault` (auto-filled).

---

### Step 4 — Clone

Click **Clone**. Sourcetree will download the repository. When complete, you will see the repository listed in Sourcetree's left sidebar.

---

### Step 5 — Open the vault in Obsidian

1. Open Obsidian
2. Click **Open folder as vault**
3. Navigate into the cloned folder and select the **`Obsidian Vault`** subfolder (not the root `literatureVault` folder)
4. Obsidian will load the vault

---

### Step 6 — Follow the in-vault quickstart

Once Obsidian opens, navigate to:

```
_setup_files/QUICKSTART.md
```

This file walks you through installing the required plugins (Dataview, Templater, Zotero Integration, Citations) and processing your first paper.

---

## Keeping the Vault Up to Date

When collaborators push changes (new templates, architecture updates, new ontology nodes):

1. Open Sourcetree
2. Select the `literatureVault` repository in the left sidebar
3. Click **Pull** (top toolbar)
4. Sourcetree will fetch and merge the latest changes

> **Note:** Your personal paper notes in `01_Papers/`, insight notes in `02_Insights/`, and reference data in `04_Reference_Data/` are tracked by Git. Coordinate with collaborators if multiple people are working on the same paper notes to avoid merge conflicts.

---

## Repository Structure

```
literatureVault/
└── Obsidian Vault/
    ├── 00_Inbox/           Processing queue, insight explorer, changelog
    ├── 01_Papers/          One note per paper (created by Zotero Integration)
    ├── 02_Insights/        Atomic scientific claims
    ├── 03_Ontology/        Controlled vocabulary nodes
    ├── 04_Reference_Data/  Structured numerical results from papers
    ├── 05_Projects/        Active research project notes
    ├── 06_Manuscripts/     Manuscript working notes
    ├── _setup_files/       Architecture docs, quickstart, LLM context
    └── _templates/         Note templates for all note types
```

---

## Documentation

| File | Contents |
|---|---|
| `_setup_files/QUICKSTART.md` | Software setup, plugin installation, first paper walkthrough |
| `_setup_files/Lab Vault System Architecture.md` | Full system design, folder roles, workflows, conventions |
| `_setup_files/LLM_CONTEXT.md` | Compact reference for AI assistants working with this vault |
| `00_Inbox/changelog.md` | Log of structural changes to the vault |
