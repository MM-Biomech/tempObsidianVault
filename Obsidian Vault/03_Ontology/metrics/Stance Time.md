
# Stance Time

Type: Metric

Definition:
The time spent when the foot is on the ground. Encompasses [[Foot Strikes]], [[Foot on Floor]], and [[Heel Rise]]. When both feet are in stance, they are in double support

Domain: 
[[]]

Unit:
seconds 

Interpretation:
- Higher values indicate: less healthy behaviour, possibly lower walking speed, higher [[Double Support Time]]
- Lower values indicate: more healthy behaviour, possibly higher walking speed

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
