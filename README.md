# Chronic-Tire-Pressure-Loss-Detection-at-Fleet-Scale
An automated system to detect chronic tire pressure data anomalies and slow leaks in large-scale vehicle fleets


## 🚀 Replication Quick Start & Environment Setup

To ensure seamless alignment with our PySpark execution environment, please configure your cluster infrastructure using the exact specifications below.

### 1. Cluster Dependency Configuration
Our pipeline is verified on **Apache Spark 3.2+** (configured natively within Azure Synapse Analytics). The core anomaly detection algorithm relies on Microsoft's **SynapseML** ecosystem. 

If running on a local cluster or standard Databricks, you **must** coordinate the following Maven dependency package inside your Spark session initiation:

* **Coordinates:** `com.microsoft.azure:synapseml_2.12:0.11.1` (or your corresponding Spark-compatible version)
* **Python Runtime:** `Python >= 3.8` with `pandas>=1.3`, `scipy>=1.7`, and `seaborn>=0.11`.

---

### 2. Local-Standard Code Adaption (Crucial for Reviewers)
To execute the interactive pipeline without access to our enterprise Azure Data Lake Storage (ADLS) container, we have embedded a **Local Parquet Compatibility Layer** at the beginning of the notebook.

In **Section 1 (Data Ingestion)** of the provided `CIKM_Tire_Pressure_Loss_Pipeline.ipynb`, simply toggle the storage paths from global cloud URIs to your local relative repository paths:

```python
# --- CLOUD INFRASTRUCTURE ROADMAPPED IN PAPER ---
# telematics_path_parquet = "abfss://prod-container@fleetstorage.dfs.core.windows.net/telematics/..."

# --- LOCAL REPLICATION PATH (ENABLED FOR REPRODUCTION) ---
fleet_modeling_path = "./data/1_fleet_modeling_demo.parquet"
out_of_sample_path  = "./data/2_out_of_sample_demo_finished.parquet"

# Load the local replication samples instantly
df_final = spark.read.parquet(fleet_modeling_path)
out_of_sample_df = spark.read.parquet(out_of_sample_path)
