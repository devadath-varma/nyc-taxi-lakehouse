---
title: "Checkpoint 3: Progress Note"
---

**Team T03** | James Mathew (BA05024) | Ram Kumar (BA05045) | Devadath Varma (BA05020) | S Saurav (BA05050) | Abhishek Manuel N (BA05004) | Kevin Ruban (BA05028)

**Project:** where and when a New York taxi fleet earns the most | **Repository:** [PASTE GITHUB LINK HERE]



1. **Bronze done.** We loaded 12 monthly Yellow Taxi files for 2023 and the zone lookup into Delta tables on Databricks, with fixed column types, a source file name and a load time: 38,310,226 trips in `bronze_taxi_trips`.
2. **Silver done.** With PySpark we removed 2 duplicates, joined zone names, decoded payment and rate types, and added trip minutes, fare per minute, hour, weekday and month.


