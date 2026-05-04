# rxmanager-data

Public data repository for **RxManager Pro** — a practical clinical reference and prescription tool for junior doctors and medical students.

Served globally via jsDelivr CDN. Every commit is immediately available to all app users.

---

## Structure

```
/drugs
  drugs.json              ← all generic drug records
  products.json           ← all brand/product records

/conditions
  conditions.json         ← condition metadata
  prescriptions.json      ← prescription templates (iterations)
  iterations.json         ← reserved for future use
  prescription_drugs.json ← drug-prescription linking table

/reference
  specialties.json        ← specialty list with emoji
  drug_groups.json        ← group + subgroup taxonomy (fixed)
  formulas.json           ← formula types list (fixed)
```

---

## CDN URLs

Base URL:
```
https://cdn.jsdelivr.net/gh/omarabdo50m-dev/rxmanager-data@main
```

Example fetch:
```javascript
const drugs = await fetch('https://cdn.jsdelivr.net/gh/omarabdo50m-dev/rxmanager-data@main/drugs/drugs.json').then(r => r.json())
```

---

## Data Rules

- `isPublished: false` — default for all AI-generated or unreviewed records
- `group` / `subgroup` — must be exact strings from `reference/drug_groups.json`
- `moa` — maximum 60 words, no bracket prefix, flow logic only
- `therapeuticClass` / `pharmacologicalClass` — separate fields, ≤5 words each
- `brandAr` — copied verbatim from Step 1 extraction, never generated
- Every published record requires a `source` field

---

## Taxonomy

The `group` and `subgroup` fields use fixed strings defined in `/reference/drug_groups.json`. These strings are used verbatim in all data, all AI prompts, and all app code. Never abbreviated, never paraphrased.

---

## Workflow

1. Editorial work happens in Google Sheets
2. Reviewed records exported as JSON
3. JSON committed to this repo
4. jsDelivr CDN propagates to all users automatically
5. Full rollback available via GitHub commit history

---

*RxManager Pro — bridging the gap between textbook knowledge and real clinical practice*
