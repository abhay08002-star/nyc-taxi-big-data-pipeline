# nyc-taxi-big-data-pipeline
 NYC Taxi Trip Big Data Optimization & Analytics Pipeline

## Project Overview
An end-to-end Data Engineering and Data Analytics project built in **Databricks** using **PySpark**, **Delta Lake**, and **SQL**. This pipeline ingests **11.19 million** raw NYC Yellow Taxi trip records (2025), enforces automated data quality validation, enriches location IDs with neighborhood names, optimizes storage via month partitioning, and uncovers key urban mobility insights.

##  Tech Stack
* **Platform:** Databricks Unified Data Analytics Platform
* **Processing Engine:** Apache Spark (PySpark)
* **Storage Format:** Parquet & Delta Lake (Partitioned by `pickup_month`)
* **Analytics & Visualization:** Spark SQL & Databricks Visualizations

##  Data Engineering Pipeline (ETL)
1. **Extract:** Combined multi-month Parquet trip records (`11,198,026` raw rows) and `taxi_zone_lookup.csv` (`265` zones) from Databricks Unity Catalog Volumes.
2. **Data Quality & Validation:** Filtered out cancelled, corrupted, and incomplete records (`trip_distance <= 0`, `fare_amount <= 0`, `passenger_count <= 0`), retaining **`8,579,020` clean records** (removing ~23.4% noisy data).
3. **Transform & Enrich:** Engineered `pickup_hour`, `pickup_month`, and `tip_percentage` features, and joined pickup/dropoff location IDs to map real NYC boroughs and neighborhoods.
4. **Load & Optimize:** Saved the cleaned dataset as a managed **Delta Table** (`workspace.default.nyc_taxi_clean`) partitioned by `pickup_month` to enable partition pruning and faster SQL query performance.

##  Key Analytical Insights (SQL)
* **Peak Rush-Hour Demand:** Evening commuter demand peaks at **6:00 PM (Hour 18)** with **625,837 trips**, while early morning drops to **40,554 trips** at **4:00 AM**.
* **Tipping Behavior:** **Credit Card** accounts for **7,369,802 trips** (~85.9% of rides) with an average tip of **26.14%**, compared to **1,056,915 Cash trips**.
* **Top Routes:** The #1 busiest corridor is **Upper East Side South → Upper East Side North** (**67,336 trips**, averaging **1.04 miles** and **$15.52** total fare).
