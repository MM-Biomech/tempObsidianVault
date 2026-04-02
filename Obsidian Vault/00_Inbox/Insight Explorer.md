# Insight Explorer

Use this note to retrieve insights for manuscript writing, literature reviews, or project planning.
All queries read from `02_Insights/` YAML frontmatter. Results update automatically as new insight notes are created.

---

## All Insights by Population

```dataview
TABLE population, metric, domain, property, citekey
FROM "02_Insights"
SORT population ASC, metric ASC
```

---

## Filter by Population

Edit the population name in the WHERE clause to filter.

```dataview
TABLE metric, domain, property, file.link AS Insight, citekey
FROM "02_Insights"
WHERE population = "Healthy Older Adults"
SORT metric ASC
```

---

## Filter by Metric

```dataview
TABLE population, domain, property, file.link AS Insight, citekey
FROM "02_Insights"
WHERE metric = "Stride Velocity"
SORT population ASC
```

---

## Filter by Domain

```dataview
TABLE population, metric, property, file.link AS Insight, citekey
FROM "02_Insights"
WHERE domain = "Variability"
SORT population ASC
```

---

## Filter by Property

```dataview
TABLE population, metric, domain, file.link AS Insight, citekey
FROM "02_Insights"
WHERE property = "Validation"
SORT population ASC
```

---

## Filter by Method

```dataview
TABLE population, metric, property, file.link AS Insight, citekey
FROM "02_Insights"
WHERE method = "IMU"
SORT population ASC
```

---

## Filter by Paper (all insights from one source)

```dataview
TABLE population, metric, property, file.link AS Insight
FROM "02_Insights"
WHERE citekey = "kim2026InsoleDerivedPlantar"
SORT metric ASC
```

---

## Insights Missing Frontmatter Fields

Flags incomplete insight notes where key fields are blank.

```dataview
TABLE population, metric, domain, property, citekey
FROM "02_Insights"
WHERE !population OR !metric OR !citekey
SORT file.name ASC
```
