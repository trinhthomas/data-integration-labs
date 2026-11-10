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

## Task 6 · Profile the dataset

### 1. Facts

| | Deutsche Bahn Data |
| --- | --- |
| Publisher | [piebro](https://github.com/piebro/deutsche-bahn-data) on Hugging Face; original publisher: Deutsche Bahn (public timetable API) |
| Link | [huggingface.co/datasets/piebro/deutsche-bahn-data](https://huggingface.co/datasets/piebro/deutsche-bahn-data) |
| Formats | Parquet (monthly processed files); the raw API responses are also available as Parquet |
| Size | 28 monthly files (2024-07 to 2026-10). The file for October 2026 has 369 MB, 15,211,477 rows and 23 columns; 218,119 of these rows are stops in Cologne |
| Coverage | Germany, from July 2024; one row per train stop (arrival and/or departure at a station). Until early November 2025 only the ~100 biggest stations, since then all stations; 25 stations in Cologne in October 2026 |
| Last update | 10.11.26; one new file per month |
| Licence | CC BY 4.0, stated "by Deutsche Bahn" in the README and in the metadata (`license: cc-by-4.0`) |

### 2. Stars

★★★: openly licensed, structured, and in an open, machine-readable format (Parquet). For the fourth star, stations and trains would need URIs; the dataset only uses codes such as the EVA station number `08000207` for Köln Hbf.

### 3. Open the data

I opened `data-2026-10.parquet` with DuckDB in Python, because LibreOffice cannot read Parquet, and filtered it to stations whose name starts with "Köln" (218,119 rows).

| Column | Minimum | Maximum | Mean |
| --- | --- | --- | --- |
| `delay_in_min` | −61 | 503 | 5.77 |
| `train_line_station_num` | 1 | 104 | 10.8 |

- **Empty cells:** `line_number` is empty in 8,142 rows. The README explains why: long-distance trains (ICE, IC, EC) have no line number.
- **Odd things:**
  - The README documents 18 columns, but the file has 23: `is_additional_stop`, `is_replacement_train`, `replaced_train_type`, `replaced_train_number` and `has_plan_record` are not documented.
  - 1,006 stops have a negative delay, down to −61 minutes; a train an hour early is unlikely, so these may be errors.
  - The maximum of 503 minutes is the night train NJ 469 at Köln Hbf on 24 October 2026.
  - 73 rows have no train type, train number and delay.
  - Köln Messe/Deutz appears with two EVA numbers (`08003368` and `08073368`).
  - The timestamps have no time zone.
- **Tool:** DuckDB (Python).

### 4. Data dictionary

| Column | Meaning | Type and unit | Example |
| --- | --- | --- | --- |
| `station_name` | Name of the station | text | `Köln Hbf` |
| `eva` | EVA number, the station's code at Deutsche Bahn | text (8 digits) | `08000207` |
| `train_type` | Type of train | text | `ICE`, `RE`, `S` |
| `delay_in_min` | Delay at this stop | integer, minutes | `101` |
| `time` | Actual time of arrival or departure | timestamp, no time zone | `2026-10-01 00:03:00` |

The publisher documents the columns in a schema table in the [README](https://huggingface.co/datasets/piebro/deutsche-bahn-data/blob/main/README.md), but five columns are missing there.

### 5. Licence

Yes, the dataset is open: CC BY 4.0 conforms to the Open Definition. When I reuse it, I must credit the source, link the licence and say if I changed the data, for example by filtering it to Cologne.

Attribution line (TASL):

> "Deutsche Bahn Data" by Deutsche Bahn, collected by piebro, [huggingface.co/datasets/piebro/deutsche-bahn-data](https://huggingface.co/datasets/piebro/deutsche-bahn-data), licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Filtered to stations in Cologne.

### 6. People

The data contains no personal data: it describes trains,
