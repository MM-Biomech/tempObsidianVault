
# Coefficient of Variation

Type: Statistic

Description:
A relative measure of variability that indicated the size of a standard deviation relative to its mean. 

Formula / Equation:
$$
\text{CV} = \frac{\text{Standard Deviation}}{\text{Mean}}
$$

Interpretation:
- Percentage, dimensionless
- High value is more variability relative to the mean

Assumptions / When to use:
- Comparing between datasets with different units or widely different means
- Understanding the variability of a metric

Common uses:
- [[03_Ontology/metric_domains/Variability|Variability]]

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

papers.length > 0
    ? dv.table(["Paper", "Year", "Status"], papers.map(p => [p.file.link, p.year, p.status]))
    : dv.paragraph("_No papers indexed yet._");

if (insights.length > 0) {
    dv.header(4, "Insights");
    dv.list(insights.map(p => p.file.link));
}
```
