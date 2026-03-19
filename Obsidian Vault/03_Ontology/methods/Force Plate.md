
# Force Plate

Type: Measurement Method

Description:
Measures ground reaction force, typically measured in Newtons. Can be embedded into floors or used as a mobile system. Often used as the [[Gold Standard]]
Can use strain gages or piezoelectric 

Key specifications:
- Sampling rate: varies, could be 1000 Hz
- Sensor type: Force

Common uses:
- [[Jumping]]
- [[Gait Event Detection]]
- [[Kinetics]]

Compared to:
- Is the gold standard

Limitations:
- Not very portable
- Often linked to [[Optical motion capture]] systems
- Expensive

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
