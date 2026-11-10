# Lab 1 · Part C · Dataset profile: Deutsche Bahn delays in Cologne

## Task 5 · Find a dataset

### Where I searched

| Source | Kind | Search term | Hits | Useful? |
| --- | --- | --- | --- | --- |
| [Open.NRW](https://open.nrw) (includes Offene Daten Köln) | State and city portal | `Verspätung` | 1 | No: only live bus positions in Münster under a closed licence |
| [Open.NRW](https://open.nrw) | State and city portal | `kvb` | 8 | No delay data: only lifts, escalators, ticket offices and bike rental of the Cologne transport company KVB |
| [GovData](https://www.govdata.de) | National portal | `Pünktlichkeit` | 3 | Partly: two datasets on the punctuality of regional trains, but only in Schleswig-Holstein, not in Cologne; the third hit is unrelated |
| [GovData](https://www.govdata.de) | National portal | `deutsche bahn` | 36 | No delay data, but stations and the rail network |
| [Hugging Face](https://huggingface.co/datasets?search=deutsche-bahn) | Repository | `deutsche-bahn` | 8 | Yes: `piebro/deutsche-bahn-data` |

Public portals have no historical train delay data for Cologne; the useful archives are collected by private projects from Deutsche Bahn's public timetable API.

### Searching like a machine

[GovData API: `q=deutsche bahn`](https://www.govdata.de/ckan/api/3/action/package_search?q=deutsche%20bahn&rows=1)

- **Hits (`count`):** 36 (as of 10.11.26)
- **First hit:** Haltestellen Deutsche Bahn
- **Licence:** `license_id` is empty for the whole dataset; the licence (CC BY 4.0) is given for each file under `resources`.

### My choice

[piebro/deutsche-bahn-data](https://huggingface.co/datasets/piebro/deutsche-bahn-data): historical arrivals and departures with delays and cancellations, collected from Deutsche Bahn's public timetable API, as monthly Parquet files. The original publisher is Deutsche Bahn, but its API only shows current data, so this archive is the only way to get past months.

The data covers all of Germany, so I filter it to Cologne: in October 2026, it contains 25 stations in Cologne, for example Köln Hbf, Köln Messe/Deutz and Köln-Ehrenfeld. Until early November 2025, the archive only covers the ~100 biggest stations in Germany, so complete data for all Cologne stations starts in November 2025.
