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

Interpretation:
- Higher values indicate slower cadence and overall walking speed
- Lower values indicate faster stepping

---

## Celestra

Celestra Status:: Implemented

Algorithm / Implementation Notes:
spatiotemporal.py

<!-- If Implemented: brief description of the algorithm used, or a link to the internal doc / codebase reference. If Planned: note the intended approach or any dependencies. If Not Possible: note the technical reason (e.g. sensor location limitation, or sensor type not available). -->

Validated Against:
- [[Optical Motion Capture]]
- [[Force Plate]]

<!-- Wikilink to the reference method used for validation. Leave blank if not yet validated. Link to the relevant paper note once a validation study exists. -->

---

## Referenced In

```dataviewjs
const path = dv.current().file.path;
const papers = dv.pages('"01_Papers"')
    .where(p => p.file.outlinks.some(l => l.path === path))
    .sort(p => p.year, 'desc');
const currentTitle = dv.current().file.name;
const insights = dv.pages('"02_Insights"')
    .where(p =>
        p.file.outlinks.some(l => l.path === path) ||
        [p.population, p.activity, p.metric, p.method, p.domain, p.property]
            .flat()
            .some(v => String(v ?? '').toLowerCase() === currentTitle.toLowerCase())
    );

const refData = dv.pages('"04_Reference_Data"')
    .where(p => p.file.outlinks.some(l => l.path === path));

papers.length > 0
    ? dv.table(["Paper", "Year", "Status"], papers.map(p => [p.file.link, p.year, p.status]))
    : dv.paragraph("_No papers indexed yet._");

if (insights.length > 0) {
    dv.header(4, "Insights");
    dv.list(insights.map(p => p.file.link));
}

if (refData.length > 0) {
    dv.header(4, "Reference Data");
    dv.list(refData.map(p => p.file.link));
}
```
