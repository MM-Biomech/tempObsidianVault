<%* await tp.file.move("03_Ontology/metrics/" + tp.file.title) %>
# <% tp.file.title %>

Type: Metric

Definition:


Equation:
$$
\text{Metric} = \frac{\text{numerator}}{\text{denominator}}
$$

Domain: 
[[]]

Unit:


Interpretation:
- Higher values indicate:
- Lower values indicate:

---
## Celestra

Celestra Status:: 
<!-- Implemented | Planned | Not Planned | Not Possible -->

Algorithm / Implementation Notes:

<!-- If Implemented: brief description of the algorithm used, or a link to the internal doc / codebase reference. If Planned: note the intended approach or any dependencies. If Not Possible: note the technical reason (e.g. sensor location limitation, or sensor type not available). -->

Validated Against:
- [[]]

<!-- Wikilink to the reference method used for validation (e.g. [[Motion Capture]], [[Force Plates]]). Leave blank if not yet validated. Link to the relevant paper note once a validation study exists. -->

---

## Referenced In

```dataviewjs
const path = dv.current().file.path;
const currentTitle = dv.current().file.name;

const papers = dv.pages('"01_Papers"')
    .where(p => p.file.outlinks.some(l => l.path === path))
    .sort(p => p.year, 'desc');

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
