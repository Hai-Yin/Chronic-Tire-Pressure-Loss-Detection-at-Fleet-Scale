
This directory contains the fully randomized, anonymized, and normalized telematics benchmark datasets required to replicate the experimental results of our paper. 

To ensure commercial data privacy and eliminate geospatial tracking risks (e.g., reversing routes via altitude vectors), absolute location coordinates and raw data-cleaning streams are omitted. The data types and internal schemas are locked using high-precision binary Parquet format to prevent formatting drift or data truncation commonly caused by CSV conversions.

---

Core Dataset Descriptions

1. `1_fleet_modeling_demo.parquet`
Scope: 25 independent heavy-duty vehicles/trailers.
Target Utilization: Used to establish historical tire behavior profiles, construct and evaluate intra-vehicle trend differentials.

2. `2_out_of_sample_demo_finished.parquet`
Scope: 25 separate vehicles tracking a forward-looking timeline.
Target Utilization: Used to evaluate the model's anti-leak generalization performance in a simulated real-time inference window without temporal data leakage.

---

Data Schema & Feature Alignment

Both parquet artifacts share a structurally consistent, high-fidelity data schema:

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `mongoID` | `String` | Anonymized Telematic Box ID for the vehicle or trailer fleet asset. |
| `timestamp` | `timestamp` | Timestamp of data received. |
| `date` | `Date` | Physical observation timeline (Format: `YYYY-MM-DD`). |
| `pressure 17-1a` | `Double` | Highly calibrated tire pressure reading normalized to standard temperature (bar). |
