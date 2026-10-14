### Milestone 1: Project Proposal

##### 1. Team Members

- [Member 1 Name] - [Email / Student ID]
- [Member 2 Name] - [Email / Student ID]
- [Member 3 Name] - [Email / Student ID]
- [Member 4 Name] - [Email / Student ID] 

---

##### 2. The Problem

- **What we are building:** An end-to-end data processing and sensor calibration pipeline for micro-level air quality monitoring. Low-cost air quality sensors offer high spatial resolution but suffer from sensor drift and poor reliability. Instead of just visualizing raw Air Quality Index (AQI) values, our system ingests multi-source PM2.5 data, evaluates low-cost sensor credibility using statistical quality control, detects drift against official regulatory reference stations, and applies robust spatial-temporal regression to dynamically calibrate the data.
- **Target Audience:** Local residents who need dense, accurate micro-level air quality maps (e.g., to evaluate neighborhood-level pollution exposure), as well as environmental researchers looking for reliable quality-controlled low-cost sensor networks.

---

##### 3. The Data

- **Data Sources:**
  - **OpenAQ S3 Bucket / AWS Open Data**: High-frequency bulk dataset containing historical global air quality measurements (specifically focusing on PM2.5).
  - **EPA / Local Government Reference Stations**: Official regulatory station data retrieved via OpenAQ to serve as ground-truth calibration baselines.
- **Data Scale:** The raw global bulk dataset exceeds tens of gigabytes (millions of records). For this project, we will focus on a designated urban region (e.g., major California metropolitan area) covering multiple sensor networks over a multi-month/year window.
- **Access Status:** **Data access is already secured.** The dataset is fully available via public S3 buckets on AWS Open Data without requiring private API keys or access approvals.

---

##### 4. What "Done" Looks Like

Upon completion, our system will be able to perform the following core functions:

1. **Automated Multi-Source Ingestion & Spatial Aggregation:** Efficiently ingest and deduplicate high-volume sensor streams from OpenAQ using PySpark/Polars, mapping scattered coordinates to standardized spatial grids (e.g., Uber H3 spatial index or Geohash).
2. **Sensor Drift & Anomaly Detection:** Automatically flag malfunctioning, outlier, or degrading low-cost sensors by computing historical variance and spatial dissimilarity relative to neighboring reference stations.
3. **Robust Calibration Model:** Train and apply robust regression models (e.g., Huber/RANSAC regression) using nearby ground-truth stations to auto-correct low-cost PM2.5 readings.
4. **Interactive Air Quality Dashboard:** Deploy a web dashboard (using Folium/Mapbox) displaying a real-time, micro-level air quality heatmap with interactive toggles between uncalibrated raw data and calibrated sensor outputs.
5. **Validation & Metrics Reporting:** Evaluate model performance by reporting Root Mean Square Error (RMSE) reduction and calibration metrics before vs. after alignment with reference stations.

---

##### 5. Additional Considerations

- **Data Privacy/Sensitivity:** All data used in this project is publicly available environmental sensor data with no personally identifiable information (PII) or sensitive records.
- **Research/Course Overlap:** This project is developed solely for this course and does not overlap with existing thesis research or prior course submissions.
- **Technical Risk Mitigation:** To manage the computational challenge of large-scale spatial joins, we will utilize chunking/distributed processing (PySpark/Polars) and spatial indexing (H3) locally, avoiding rate-limit bottlenecks by leveraging direct AWS bulk downloads rather than live REST API calls.
