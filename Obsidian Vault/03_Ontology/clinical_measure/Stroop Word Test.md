# Stroop Word Test

Type: Clinical Measure

Purpose:
Assesses cognitive processing speed and executive function, specifically the ability to suppress a habitual response in favor of a less automatic one (cognitive inhibition). Commonly used as the secondary task in dual-task walking paradigms.

Administration:
Clinician-administered (verbal response)

Score range:
Number of correct responses in 30 seconds per condition (W, C, CW)

Interpretation:
- Higher scores in each condition indicate better processing speed
- A larger interference score (IG) indicates greater susceptibility to cognitive interference

Equation:
$$
\text{IG} = CW - \frac{W \times C}{W + C}
$$
IG: interference score. CW, W, and C are the number of correct responses in the color-word, word-only, and color-only conditions respectively.

Conditions:
1. W — read the name of colors
2. C — identify the color of rectangle patches
3. CW — identify the ink color of words with incongruent color-word combinations

MDC:
MCID:

Relevant populations:
- [[Parkinsons Disease]]
- [[Multiple Sclerosis]]
- [[Healthy Adults]]

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
