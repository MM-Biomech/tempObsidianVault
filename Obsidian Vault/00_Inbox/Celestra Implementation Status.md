# Celestra Implementation Status

Live view of all metrics in the vault by Celestra implementation status. Status is set in the `## Celestra` section of each metric note using the `Celestra Status::` inline field.

Valid values: `Implemented` · `Planned` · `Not Planned` · `Not Possible`

---

## Implemented

```dataview
TABLE WITHOUT ID file.link AS "Metric"
FROM "03_Ontology/metrics"
WHERE celestra-status = "Implemented"
SORT file.name ASC
```

---

## Planned

```dataview
TABLE WITHOUT ID file.link AS "Metric"
FROM "03_Ontology/metrics"
WHERE celestra-status = "Planned"
SORT file.name ASC
```

---

## Not Planned

```dataview
TABLE WITHOUT ID file.link AS "Metric"
FROM "03_Ontology/metrics"
WHERE celestra-status = "Not Planned"
SORT file.name ASC
```

---

## Not Possible

```dataview
TABLE WITHOUT ID file.link AS "Metric"
FROM "03_Ontology/metrics"
WHERE celestra-status = "Not Possible"
SORT file.name ASC
```

---

## Status Not Set

Metrics that exist in the vault but have not yet been assigned a Celestra status.

```dataview
TABLE WITHOUT ID file.link AS "Metric"
FROM "03_Ontology/metrics"
WHERE !celestra-status
SORT file.name ASC
```
