# NYC Yellow Taxi 2023 - Lakehouse Pipeline (Team T03)

We built a bronze, silver and gold pipeline in PySpark on Databricks Free Edition to answer one business question:

> **Where and when does a New York taxi fleet earn the most?**

Job posting we are working towards: Cognizant, Returnship - Azure Data Engineer. Gaps closed: Azure / big data technologies, ETL pipelines, Python / PySpark.

## Status

| Checkpoint | Content | Status |
|---|---|---|
| 1 | Job posting and gap matrix | Done |
| 2 | Project plan | Done |
| 3 | Bronze and silver notebooks, quality log, progress note, Agile write-up | **This repository** |
| 4 | Gold tables, dashboard, Databricks Job, README, governance note | Planned (due 24 Nov 2026) |

## Repository layout

```
notebooks/
    T03_CP3_Notebook.ipynb                Bronze + silver in one notebook (the file we submit)
docs/
  agile_approach.md                     Write-up: how we run the project the Agile way
  cp3_progress_note.md                  Five-line progress note for Checkpoint 3
```

## Data (not stored in this repository)

* **Source:** NYC Taxi & Limousine Commission (TLC), Yellow Taxi Trip Records, 2023 (12 monthly Parquet files) and `taxi_zone_lookup.csv`.
  Page: https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
* **Licence:** free public data from the City of New York. Credit: NYC TLC.
* The data files are large, so they are **not** committed (see `.gitignore`). Download them from the TLC page.

## How to run it (about 15 minutes of clicking, plus run time)

1. In Databricks Free Edition, import the two notebooks from `notebooks/` (Workspace, Import).
2. Run the first cells of `01_bronze_load` (they create the schema `workspace.taxi` and the volume `raw`).
3. Upload `yellow_tripdata_2023-01.parquet` and `taxi_zone_lookup.csv` to `/Volumes/workspace/taxi/raw/` (Catalog, workspace, taxi, raw, Upload to this volume).
4. Run `01_bronze_load` with **Run all**, then `02_silver_clean_and_quality` with **Run all**. This is the January test run.
5. To run the full year: upload the other 11 months, change `MONTHS_TO_LOAD = ["2023-01"]` to `MONTHS_TO_LOAD = ALL_MONTHS` in the settings cell of both notebooks, and run bronze, then silver.

Both notebooks stop with a clear message if a file is missing and end with automatic checks that stop the run if something is wrong. They can be rerun safely: bronze and silver are overwritten, not duplicated.

## What the tables contain

| Table (in `workspace.taxi`) | Layer | Content |
|---|---|---|
| `bronze_taxi_trips` | Bronze | Every trip as delivered by TLC, lowercase names, one fixed type per column, plus `source_file` and `load_time` |
| `bronze_taxi_zones` | Bronze | Zone lookup (location ID, borough, zone, service zone) |
| `silver_taxi_trips` | Silver | Clean trips: no duplicates, zone names, decoded payment and rate types, `trip_minutes`, `fare_per_minute`, pickup date, hour, weekday and month, `is_airport_trip` |
| `quality_log` | Log | One row per month and run: rows in bronze, duplicates removed, trips removed by each reason, rows kept |

### Rules used to remove trips from silver

A trip is removed for the **first** reason that applies, so each removed trip is counted once:

1. `bad_times`: pickup or drop-off missing, or drop-off not after pickup
2. `outside_2023`: pickup year is not 2023
3. `over_24_hours`: trip longer than 1,440 minutes
4. `zero_distance`: distance missing or 0 or less
5. `non_positive_fare`: fare missing or 0 or less

Exact duplicates (identical in all 19 TLC columns) are removed first.


