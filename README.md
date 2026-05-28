# CHRONIC-TIRE-PRESSURE-LOSS-DETECTION-AT-FLEET-SCALE

> *An automated system to detect chronic tire pressure data anomalies and slow leaks in large-scale vehicle fleets.*

[![Conference](https://img.shields.io/badge/CIKM-2026-blue.svg)](https://www.cikmconference.org/)
[![Spark](https://img.shields.io/badge/Engine-PySpark%20%7C%20Azure%20Synapse%20%7C%20MS%20Fabric-orange.svg)](https://learn.microsoft.com/en-us/fabric/data-engineering/spark-overview)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Official replication package and benchmark artifacts accompanying the peer-reviewed paper:  
**"Chronic Tire Pressure Loss Detection at Fleet Scale: A Deployed Weak-Supervision Approach for IoT Trend Anomalies"** 
*Hai Yin, Jens Dorniak, Christian Beecks.* — **CIKM '26 (Applied Research Track)**.

---

## OVERVIEW

This repository contains the reference implementation and localized benchmark datasets for our deployed automated system tracking insidious, long-term slow air leaks across massive commercial logistics fleets. 

Deployed in production at **KRONE FLEET**, the system currently monitors **~15,900 tires across 2,600+ active commercial vehicles**, achieving a production-verified performance of **88% precision and 90% recall** at the segment level. The underlying computational framework is consolidated into a **single comprehensive notebook**, executing a unified three-stage intelligent pipeline:

1. **PREPROCESSING & SEGMENTATION:** Daily trend aggregation, intra-vehicle normalization, and structural segmentation of TPMS streams. *(Note: Proprietary GPS-based altitude and temperature compensation, as well as telematics cleaning steps applied to the raw telemetry, are omitted from this public release to preserve corporate hardware confidentiality.)*
2. **WEAK LABEL GENERATION:** Scalable deterministic labeling driven by physics-informed boundary conditions mapped directly onto segment tails.
3. **DETECTION & COVARIANCE TRACKING:** Distributed *Isolation Forest* combined with *Gradient Boosted Trees (GBT)* operating over 7-day sliding windows, temporally aggregated via our custom online tracking metric: **Soft-Excess-Mean**.

---

## 📂 REPOSITORY LAYOUT

```text
.
├── data/                  # Anonymized TPMS benchmark slices (Parquet format)
│   └── README.md          # Comprehensive data dictionary & feature schema
├── notebooks.ipynb        # Step-by-step Jupyter notebooks reproducing the pipeline
├── requirements.txt       # Unified python dependency tree
├── CITATION.cff           # Machine-readable citation file
└── LICENSE                # Open-source legal framework
```

---

##  ENVIRONMENT & PREREQUISITES

Our core pipeline is engineered for extreme data scales and is verified on **Apache Spark 3.2+**. It provides out-of-the-box native compatibility with **Azure Synapse Analytics Workspace** and **Microsoft Fabric (Data Engineering / Lakehouse)**. 

* **SynapseML Integration:** The anomaly scoring matrix leverages Microsoft's `SynapseML` ecosystem. It comes **pre-installed** inside Microsoft Fabric Spark runtimes (Runtime 1.2+).
* **Python Requirements:** `Python >= 3.8` natively backed by `pandas>=1.3`, `scipy>=1.7`, `pyarrow>=6.0`, and `seaborn>=0.11`.

---

##  QUICKSTART & LOCAL REPLICATION

To evaluate and execute this interactive replication package locally or within an integrated cloud workspace, perform the following commands:

### 1. Clone & Set Up Python Environment
```bash
git clone https://github.com/<org>/<repo>.git
cd <repo>
python -m venv .venv

# Windows Environment Activation
.venv\Scripts\activate          
# macOS/Linux Environment Activation
# source .venv/bin/activate     

pip install -r requirements.txt
jupyter lab
```

### 2. Local Cloud-Layer Bypass (For Reviewers)
To execute the notebooks end-to-end without linking to active enterprise Azure Data Lake Storage (ADLS) containers, we have embedded a relative path toggle at the top of the ingestion scripts. The local benchmark snippets in `data/` will automatically feed the pipeline smoothly.

```python
# --- CLOUD PRODUCTION INFRASTRUCTURE ---
# telematics_path = "abfss://prod-container@fleetstorage.dfs.core.windows.net/..."

# --- LOCAL REPRODUCTION LAYER (ENABLED BY DEFAULT) ---
fleet_modeling_path = "./data/1_fleet_modeling_demo.parquet"
out_of_sample_path  = "./data/2_out_of_sample_demo_finished.parquet"
```


---

## DATASET PRIVACY POLICY

The `data/` directory hosts a thoroughly randomized, anonymized example slice of TPMS telemetry sufficient to run the replication package end-to-end. To comply with corporate fleet operational privacy mandates, absolute geospatial tracking indicators and confidential routing vectors are stripped. The full production fleet dataset remains proprietary. Please refer to `data/README.md` for specific schema structures.

---

##  CITATION

If you leverage this architectural system, codebase frameworks, or benchmark datasets in an academic or industrial context, please cite our CIKM reference paper as configured in the sidebar or via the `CITATION.cff` asset.

---

##  LICENSE

* **Codebase:** Distributed openly under the permissive **MIT License** (see `LICENSE`).
* **Telemetry Data:** Provided strictly for academic peer-review and non-commercial validation use cases.

---


## CONTACT & CORRESPONDENCE

* **Hai Yin** — `hai.yin@krone-fleet.com` 
* **Jens Dorniak** — `jens.dorniak@krone.de`
* **Christian Beecks** — `christian.beecks@fernuni-hagen.de` 
