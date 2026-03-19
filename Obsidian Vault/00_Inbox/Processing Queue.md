## Papers Pending Insight Extraction

Papers with `status: reading` have been imported and reviewed — insight names are written in the note as wikilinks — but the actual insight files in `02_Insights/` have not been created yet.

```dataview
TABLE year, status
FROM "01_Papers"
WHERE status = "reading"
SORT year DESC
```

**To process a paper from this list:**
1. Open the paper note
2. Open the **Outgoing Links panel** (right sidebar) — unresolved links are listed there
3. For each unresolved insight wikilink: click to create the file, fill YAML frontmatter, write one sentence using the yellow highlight text below it as a draft
4. Set `status: processed` when done

---

## Unresolved Ontology References

Wikilinks used in paper notes or insight notes that point to a file that does not exist yet. These are likely ontology nodes (populations, activities, methods, metrics, statistics) that need a `.md` file created in `03_Ontology/`.

Insight-style links (sentence-form titles with 7+ words) are excluded — those are tracked by the insight extraction workflow above.

```dataviewjs
const WORD_THRESHOLD = 7;
const SCAN_FOLDERS = ['"01_Papers"', '"02_Insights"'];
const IMAGE_EXTENSIONS = ['.png', '.jpg', '.jpeg', '.gif', '.webp', '.svg', '.bmp', '.tiff'];

const LABEL_TO_TYPE = {
    'Population':      'Population',
    'Activity':        'Activity',
    'Methods':         'Method',
    'Statistics':      'Statistic',
    'Metrics Studied': 'Metric',
};

// First pass: collect all missing links and their source pages
const missing = new Map(); // linkName -> [{ page, typeHint }]

for (const folder of SCAN_FOLDERS) {
    for (const page of dv.pages(folder)) {
        for (const link of page.file.outlinks) {
            if (dv.page(link.path)) continue;
            const lower = link.path.toLowerCase();
            if (IMAGE_EXTENSIONS.some(ext => lower.endsWith(ext))) continue;
            if (link.path.trim().split(/\s+/).length >= WORD_THRESHOLD) continue;
            if (!missing.has(link.path)) missing.set(link.path, []);
            missing.get(link.path).push({ page, typeHint: '' });
        }
    }
}

// Headings that reset the label (sublabels will re-set within them)
const RESET_HEADINGS = new Set([
    '## Study Context', '## Results', '## Key Insights Extracted',
    '## Reference Data Extracted', '## Notes'
]);
// Headings that directly map to a type
const HEADING_TO_LABEL = {
    '## Metrics Studied': 'Metrics Studied',
};

// Second pass: read each source file to detect which section the link is under
for (const [linkName, entries] of missing) {
    for (const entry of entries) {
        const tFile = app.vault.getAbstractFileByPath(entry.page.file.path);
        if (!tFile) continue;
        const content = await app.vault.read(tFile);
        let lastLabel = '';
        for (const line of content.split('\n')) {
            const trimmed = line.trim();
            if (trimmed.startsWith('## ')) {
                // Section heading — reset or assign based on which section
                lastLabel = HEADING_TO_LABEL[trimmed] ?? (RESET_HEADINGS.has(trimmed) ? '' : lastLabel);
            } else {
                for (const label of Object.keys(LABEL_TO_TYPE)) {
                    if (trimmed.startsWith(label + ':')) { lastLabel = label; break; }
                }
            }
            if (line.includes(`[[${linkName}]]`)) {
                entry.typeHint = LABEL_TO_TYPE[lastLabel] || '?';
                break;
            }
        }
    }
}

// Render
if (missing.size === 0) {
    dv.paragraph("✓ No unresolved ontology references found.");
} else {
    const rows = [];
    for (const [linkName, entries] of missing) {
        const sources = [...new Set(entries.map(e => e.page.file.link))];
        const types   = [...new Set(entries.map(e => e.typeHint).filter(Boolean))];
        rows.push([`[[${linkName}]]`, types.join(', ') || '?', sources]);
    }
    rows.sort((a, b) => a[1].localeCompare(b[1]) || a[0].localeCompare(b[0]));
    dv.table(["Missing Note", "Type", "Referenced In"], rows);
}
```

**To process an item from this list:**
1. Note the **Type** column — this tells you which template to use:

| Type | Template | Destination |
|---|---|---|
| Population | `ontology_population.md` | `03_Ontology/populations/` |
| Activity | `ontology_activity.md` | `03_Ontology/activities/` |
| Method | `ontology_method.md` | `03_Ontology/methods/` |
| Statistic | `ontology_statistic.md` | `03_Ontology/methods/` |
| Metric | `ontology_metric.md` | `03_Ontology/metrics/` |
| Clinical Measure | `ontology_clinical_measure.md` | `03_Ontology/Clinical Measure/` |

2. Run **Templater: Create new note from template** from the command palette
3. Select the matching template
4. Enter the filename exactly as shown in the Missing Note column
5. The file will be created and automatically moved to the correct folder

---

## Missing Insight Files

Sentence-form wikilinks (7+ words) in paper notes that point to a file that does not yet exist. These are insights that have been named but not created.

```dataviewjs
const WORD_THRESHOLD = 7;
const IMAGE_EXTENSIONS = ['.png', '.jpg', '.jpeg', '.gif', '.webp', '.svg', '.bmp', '.tiff'];

const missing = new Map(); // linkName -> [page]

for (const page of dv.pages('"01_Papers"')) {
    for (const link of page.file.outlinks) {
        if (dv.page(link.path)) continue;
        const lower = link.path.toLowerCase();
        if (IMAGE_EXTENSIONS.some(ext => lower.endsWith(ext))) continue;
        if (link.path.trim().split(/\s+/).length < WORD_THRESHOLD) continue;
        if (!missing.has(link.path)) missing.set(link.path, []);
        missing.get(link.path).push(page);
    }
}

if (missing.size === 0) {
    dv.paragraph("✓ No missing insight files found.");
} else {
    const rows = [];
    for (const [linkName, pages] of missing) {
        const sources = [...new Set(pages.map(p => p.file.link))];
        rows.push([`[[${linkName}]]`, sources]);
    }
    rows.sort((a, b) => a[0].localeCompare(b[0]));
    dv.table(["Missing Insight", "Source Paper"], rows);
}
```

**To process an item from this list:**
1. Open the source paper note — find the wikilink in **Key Insights Extracted**
2. Use the Yellow highlight text below it as the body draft
3. Run **Templater: Create new note from template** → `insight_note.md`, name it exactly as shown
4. Fill YAML frontmatter (`population`, `metric`, `domain`, `property`, `method`, `citekey`) and write one sentence claim

---

## Incomplete Insight Notes

Insight files that exist in `02_Insights/` but are missing critical frontmatter. These were created (by clicking a wikilink) but not yet filled in.

```dataview
TABLE population, metric, citekey
FROM "02_Insights"
WHERE !citekey OR !population OR !metric
SORT file.name ASC
```

**To process an item from this list:**
1. Open the insight note
2. Fill the YAML frontmatter (`population`, `metric`, `domain`, `property`, `method`, `citekey`)
3. Replace the placeholder body with one sentence claim

---

## All Papers by Status

```dataview
TABLE year, status
FROM "01_Papers"
SORT status ASC, year DESC
```
