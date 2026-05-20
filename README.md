# Cambridgeshire-Road-Casualties

Analysis of road casualties across Cambridgeshire (2020–2024), with a focus on identifying danger spots, cyclist safety trends, and whether road infrastructure investment is reflected in casualty data.

---

## Project summary

This project uses the UK government's official STATS19 collision database to map where Cambridge casualties are occurring, identify high-risk locations, and examine whether casualty rates are improving over time. Cambridge is one of the most cycling-intensive cities in the UK, with over 30% of commuters travelling by bike. The analysis is intended to produce insights relevant to Cambridgeshire County Council, Cambridge City Council, and transport planning teams working on active travel and road safety policy.

---

## Key questions

- Where are the highest concentrations of road casualties in Cambridgeshire?
- How has the total number of casualties changed year on year since 2020?
- Are serious and fatal casualties declining faster than slight injuries?
---

## Tools used

| Tool | Purpose |
|------|---------|
| Python (pandas, matplotlib, folium) | Data cleaning, filtering, analysis, map visualisation |
| SQL (BigQuery) | Aggregation, year-on-year calculations, severity breakdowns |
| Tableau Public | Interactive dashboard — danger spot map + trend charts |

---

## Data sources

| Dataset | Source | Licence |
|---------|--------|---------|
| STATS19 Collisions 2020–2024 | [GOV.UK Road Safety Open Data](https://www.gov.uk/government/statistical-data-sets/road-safety-open-data) | OGL v3 |
| STATS19 Casualties 2020–2024 | [GOV.UK Road Safety Open Data](https://www.gov.uk/government/statistical-data-sets/road-safety-open-data) | OGL v3 |
| STATS19 Data Guide (lookup codes) | [GOV.UK Road Safety Open Data](https://www.gov.uk/government/statistical-data-sets/road-safety-open-data) | OGL v3 |

All data is published by the UK Department for Transport under the [Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/).

---

## Data governance & ethics

**No personal data is used.** STATS19 data is anonymised — no names, personal identifiers, or addresses are present. GPS coordinates are recorded at collision location only, not at casualty home address level.

**GDPR consideration.** This dataset contains location data for road collisions. No attempt is made to identify individuals. All analysis is aggregate or location-based only.

**Limitations.** STATS19 only captures collisions reported to the police. Minor collisions and near-misses are not recorded, meaning casualty counts are likely an underestimate — particularly for cyclists, who are known to under-report incidents. No causal claims are made about infrastructure investment and casualty trends without supporting evidence.

**Data note.** The severity of casualties in STATS19 has been subject to adjustment by DfT due to changes in reporting methodology across police forces. Adjusted severity figures are used in this analysis where available.

---

## Key findings

Cambridge Road Casualties & Hotspots (2020–2024)
Executive Summary

Road casualties in Cambridge peaked in 2022 and remain concentrated in North Cambridge, particularly Arbury and Chesterton, with pedestrians and car occupants accounting for the majority of incidents.

---

## Project structure

```
├── data/
│   ├── collisions_cambridgeshire.csv
│   └── casualties_cambridgeshire.csv
├── sql/
│   └── casualty_analysis.sql
├── notebooks/
│   └── casualty_analysis.ipynb
└── dashboard/
    └── tableau_public_link.md
```

---

## Dashboard

[[View on Tableau Public](#) (https://public.tableau.com/authoring/CambridgeRoadCasualties2020to2024/CambridgesRoadCasualties/Cambridge%20Road%20Casualties%20%26%20Hotspots%20(2020%E2%80%932024)#1)

---

## What I'd do next

- Add cycling infrastructure data (cycle lane locations from Cambridgeshire Open Data) to test whether danger spots correlate with gaps in the cycle network
- Compare Cambridgeshire casualty rates per capita against other university cities (Oxford, Bristol, Leeds)
- Build a severity prediction model — which road characteristics predict serious vs slight casualties?

