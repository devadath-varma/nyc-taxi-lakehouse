---
title: "Checkpoint 3: Progress Note"
---

**Team T03** | James Mathew (BA05024) | Ram Kumar (BA05045) | Devadath Varma (BA05020) | S Saurav (BA05050) | Abhishek Manuel N (BA05004) | Kevin Ruban (BA05028)

**Project:** where and when a New York taxi fleet earns the most | **Repository:** [PASTE GITHUB LINK HERE]



1. **Bronze done.** We loaded 12 monthly Yellow Taxi files for 2023 and the zone lookup into Delta tables on Databricks, with fixed column types, a source file name and a load time: [TOTAL BRONZE ROWS] trips in `bronze_taxi_trips`.
2. **Silver done.** With PySpark we removed [DUPLICATES] duplicates, joined zone names, decoded payment and rate types, and added trip minutes, fare per minute, hour, weekday and month; [ROWS SILVER] trips ([PCT KEPT]%) are in `silver_taxi_trips`.
3. **Quality log done.** Each removed trip has one reason, saved per month in `quality_log`: bad times [N], outside 2023 [N], over 24 hours [N], zero distance [N], non-positive fare [N]; for every month, bronze rows = duplicates + removed + silver rows.
4. **What broke and how we fixed it.** [Example: TLC changed column types and the airport fee spelling between months, so we read each file separately and cast every column to one type. Replace with your own real problem and fix.]

