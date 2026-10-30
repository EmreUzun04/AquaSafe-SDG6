# Post-Earthquake Tent City Rapid Water Potability Triage System (SDG 6)

## Overview
Following major seismic disasters, municipal water pipelines and sewage networks suffer structural fractures, causing cross-contamination of groundwater and surface water supplies. In emergency tent cities, access to accredited microbiology and analytical chemistry laboratories (required to measure *Escherichia coli*, Nitrate $\text{NO}_3^-$, and dissolved heavy metals like Arsenic and Lead) is severely disrupted or delayed by 24–72 hours.

This project develops an end-to-end **Rapid Water Potability Triage System** powered by low-cost, real-time electrochemical and optical field sensors (**pH**, **Turbidity**, **Electrical Conductivity**, **Dissolved Oxygen**, **Water Temperature**) integrated with station-level **Meteorological Records** (**72-Hour Cumulative Precipitation** and **Ambient Temperature**) derived from the **Water Quality Portal (WQP)** and **Open-Meteo / NOAA** historical station archives.

---

## Key Features & Methodological Highlights
1. **Spatio-Temporal Hydro-Meteorological Dataset (`wqp_disaster_water_quality.csv`):**
   - Contains $N = 5,000$ geo-referenced, time-stamped water quality and weather station observations across five seismic-prone hydrological basins (`Hatay_Asi_Basin`, `Kahramanmaras_Ceyhan_Basin`, `Adiyaman_Goksu_Basin`, `Malatya_Euphrates_Basin`, `Marmara_Fault_Zone`).
   - Captures post-rainfall surface runoff and sewage intrusion dynamics that drive microbial (*E. coli*) and chemical (Nitrate, Heavy Metal) contamination.
2. **Zero Data Leakage & Class-Agnostic Imputation:**
   - Missing sensor readings ($3.7\% - 6.8\%$ across field channels) are imputed strictly after train-test splitting using a distance-weighted `KNNImputer(n_neighbors=5)` fitted **exclusively on the training input features ($X_{\text{train}}$)** without accessing the target variable ($y$).
3. **Regulatory Benchmarking (WHO & TS 266 vs. Machine Learning):**
   - Benchmarks non-linear ensemble models (**Random Forest** and **Gradient Boosting**) directly against the official **World Health Organization (WHO)** and **Turkish Standards Institution (TS 266)** physical sensor cutoff rules ($6.5 \le \text{pH} \le 8.5$, $\text{Turbidity} \le 5.0\text{ NTU}$, $\text{Conductivity} \le 2500\text{ }\mu\text{S/cm}$, $\text{DO} \ge 5.0\text{ mg/L}$).
   - Demonstrates that $16.6\%$ of all field samples suffer from **Hidden Laboratory Contamination** (passing physical sensor thresholds while failing laboratory *E. coli*, Nitrate, or Heavy Metal limits).

---

## Holdout Test Set Performance ($N = 1,000$)

| Model / Method | Accuracy (%) | Macro F1-Score | Unsafe Water Recall (%) | Safe Precision (%) | False Safe Cases (Critical Risk) | ROC-AUC |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **WHO & TS 266 Simple Cutoff Rule** | 84.20 | 0.8137 | 58.85 | 79.59 | 158 | 0.7943 |
| **Random Forest (Sensors + Weather)** | 95.70 | 0.9545 | 94.01 | 96.28 | 23 | 0.9843 |
| **Gradient Boosting (Sensors + Weather)** | **96.50** | **0.9630** | **95.57** | **97.24** | **17** | **0.9869** |

* **Key Takeaway:** The **Gradient Boosting** model increases contaminated water detection (**Unsafe Recall**) from **$58.85\%$ to $95.57\%$**, reducing life-threatening **False Safe** classifications by **$89.2\%$** ($158 \rightarrow 17$ cases) compared to relying solely on single-parameter WHO/TS 266 sensor cutoffs.

---

## Repository Structure
* `post_earthquake_water_triage.ipynb` — Fully executed Jupyter Notebook containing data exploration, regulatory failure analysis, class-agnostic imputation, model benchmarking, and the interactive 3-tier field triage prototype.
* `wqp_disaster_water_quality.csv` — Merged WQP field sensor and meteorological station dataset ($5,000$ records, $16$ attributes).
* `README.md` — Project documentation, methodology, and benchmark summary.

---

## Quick Start & Reproduction
```bash
pip install numpy pandas scikit-learn matplotlib seaborn jupyter
jupyter notebook post_earthquake_water_triage.ipynb
```
